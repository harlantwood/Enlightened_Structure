---
title: "Software Zero ::: Technical Architecture"
author: Harlan Knight Wood, Jack Senechal, Travis Wellman
layout: post
---

We are organizing our development efforts around the launching of "[Software Zero][]" -- the minimum viable slice of massively parallel creative collaboration.  

What we are building: 

 * Composed of thin components which communicate over well-defined HTTP interfaces
 * The MVP must be compelling: people want to use it, and keep coming back
 * Building on existing components where they exist

Assumptions
===========

Publishing
  : People publish their content however they choose, eg blogs, wikis, Google Docs, etc.

NodeCollective
==============

 * The domain owner can give their domain, e.g. nanotechdesertsolar.com, to the commons as a "node collective".
 * This allows the user Steve to visit the nanotechdesertsolar.com node collective, and register his site, nanotechdesertsolar.steve77.com as a nanotechdesertsolar fork.         
 * When a friend of Steve's visits nanotechdesertsolar.com, they see his fork prominently featured, as part of an interactive navigable data visualization of all nodes of interest, according to the specific users' filters, which are drawn from their trust network.

Data Visualization / Data Navigation
====================================

 * View the node collection that is the intersection between this node collective (eg “nanotechdesertsolar”) and the viewer's trust network
 * Radial node network interface
 * Navigate the node collections' radial node/edge interface
 * One node is central, surrounded by nodes of interest to the viewer -- "related" through topic, trust metrics, etc
 * When you click on a node, it zooms into full view (ie you are on that "page" or node), but navigation is still present around the edges, eg the network is present but compressed around the edges, or hints of the network are present

Trust Filters
=============

Information in the data visualization is informed by users' trust ratings of authors and content. &nbsp; [read more &raquo;](/Trust_Exchange)

Remixing &amp; Merging Changes
==============================

Authors can drop in JavaScript snippet to make a fork button on their page, and show other available forks (through NodeCollective)

Users submits documents to compare, and a diff is displayed.

Merging is an interactive process that happens on the client side, in the diff tool. The resulting document can be saved to the node store. &nbsp; [read more
&raquo;](/ForkDiffMerge)

Under the Hood
==============

BaseParadigm
------------

At a low level, everything rests on the node stores and graph edges of [BaseParadigm][].


Content Nodes 
-------------

* Contain data that will be served to the users' web browser; for example, a video or the HTML of your home page
* Have "format" metadata attached, for example "html", "markdown", "jpg"

Fragment Nodes
--------------

* Contain data with no intrinsic "format"
* For example, storing the relationhip: "Jack Senechal" "is the author of" "https://gist.github.com/823686" creates (among others) a fragment node "Jack Senechal" (sha512:98ecee1de7...)

Graph Edges 
-----------

Rich "edges" connect the nodes, containing:

* Subject, predicate, object
* Authors, patterns, assumptions
  
Technologies under consideration
--------------------------------

* [Smallest Federated Wiki][]
* [Camlistore][]
* [Riak][]: "An open source, highly scalable, fault-tolerant distributed database"
* [Bitcask][]: Riak's "Log-Structured Hash Table for Fast Key/Value Data"



[BaseParadigm]: /BaseParadigm
[Bitcask]: http://downloads.basho.com/papers/bitcask-intro.pdf
[Camlistore]: http://camlistore.org
[ForkDiffMerge]: /ForkDiffMerge
[Riak]: http://labs.linkfluence.net/nosql/2011/03/07/moving_from_couchdb_to_riak.html
[Smallest Federated Wiki]: http://fed.wiki.org
[Software Zero]: /Software_Zero