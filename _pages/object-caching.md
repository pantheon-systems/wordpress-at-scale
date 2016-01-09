---
ID: 16
post_title: Object Caching
layout: page
published: true
---

## Object Caching

### Persistent Object Caching Speeds Up Dynamic Pageviews

As a content management system, WordPress is naturally heavily dependent on its database, and database efficiency is crucial to scaling WordPress. If requests to your website generate a large number of database queries, your database server’s resources can become overwhelmed. With your database server overloaded, your site performance and uptime will suffer across the board.

In 2005, WordPress introduced its internal object cache — a way of automatically storing any data from the database (not just objects) in PHP memory to prevent unnecessary queries. However, out of the box, WordPress will discard all of those objects at the end of the request, requiring them to be rebuilt from scratch for the next pageload. Not very efficient.

Luckily, WordPress easily integrates with persistent storage backends like Redis or Memcached, making it possible to persist the object cache between requests. This speeds up PHP execution time while lessening the load on the Database, a real win-win scenario.

<img src="https://raw.githubusercontent.com/pantheon-systems/wordpress-at-scale/master/diagrams/object_cache.png" width="1100" title="Persistent Object Cache" />

Much like reverse proxy caching for pages, object caching is an established pattern in software development. It is an element to every large-scale application architecture, from Facebook or Google Docs to WordPress.com. Your WordPress site should be no exception.

Persisting database objects with a high-performance storage backend is a must-have for scaling WordPress for logged in users and dynamic pages. Without it, the inefficiency of regenerating the data in the object cache will start to hurt the performance of your website, particularly as site complexity and dynamic traffic increase.

While it’s possible to persist objects within a single PHP instance (e.g. APC), scaling your object cache requires sharing persistence layers among PHP Application servers. If you don’t share the persistent object cache values between PHP application servers, you’ll quickly run into problems of “cache (in)coherency” — when your application servers have different versions of cached objects, leading to buggy behavior.

Further, for all that object caching gives WordPress automatically, it is of even more value for developers when optimizing a particular use-case. The challenges of serving varying data to many concurrent logged-in users, or high volumes of dynamic traffic, are the hard problems are that engineers love, and there is no “one size fits all” solution.

WordPress stores its object cache in as simple named key=&gt;value pairs, so there many backends can serve as a persistent object cache. The most common open source tools for persistent object caching are Memcached and Redis. In addition there are cloud services (e.g. AWS’s ElastiCache, Azure’s Managed Cache) that provide equivalent functionality.

### Challenges:

*   **Complexity:** this is yet another layer in the stack, and it can create challenges to run operationally. In addition, you will need to make sure you have the same Object Caching solution present for development environments, and as part of your acceptance testing / QA process.
*   **Invalidation:** If your site is actively used, WordPress data can be updated frequently. However, you don’t necessarily want this activity to invalidate the object cache with the same frequency. You may need to intelligently purge specific keys within the object cache. 
*   **Eviction:** Most popular cache backends have storage limits, and us a LRU (last resource used) strategy for “evicting” items from the cache when more room is needed. This can create unexpected expirations and can sometimes confuse developers. 
*   **Optimization:** Using a persistent storage backend to cache objects for a highly dynamic application isn’t as simple as implementing a full page cache. You’ll need to smartly cache data based on an equation of how expensive it is to generate, how frequently it’s requested (aka likelihood of actually being served), and how much capacity you have in your persistent storage backend.

[do_widget_area]

[link-library settings="1" categorylistoverride="8"]
