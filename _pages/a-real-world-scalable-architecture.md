---
ID: 20
post_title: A Real-World Scalable Architecture
layout: page
published: true
---

## A Real-World Scalable Architecture

### Don't Panic

Putting all these components together, it’s clear that the “stack” has become a lot more complex since WordPress got started. Rather than the classic Linux Apache MySQL PHP (LAMP) configuration, you now have:

*   Linux
*   Varnish or Edge Cache Provider
*   Content Delivery Network
*   Apache or Nginx
*   PHP
*   Memcached or Redis
*   ElasticSearch or Apache Solr
*   MySQL

It doesn’t lend itself to a nice acronym, and a full diagram can start to feel overwhelming:

<img src="https://raw.githubusercontent.com/joshkoenig/wordpress-at-scale/master/diagrams/real_world.png" width="1100" title="Putting it all together" />

**Don’t panic!** This is why the discipline of DevOps exists. There are many professionals who are experienced with setting up this style of implementation, and many of the component pieces are now available as cloud services.

Also, you don’t have to run it yourself. This style of architecture is also available from many managed hosting and platform providers. If you are looking to outsource your website infrastructure — and increasingly common choice — you should now be armed with sufficient knowledge to evaluate various providers:

*   Do they provide load-balancing and reverse-proxy caching?
*   Is their infrastructure truly elastic? What is the turnaround time for scaling horizontally?
*   How do they handle the need for a network filesystem for uploads?
*   Which persistent object caching system(s) do they support?
*   Can they provide MySQL replication? Does it support HyperDB?
*   What options do they offer for a Search Index?

Beyond all that, there’s another key concern when it comes to running WordPress at scale, but it isn’t about the production infrastructure. It’s about how you can be agile and effective developing and debugging your site.

[do_widget_area]

[link-library settings="1" categorylistoverride="12"]
