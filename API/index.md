---
layout: default
title: Developer's Corner
---

Project Matrix
==============

|                          | Node Stores                 | Node Relationships        | Node Differences      | Node Merging                | Node Visualization       | Node Navigation    | Trust Ratings               |
|:-------------------------|:---------------------------:|:-------------------------:|:---------------------:|:---------------------------:|:------------------------:|:------------------:|:---------------------------:|
| [Trust Exchange][]       |                             |                           |                       |                             |                          |                    | &#x2713;                    |
| [Core Network][]         |                             |                           |                       |                             | &#x2713;                 | &#x2713;           |                             |
| [ForkDiffMerge][]        |                             |                           |  &#x2713;             |  &#x2713;                   |                          |                    |                             |
| [Base Paradigm][]        |  &#x2713;                   |  &#x2713;                 |                       |                             |                          |                    |                             |

[Trust Exchange]: /Trust_Exchange
[ForkDiffMerge]: /ForkDiffMerge
[Base Paradigm]: /BaseParadigm
[Core Network]: /Core_Network

<div class="hr-ellipsis">&nbsp;</div>

Enlightened Structure APIs
==========================

The Enlightened Structure technology stack is being implemented as a set of lean HTTP
APIs. *This is a work in progress, and these APIs are likely to change before their official
release.*  Your feedback is very welcome -- we want to make these APIs work for you.

HTTP API definitions below are defined as Rails-style routes.  A 2 line introduction to routing in Rails:

<pre class="brush: ruby; gutter: false; toolbar: false">
  get &quot;/patients/:id&quot; =&gt; &quot;patients#show&quot;
</pre>
<p>the GET request is dispatched to the <tt>patients</tt> controller&#8217;s <tt>show</tt> action with <tt>{ :id =&gt; &#8220;17&#8221; }</tt> in <tt>params</tt>.</p>

-- for more information see the [Rails Routing Guide].

NodeMap
-------

    post '/' => 'nodes#create'    # POST params: { :content => content_blob }   # returns key
    get  '/:key' => 'nodes#show', :constraints => { :key => CONTENT_ADDRESS }
    get '/' => 'nodes#index'

BaseParadigm
------------

See also [baseparadigm.org][]

    post '/' => 'edges#create'    
        #  POST params: 
        #    { 
        #      :subjects => subjects_sha512,
        #      :predicates => predicates_sha512,
        #      :objects => objects_sha512,
        #      :authors => authors_sha512,
        #      :assumptions => assumptions_sha512,
        #      :patterns => patterns_sha512
        #    }

    get '/:key' => 'edges#show', :constraints => { :key => CONTENT_ADDRESS }
    get '/' => 'edges#index'

NodeSentences
-------------

    post '/' => 'sentences#create'
        #  format: json|xml|yaml
        #  POST params:
        #    { :content => arbitrary_data_structure_of_values }
        #
        #  eg:
        #    { :content =>
        #       "{
        #           url: 'http://icanhascheezburger.com/',
        #           name: 'LOLCats Blog',
        #           categories: ['funny', 'cats', 'pictures']
        #        }"
        #    }

    get  '/:key' => 'sentences#show', :constraints => { :key => CONTENT_ADDRESS }
    get '/' => 'sentences#index'

Diff
----

    get '/nodes/compare/:before..:after', 'nodes#compare_blobs',
      :constraints => { :before => /#{CONTENT_ADDRESS}/, :after => /#{CONTENT_ADDRESS}/ }

    get '/nodes/compare/:before_url..:after_url', 'nodes#compare_from_urls'

Merge
-----

    post '/nodes/:id/merge' => 'nodes#merge', :constraints => { :id => /#{CONTENT_ADDRESS}/ }
        # POST params: { :patch => patch_text }

    get '/nodes/:id/merge/:patch' => 'nodes#merge', :constraints => { :id => /#{CONTENT_ADDRESS}/, :patch => /#{CONTENT_ADDRESS}/ }

    # todo: merge conflict resolution API

Trust Exchange
--------------

    post '/' => 'ratings#create'
        # POST params:
        # {
        #    :entity => entity_name,            # eg google.com
        #    :category => category_name,        # eg integrity
        #    :rating => [0..1]                  # eg 0.77
        #    :source => source_domain           # eg jacksenechal.com
        # }

    get  '/:key' => 'ratings#show', :constraints => { :key => CONTENT_ADDRESS }

    # show recent ratings of interest
    get '/' => 'ratings#index'

    # show ratings of an entity
    get '/entities/:entity' => 'ratings#index'

    # show ratings of an entity by a given user
    get '/users/:user/entities/:entity' => 'ratings#index'

    # show ratings of an entity by a given user within a category
    get '/users/:user/entities/:entity/categories/:category' => 'ratings#index'

    # show ratings by a given user within a category
    get '/users/:user/categories/:category' => 'ratings#index'

    # show ratings of an entity within a category
    get '/entities/:entity/categories/:category' => 'ratings#index'



[baseparadigm.org]: http://baseparadigm.org/
[Rails Routing Guide]: http://guides.rubyonrails.org/routing.html