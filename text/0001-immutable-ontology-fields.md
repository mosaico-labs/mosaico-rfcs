# Immutable Ontology fields

## Summary

`mosaicod` allows writers to push a topic with the same Ontology Tag as an already persisted one but with different field types. In other words, Ontology Tags aren't enough to identify the schema of the persisted data. This RFC proposes a [design](#design) that lets consumers rely on a single representation per Ontology Tag.

## Motivation

Queries are currently unable to handle the case of topics with the same Ontology Tag but schema fields with different type or missing schema fields ([#967](https://github.com/mosaico-labs/mosaico/discussions/967)). By applying the proposed solution, we won't have to care about the problem anymore.

As a side note, this would also simplify other aspects. For instance, by applying this RFC we wouldn't need to keep track of different versions of schemas linked to an Ontology Tag on the SQL DB (currently disambiguated with the `(ontology_tag, schema_hash)` tuple).

## Design

We can make `mosaicod` stricter by checking that each received schema doesn't change the type of any field from the schema we have stored under the same Ontology Tag (if any). New fields are added to the stored schema, and queries treat fields missing from a topic as `NULL`.

This design is based on the behavior of popular DBMS (see table below).

| DBMS          | Allows changing a field's type on write |
| ------------- | --------------------------------------- |
| MongoDB       | Yes unless validated                    |
| Elasticsearch | No                                      |
| InfluxDB      | No                                      |
| Cassandra     | No                                      |
| ClickHouse    | No                                      |
| SQL Standard  | No                                      |

## Drawbacks

`mosaicod` becomes less flexible in what it accepts.

## Alternatives

The main alternative considered is inferring the types while processing the query
- slows down query execution;
- requires validating some queries beforehand. E.g., the user wants to find the max across some topics but the schema of some of them changed the field type to string;
    - this one can also be solved by skipping rows not matching the type (more error prone since it silences the error).

## Open Questions

- **Question:** is there any specific use case that requires changing the type of Ontology fields across topics with the same Ontology Tag?
    - **Proposal:** in case the only use case is bridges with overlapping schemas, a tagged union type (Arrow's `Union`) could address the need. Doing this, only queries on union fields will carry the overhead from the type check/inference.
- **Question:** should we allow adding a new field on write?
    - **Proposal:** yes, we can open a different RFC once we have a motivation against that. The behavior of popular DBMS is shown in the table below.

| DBMS          | Allows adding a field on write |
| ------------- | ------------------------------ |
| MongoDB       | Yes                            |
| Elasticsearch | Yes                            |
| InfluxDB      | Yes                            |
| Cassandra     | No                             |
| ClickHouse    | No                             |
| SQL Standard  | No                             |

## From RFC to Discussion

These are the required Discussions:
- Validate Arrow schema on write;
    - check and add new fields atomically, so that concurrent uploads under the same Ontology Tag can't add the same field with different types;
- Quick Arrow schema comparison;
- Treat missing fields as `NULL` in queries;
- Tagged unions:
    - Store Arrow `Union` fields in Parquet, which has no union type (our own encoding, or `Variant`);
    - Add union support to the SDK;
    - Add union support for queries.

These are the tasks to carry if this one is accepted:
- drop multiple schema versions tracking;
- close [#967](https://github.com/mosaico-labs/mosaico/discussions/967).
