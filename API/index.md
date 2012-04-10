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
| [BaseParadigm][]        |  &#x2713;                   |  &#x2713;                 |                       |                             |                          |                    |                             |

<div class="hr-ellipsis">&nbsp;</div>

Enlightened Structure APIs
==========================

The Enlightened Structure technology stack is being implemented as a set of lean HTTP
APIs. *This is a work in progress, and these APIs are likely to change before their official
release.*  Your feedback is very welcome -- we want to make these APIs work for you.

HTTP API definitions below are defined as Rails-style routes.  Here is a two line introduction to routing in Rails:

{% highlight ruby %}

    get "/patients/:id" => "patients#show"

{% endhighlight %}

The GET request is dispatched to the <tt>patients</tt> controller's <tt>show</tt> action with <tt>{ :id =&gt; &#8220;17&#8221; }</tt> in <tt>params</tt>.

For more information see the [Rails Routing Guide].

Definitions
-----------

In the examples below, *ADDRESS_PATTERN* is a regular expression that matches common known cryptographic hash digest formats, eg SHA-1, SHA-512, etc.

NodeMap
-------

Simple key-value store for nodes.  

{% highlight ruby %}

    post '/' => 'nodes#create'
        # Required POST parameters:
        #     :content
        # Optional POST parameters:
        #     :format_mime_type
        #
        # Returns key, in SHA-512 format

    get  '/:key'         => 'nodes#show', :constraints => { :key => ADDRESS_PATTERN }
    get  '/:key.:format' => 'nodes#show', :constraints => { :key => ADDRESS_PATTERN }
    
    get '/' => 'nodes#index'

{% endhighlight %}

Compare
-------

Compares the *content* of two nodes, and determine if the contents are in some sense "equal" -- for example, by converting markdown to html, or by stripping whitespace from both nodes.

{% highlight ruby %}

    get '/:node1/:node2' => 'nodes#compare', 
        :constraints => { :node1 => ADDRESS_PATTERN, 
                          :node2 => ADDRESS_PATTERN }

    post '/' => 'nodes#compare_from_urls'
        # Required POST parameters:
        #     :node1_url  # eg http://mydomain.com/food.html
        #     :node1_url  # eg http://someguy.com/food-remix.html
        #
        # This POST creates nodes for the content at the given URLs if necessary,
        # and redirects to the canonical node compare GET url above

{% endhighlight %}

Diff
----

{% highlight ruby %}

    get '/:before..:after' => 'nodes#diff', 
        :constraints => { :before => ADDRESS_PATTERN, 
                          :after  => ADDRESS_PATTERN }

    post '/' => 'nodes#diff_from_urls'
        # Required POST parameters:
        #     :before_url  # eg http://mydomain.com/food.html
        #     :after_url   # eg http://someguy.com/food-remix.html
        #
        # This POST creates nodes for the content at the given URLs if necessary,
        # and redirects to the canonical node diff GET url above

{% endhighlight %}

Merge
-----

{% highlight ruby %}

    post '/nodes/:id/merge' => 'nodes#merge', 
        :constraints => { :id => ADDRESS_PATTERN }
        # Required POST parameters:
        #     :patch   # in standard unix patch format

    get '/nodes/:id/merge/:patch' => 'nodes#merge', 
        :constraints => { :id    => ADDRESS_PATTERN, 
                          :patch => ADDRESS_PATTERN }

    # todo: merge conflict resolution API

{% endhighlight %}

Trust Exchange
--------------

{% highlight ruby %}

    post '/' => 'ratings#create'
        # Required POST parameters:
        #     :entity_name            # eg google.com
        #     :category_name          # eg integrity
        #     :rating                 # eg 0.77 (in the range 0..1)
        #     :source_domain          # eg jacksenechal.com

    get  '/:key' => 'ratings#show', :constraints => { :key => ADDRESS_PATTERN }

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

{% endhighlight %}

BaseParadigm
------------

Under the hood, everything is stored as nodes and edges in [BaseParadigm][].  Note that BaseParadigm operates exclusively with SHA-512 keys.

{% highlight ruby %}

    post '/' => 'edges#create'    
        #  POST params: 
        #      :subjects_sha512
        #      :predicates_sha512
        #      :objects_sha512
        #      :authors_sha512
        #      :assumptions_sha512
        #      :patterns_sha512

    get '/:key' => 'edges#show', :constraints => { :key => ADDRESS_PATTERN }
    get '/' => 'edges#index'

{% endhighlight %}



[BaseParadigm]: /BaseParadigm
[ForkDiffMerge]: /ForkDiffMerge
[Rails Routing Guide]: http://guides.rubyonrails.org/routing.html
[Trust Exchange]: /Trust_Exchange
[Core Network]: /Core_Network