---
ID: 382
post_title: Searching for Scale
layout: page
permalink: >
  http://persch-gh2-wp-microsite.pantheon.io/searching-for-scale/
published: true
---
<a class="loopback" href="/query-performance/">J</a>

# Searching for Scale - test

## Improve User Experience and Database Performance With a Search Index

One of the first queries to hit the wall in terms of scalability is content search. It runs slowly if you have a large number of posts, and cannot produce results based on relevance. It also does not have any built in faceting or “drill down” capabilities, leaving many users wanting more from a features standpoint as well as speed.

This is a known weak spot for WordPress, and the good news is there are emerging best practices on scaling site content: using a dedicated search index. An index improves performance significantly, and allows a richer user experience. It can even help scale problematic queries not related to content searching.

Scaling search queries via an index gets those queries out of the database, allowing them to be handled by a dedicated high-performance subsystem.

(diagram here)

One of the most exciting techniques for scaling large sites with complex content is using the search index to handle a wider range of queries that would normally go to the database, taking this tool beyond the basic content search. With a proper search index backend, developers can implement various resource-intensive queries — autocompletes, recent post lists, category trees — to use the most efficient resource, speeding things up for users and avoiding “queries of death.”

Of course, you can always develop around many of the challenges of big datasets by optimizing your code to use object caching to reduce the volume of slow queries, and/or re-factor the queries themselves to be more efficient. However, the ability to “throw the queries at the index” is an excellent option to have at your disposal.

Most large-scale sites want a better answer for core content search, and the ability to use a search index as an alternate target for gnarly queries can be a bonus win from having that infrastructure in place. Most large scale WordPress sites make use of an ElasticSearch or ApacheSolr search index, though some also use AWS’s CloudSearch, which uses similar technology.

**Challenges**

*   **Overriding WP_Query():** most implementations of a search index backed involve overriding the built-in WP_Query() object. While this is relatively straightforward to do for vanilla out-of-the-box WordPress post search, doing it for more specific queries will require care and attention from a developer.
*   **Index Rebuilds:** while not common, you may come across a situation that requires you to rebuild your content index. This means being able to “fall back” to the database, at least temporarily.
*   **Complexity:** as with other dedicated subsystems, a search index is yet another piece of infrastructure to set up, monitor, and manage. While the payoffs are clearly worth it, this does become another ongoing responsibility to maintain. 

[do_widget_area]

[link-library settings="1" categorylistoverride="12"]

<a class="loopnext" href="/a-real-world-scalable-architecture/"><i class="fa fa-angle-down"></i></a>

<div class="pageloop" id="id22">
  <div>
    A Real-World Scalable Architecture
  </div>
</div>
