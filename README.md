# Mosaico RFCs

> [!WARNING]
> The RFC process is at an early stage and not stable yet. The way RFCs are
> written, discussed and approved may change.

An RFC (*request for comments*) is a high-level design of a change to
[Mosaico](https://github.com/mosaico-labs/mosaico): the problem it solves,
how it works, its drawbacks and the questions still open.

This repository is where those designs are written and discussed. Everyone
can contribute to a design while it is open: comment on it, question it, or
propose changes to it, until it reaches a shape the maintainers agree on.

Once approved, an RFC is split into parts. Each part starts with a
**discussion** in the Mosaico repository, to check that the way it will be
implemented is reasonable. Then it follows the Mosaico
[contribution guidelines][contributing]: one or more **issues**, each
solved by one or more **pull requests**. See
[From an RFC to the code][to-code].

## Why RFCs

When a design is too large for a discussion, splitting it across many
discussions, issues and pull requests makes it hard to see as a whole.
RFCs keep these large designs written down, each in a single document:

- **They track how the designs of Mosaico evolve.** Each RFC records a
  design, the alternatives considered and the reasons for the choices
  made. A new RFC that changes an old design shows what changed and why.
- **They are always in one place.** Anyone can read the approved designs
  of Mosaico in this repository, without searching through many
  discussions, issues and pull requests.

## When you need an RFC

Most changes do not need an RFC: they can start directly with a
[discussion][discussions] in the Mosaico repository.

Write an RFC when the design matches at least one of these cases:

- It spans several parts of Mosaico at once, such as the Python SDK, the
  protocol, `mosaicod`, the store and the database.
- It is too long or too complex for a single discussion, which must stay
  short and easy to read.
- It needs many discussions just to explain the idea, without talking about
  the code.
- It changes this RFC process.

If your idea is big and complex, takes a lot of text to explain, and you
are not sure whether its whole design is reasonable or fits Mosaico, write
an RFC, so that the maintainers can help you shape the design as a whole.

If your idea is a feature that can be explained in a short and clear way,
and it stands alone without affecting other parts of Mosaico, open a
[discussion][discussions] in the Mosaico repository instead.

**Bugs must never be turned into an RFC: always report them in a
[discussion][discussions].**

## What an RFC contains

An RFC should be understandable by someone who does not know the code, and
precise enough to be split into parts, each one becoming a discussion. It
usually has these sections:

- **Summary**: a short description of what the change adds, why, and how
  it works at a high level, so that a reader gets the idea without reading
  the rest of the RFC.
- **Motivation**: the problem it solves, and who is affected by it.
- **Design**: how it works, across the parts of Mosaico it touches. Explain
  the new concepts, the data that changes (for example ontologies,
  serialization formats, store layout, database) and the crates involved.
  Use diagrams only when they make the design clearer than text.
- **Drawbacks**: why we should *not* do this.
- **Alternatives**: the other designs considered, each described in
  short, without discussing them in depth. An alternative worth
  considering becomes a new RFC.
- **Open questions**: what is still to be decided. Write each one as a
  **Question:**, followed by a **Proposal:** when there is one. Questions
  about the design must be answered before the RFC is approved. Only
  questions that depend on the implementation can stay open.

Wrap the text at 79 columns, so that it reads well both in an editor and
on GitHub.

## The process

Each RFC is written and discussed in a pull request to this repository.

> [!NOTE]
> A pull request marked as **draft** contains an RFC that is still being
> written. Comments on a draft pull request are ignored: wait until it is
> marked as ready for review.

To write an RFC, follow these steps:

1. Fork this repository, create a branch named `my-feature`, and add a
   file `text/0000-my-feature.md`, where `my-feature` is a short,
   descriptive name of the RFC.
2. Write the RFC. Be honest about the drawbacks and the alternatives: an
   RFC that hides them is harder to accept.
3. Open a pull request. Then rename the file with the number of the pull
   request, for example `text/0042-my-feature.md`.
4. Everyone can comment on the pull request, and suggest changes to the
   text. A maintainer drives the discussion.
5. Address the comments by pushing new commits to the pull request. Do not
   squash or rebase them, so the history of the discussion stays readable.
   When a discussion happens elsewhere (a call, a chat), post a summary on
   the pull request. Write the answer to each open question in the RFC. A
   question that can only be answered while implementing, for example by
   measuring something, can stay open: it is answered later, in the
   discussion of the part it belongs to.
6. The RFC must be approved by at least **two maintainers**. An author who
   is also a maintainer cannot approve their own RFC. An RFC with open
   questions about the design cannot be approved. Once approved, the
   pull request is merged. Maintainers can instead close it when the RFC is
   rejected or postponed.

## From an RFC to the code

When an RFC is approved, the maintainers agree with the design. This
does not mean it will be implemented right away, or exactly as written.

To implement an approved RFC:

1. **Split the RFC into parts.** Each part can be implemented on its own,
   for example the ontology, a new crate, or a change to a background
   process.
2. **Open a discussion for each part**, in the
   [Issue category][discussions] of the Mosaico discussions. Link the RFC
   and the section the part comes from, and describe how you plan to
   implement it. The discussion checks that this way of implementing it is
   reasonable, and that it fits the roadmap.
3. **Follow the [contribution guidelines][contributing]** of the Mosaico
   repository from there: once the discussion is approved, one or more
   issues are opened, and each issue is solved by one or more pull
   requests.

## Changing an approved RFC

- An approved RFC changes rarely. Small corrections can be made with a
  pull request to this repository, but a substantial change needs a new
  RFC.
- While implementing, some details may turn out different from the RFC.
  Explain the differences in the discussions or the pull requests of the
  Mosaico repository. If they completely change the design, write a new
  RFC. The old one is not modified, so it records the design as it was
  when it was approved.

## Postponed RFCs

An RFC is postponed when it is a good idea, but it cannot be done now: the
project has other priorities, or the design depends on something not
decided yet.

A postponed RFC is closed, but not rejected. It can be reopened later:
comment on its pull request and explain what has changed.

## Credits

This process is adapted from the
[Rust RFC process](https://github.com/rust-lang/rfcs).

## License

Like Mosaico, the content of this repository is licensed under the
[Apache License, Version 2.0](LICENSE).

[to-code]: #from-an-rfc-to-the-code
[discussions]: https://github.com/mosaico-labs/mosaico/discussions/categories/issue
[contributing]: https://github.com/mosaico-labs/mosaico/blob/main/CONTRIBUTING.md
