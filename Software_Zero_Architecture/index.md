---
title: "Software Zero ::: Technical Architecture"
author: Harlan T Wood, Jack Senechal, Travis Wellman
layout: post
---

Enlightened Structure Software Zero is designed to be _the minimum viable slice of massively parallel collaboration_:

 * Composed of slim components, elucidated below
 * Components are open source, with maximally permissive licensing (MIT/GPL or CC0)
 * We strongly prefer to build on existing components where they exist; we create the minimal unaddressed chunks where we see they are most needed

Open Your Project
-----------------

- Allow users to clone Creative Commons licensed material to [Smallest Federated Wiki][] instances

- Claiming a domain or subdomain -- eg jacksenechal.openyourproject.org -- automatically claims all of its subdomains, so the user can have:
  - project1.jacksenechal.openyourproject.org
  - project2.jacksenechal.openyourproject.org
  - project3.jacksenechal.openyourproject.org

- For example, Jack can clone the content from http://liveingreatness.com to liveingreatness.jacksenechal.openyourproject.org

- The site is crawled, all content pages come over

- An index page is created, so links to all pages are easily accessible

- At the time of forking, the user can choose between stripping content down to plain text, or keeping simple HTML (notably tables).
  
- Visualization system to drill down into curators, collections, and pages.

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
  
  

[BaseParadigm]: /BaseParadigm
[Bitcask]: http://downloads.basho.com/papers/bitcask-intro.pdf
[Camlistore]: http://camlistore.org
[ForkDiffMerge]: /ForkDiffMerge
[Riak]: http://labs.linkfluence.net/nosql/2011/03/07/moving_from_couchdb_to_riak.html
[Smallest Federated Wiki]: https://github.com/WardCunningham/Smallest-Federated-Wiki#readme
[Trust Exchange]: /Trust_Exchange
[Software Zero]: /Software_Zero
