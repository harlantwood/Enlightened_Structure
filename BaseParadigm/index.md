---
title: BaseParadigm
author: Travis Wellman, Harlan Knight, Jack Senechal
layout: post
---

BaseParadigm defines a way to use the internet agnostic of physical hardware. This shift nulls
borders defined by domain names, creating a commons and lowering the barriers to inclusion in
digital culture.

At the highest level, BaseParadigm tracks two kinds of data: blobs and graph edges.

Blobs are necessarily wrapped in a map of metadata, one field of which is content containing the
blob itself. The other fields are similar in function to http headers. They tell the BaseParadigm
client how to handle the blob. Most important is the type field which hints at default built-in
renderers that the client might use, but a set of specific renderers can also be given in another
field.

Where things start getting interesting is the graph edge data. Every link between documents is its
own edge document. Every link within a document is its own edge document. Edge documents
themselves may be split and inspected as a navigable set of edges and blobs, which may be added to
and removed from and reformed into a new version of the old edge.

Edges have six fields:

- Subjects
- Predicates
- Objects
- Authors
- Assumptions
- Patterns

Every field is a plural. Multiple values in fields means the BaseParadigm client should treat the
edge document as a set of all permutations of single value edges. That is, if there are two
subjects, two predicates, and two objects in an edge, it means that both subjects are connected to
both objects via both predicates. In this case there are eight items to consider.

It is also useful to consider permutations regarding Authors, Assumptions and Patterns because these
fields are about the edge itself. These fields form an integral part of graph navigation.

