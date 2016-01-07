---
ID: 18
post_title: Query Performance
layout: page
published: true
---
<a class="loopback" href="/object-caching/">J</a>

# Query Performance

## The Database is the Ultimate Bottleneck

Your website’s database is the ultimate bottleneck when scaling. The two caching strategies we’ve outlined mostly serve to prevent load on the database. But, when do you need to scale your database, an elastic architecture allows you increase your capacity for read queries through the use of replicas.

(diagram here)

WordPress has had support for scalable read replicas for quite some time via the HyperDB plugin. This allows you not only to scale out, but also to implement specific strategies for how queries use the master and replica instances.

For example, it’s easy to configure your site to use the master database for all requests related to administrative or logged-in functionality, while using replicas exclusively for anonymous traffic. This pattern ensures that content editors are always able to use the site, even if it’s under sustained heavy load for normal content-reading use.

## Avoiding “Queries of Death”

Scaling via database replication still assumes that your queries are generally performant. If your use-case means you have a content footprint (100s of thousands or millions of posts) the WordPress default query builder (aka WP_Query()) may generate “queries of death”: requests to the database that can take several seconds to compute.

These are called “queries of death” for a reason. They can suddenly and drastically affect site performance, even to the point of causing downtime. Long-running queries are intensive, often involving the creation of a whole temporary table to compute the result. They bog down database performance for all queries and tie up PHP application capacity, a lose-lose combination.

Slow queries block the PHP Application threads that kick them off. If they’re happening in high volume they can overwhelm even a horizontally scalable “elastic” infrastructure. Eventually all your PHP threads are waiting for slow queries to respond, at which point the site is effectively offline.

Even with best-practice architecture, an important part of scalability hygiene is reviewing query performance. MySQL has a built in capability called the slow query log, which will allows you to build and analyze data on your query times. You may also find value here in using application performance monitoring tools such as New Relic.

**Challenges:**

*   **Query routing:** the HyperDB plugin has a lot of options for distributing queries across your database instances, but it’s usually best to keep it simple for starters. While your specific use-case may require customization, it’s best to minimize the amount of change and moving parts as you take the first step away from a monolithic single-instance implementation.
*   **Replication lag:** while under ideal circumstances replication lag is nearly instantaneous, not all circumstances are ideal. You’ll need to be sure that your implementation can sanely handle multi-second lag, and you’ll need to monitor if lag spikes to unacceptable levels, or if replication breaks down alltogether. 
*   **Debuggability:** when dealing with troublesome queries, you not only need access to the slow query log, but also to safely and reliably replicate the situation order to conclusively resolve the issue. That means having an environment to debug in with all the data needed to trigger the slow query. It also means taking the time to isolate where in the site code the query is being generated, so that an alternative can be implemented.
*   **Regressions:** as noted above, the impacts from a query of death can be swift. For sites with large datasets, it is important to consider the implications of new queries, as well as to test them before they are released into production. 

[do_widget_area]

[link-library settings="1" categorylistoverride="11"]

<a class="loopnext" href="/searching-for-scale/"><i class="fa fa-angle-down"></i></a>

<div class="pageloop" id="id20">
  <div>
    Searching for Scale
  </div>
</div>