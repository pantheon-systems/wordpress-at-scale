---
ID: 382
post_title: Searching for Scale
author: Josh Koenig
post_date: 2015-12-22 16:14:52
post_excerpt: >
  Improve User Experience and Database
  Performance With a Search Index
layout: page
permalink: >
  http://www.scalewp.io/searching-for-scale/
published: true
---
## Enjoy Faster, More Relevant Results

### Improved User Experience and Database Performance? Yes, Please.

One of the first queries to hit the wall in terms of scalability is WordPress's built-in content search. It runs slowly if you have a large number of posts, and cannot produce results based on relevance. It also does not have any built in faceting or “drill down” capabilities, leaving many users wanting more from a features standpoint as well as speed.

This is a known weak spot for WordPress, and the good news is there are emerging best practices on scaling site content: using a dedicated search index. An index improves performance significantly, and allows a richer user experience. It can even help scale problematic queries not related to content searching.

Scaling search queries via an index gets those queries out of the database, allowing them to be handled by a dedicated high-performance subsystem.

<img src="https://raw.githubusercontent.com/pantheon-systems/wordpress-at-scale/master/diagrams/search_index.png" width="1100" title="Using a Search Index" />

One of the most exciting techniques for scaling large sites with complex content is using the search index to handle a wider range of queries that would normally go to the database, taking this tool beyond the basic content search. With a proper search index backend, developers can implement various resource-intensive queries — autocompletes, queries by postmeta, multi-taxonomy queries — to use the most efficient resource, speeding things up for users and avoiding “queries of death.”

Of course, you can always develop around many of the challenges of big datasets by optimizing your code to use object caching to reduce the volume of slow queries, and/or re-factor the queries themselves to be more efficient. However, the ability to “throw the queries at the index” is an excellent option to have at your disposal.

Most large-scale sites want a better answer for core content search, and the ability to use a search index as an alternate target for gnarly queries can be a bonus win from having that infrastructure in place. Most large scale WordPress sites make use of an ElasticSearch or ApacheSolr search index, though some also use AWS’s CloudSearch, which uses similar technology.

### Challenges

* **Overriding WP_Query():** most implementations of a search index backed involve overriding the built-in WP_Query() object. While this is relatively straightforward to do for vanilla out-of-the-box WordPress post search, doing it for more specific queries will require care and attention from a developer.
* **Index Rebuilds:** while not common, you may come across a situation that requires you to rebuild your content index. This means being able to “fall back” to the database, at least temporarily.
* **Complexity:** as with other dedicated subsystems, a search index is yet another piece of infrastructure to set up, monitor, and manage. While the payoffs are clearly worth it, this does become another ongoing responsibility to maintain.

<!--- Do not edit below this line. Automatically pulls in resources. -->

[social_links]
####Further Reading
[link-library settings="1" categorylistoverride="14"]