---
title: "Software Zero ::: Technical Architecture"
author: Harlan Knight, Jack Senechal, Travis Wellman
layout: post
---

Enlightened Structure Software Zero is designed to be _the minimum viable slice of massively parallel collaboration_:

 * Composed of slim components, elucidated below
 * Components are open source, with maximally permissive licensing (MIT/GPL or CC0)
 * We strongly prefer to build on existing components where they exist; we create the minimal unaddressed chunks where we see they are most needed

Smallest Federated Wiki
-----------------------
From Ward Cunningham, inventor of the original wiki, [Smallest Federated Wiki][] is designed from the ground up for users to be able to fork content from other users.  Supports simple dragging and dropping of text, images, and data *across sites*.  

FreePress
---------
 * Up: push your local content up to wiki-like nodes that allow others to fork your content.
 * Down: Crawl creative commons licensed websites and pull down the plain text version of their content.  You own your forks.  Remix as you see fit, and publish what you choose to the creative commons.

Radial Node Visualization and Navigation
----------------------------------------
 * Visually explore content collections 
 * Navigate the node collections' radial node/edge interface
 * One node is central, surrounded by nodes of interest to the viewer -- "related" through topic, trust metrics, etc
 * When you click on a node, it zooms into full view (ie you are on that "page" or node), but navigation is still present around the edges, eg the network is present but compressed around the edges, or hints of the network are present

Trust Filters
-------------

Information in the data visualization is informed by users' trust ratings of authors and content.  
&nbsp; 
[read more &raquo;][Trust_Exchange]

Remixing &amp; Merging Changes
------------------------------

Merging is an interactive process that happens on the client side, in the diff tool. The resulting document can be saved to the node store. 
&nbsp; 
[read more &raquo;][ForkDiffMerge]

NodeCollective
--------------

 * The domain owner can give their domain, e.g. nanotechdesertsolar.com, to the commons as a "node collective".
 * This allows the user Steve to visit the nanotechdesertsolar.com node collective, and register his site, nanotechdesertsolar.steve77.com as a nanotechdesertsolar fork.         
 * When a friend of Steve's visits nanotechdesertsolar.com, they see his fork prominently featured, as part of an interactive navigable data visualization of all nodes of interest, according to the specific users' filters, which are drawn from their trust network.

Graph / Node / Edge Stores
--------------------------

At a low level, everything rests on node stores and graph edges in content-addressable systems like [BaseParadigm][] or [Camlistore][].

* Content Nodes 
  * Contain data that will be served to the users' web browser; for example, a video or the HTML of your home page
  * Have "format" metadata attached, for example "html", "markdown", "jpg"
* Fragment Nodes
  * Contain data with no intrinsic "format"
  * For example, storing the relationhip: "Jack Senechal" "is the author of" "https://gist.github.com/823686" creates (among others) a fragment node "Jack Senechal" (sha512:98ecee1de7...)
* Graph Edges: rich "edges" connect the nodes, containing:
  * Subject, predicate, object
  * Authors, patterns, assumptions (see also [BaseParadigm][])
  
External Technologies Under Consideration
-----------------------------------------

* [Smallest Federated Wiki][]
* [Camlistore][]
* [Riak][]: "An open source, highly scalable, fault-tolerant distributed database"
* [Bitcask][]: Riak's "Log-Structured Hash Table for Fast Key/Value Data"



[BaseParadigm]: /BaseParadigm
[Bitcask]: http://downloads.basho.com/papers/bitcask-intro.pdf
[Camlistore]: http://camlistore.org
[ForkDiffMerge]: /ForkDiffMerge
[Riak]: http://labs.linkfluence.net/nosql/2011/03/07/moving_from_couchdb_to_riak.html
[Smallest Federated Wiki]: https://github.com/WardCunningham/Smallest-Federated-Wiki#readme
[Trust Exchange]: /Trust_Exchange
[Software Zero]: /Software_Zero