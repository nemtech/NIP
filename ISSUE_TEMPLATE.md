# NIP-XX - NIP Title

This document is provided as a template to get you started. Feel free to add, augment, remove, restructure and otherwise adapt the structure for what you need after cloning it.

## Summary

Each NIP must begin with an RFC 822 style header preamble. The headers must appear in the following order. Headers marked with "*" are optional and are described below. All other headers are required. (delete this before publish)

```
    NIP: <NIP number, or "?" before being assigned>
    * Layer: <Core Layer | API/WS | SDK | Applications | Library>
    Title: <NIP title; maximum 44 characters>
    Author: <list of authors' real names and email addresses>
    * Discussions-To: <telegram group>
    * Comments-Summary: <summary tone>
    Comments-URI: <links to issue page for comments>
    Status: <Draft | Active | Proposed | Deferred | Rejected |
            Withdrawn | Final | Replaced | Obsolete>
    Type: <Standards Track | Informational | Process>
    Created: <date created on, in ISO 8601 (yyyy-mm-dd) format>
    License: <abbreviation for approved license(s)>
    * License-Code: <abbreviation for code under different approved license(s)>
    * Post-History: <dates of postings to NEM mailing list, or link to thread in mailing list archive>
    * Requires: <NIP number(s)>
    * Replaces: <NIP number>
    * Superseded-By: <NIP number>
```

## Introduction/Abstract

: required

(feel free to rename this section to Introduction, Motivation, Abstract, whatever best suits your proposal.)

A high level overview of the proposal.

- Description / Scope
- An explanation of the reason it's needed

A short (~200 word) description of the technical issue being addressed.

## Specification

: required

The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current components.

## Motivation

: required

 The motivation is critical for NIPs that want to change NEM components. It should clearly explain why the existing component is inadequate to address the problem that the NIP solves.

## Design Decisions

: required

Discuss design decisions (including, as examples):

- Reason about correctness of the implementation.
- "Feel and fit" with existing core libraries.
- Performance and threading considerations.
- Potential conflicts with existing libraries, e.g. name clashes, IDE auto-import friction, etc.

The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work. The rationale should provide evidence of consensus within the community and discuss important objections or concerns raised during discussion.

## Implementation

: required

The reference implementation must be completed before any NIP is given status "Final", but it need not be completed before the NIP is accepted. It is better to finish the specification and rationale first and reach consensus on it before writing code. The final implementation must include test code and documentation appropriate for the NEM component.

Include the following:

- GitHub repository with the implementation
- Test cases

## Backwards compatibility

: optional

All NIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their severity. The NIP must explain how the author proposes to deal with these incompatibilities.

## Drawbacks

: required

Why should we not do this. Be honest, these questions will come out during the process anyway so it’s better to get them out up front.

## Alternatives

: optional

- What other possibilities have been examined?
- What is the impact of not implementing this proposal?

## References

: required

## History

| **Date**      | **Version**   |
| ------------- | ------------- |
| Jan 1 2018    | Initial Draft |
