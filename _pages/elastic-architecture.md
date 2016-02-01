---
ID: 11
post_title: Elastic Architecture
author: Josh Koenig
post_date: 2015-12-04 09:59:36
post_excerpt: >
  Horizontal Scalability Is the
  Scalability That Matters
layout: page
permalink: >
  http://www.scalewp.io/elastic-architecture/
published: true
---
## Elastic Architecture

### Horizontal Scalability is the Scalability That Matters

The key to running a WordPress site that can handle a large amount of traffic consistently, without risking downtime, is an elastic architecture. Simply put, this means the ability to run the website on many machines at once. Your website *must* transcend a single server in order to scale.

With an elastic architecture, when traffic increases, you can provision more machines to run your website. When traffic has calmed down a bit, you can save resources and turn off your extra capacity. Without an elastic architecture, your website is inherently not scalable.

This is also the only way to ensure that your site is **Highly Available** — not at the mercy of a single server’s uptime. This capability is also often called “horizontal scalability”, from the way architecture diagrams have been drawn since the 1990s. Let’s take a look. The most simple representation of an elastic architecture is drawn as a four-square cluster, like so:

<img src="https://raw.githubusercontent.com/pantheon-systems/wordpress-at-scale/master/diagrams/simple_cluster.png" width="1100" title="Simple Cluster Concept" />

This cluster model lets you add additional (n) PHP Application servers (sometimes called “Web Heads”) as well as additional replica databases to increase your website’s capacity to serve pages. That’s fundamental to elasticity. As a drawing, the architecture appears to scale out “horizontally”:

<img src="https://raw.githubusercontent.com/pantheon-systems/wordpress-at-scale/master/diagrams/horizontal_scale.png" width="1100" title="Horizontal Scalability" />

In addition to allowing you to add capacity horizontally, with this style of architecture any of the PHP App servers can go down, and others can take the load. Likewise, if a database fails, a replica can be promoted to the new master. That’s how you get away from any individual machine being a single point of failure. This is **High Availability.**

While there are practical limitations to any architecture — and real-world implementations are usually more complex, as we’ll see — this is the model of how most web applications scale, including WordPress. This architecture is used today to push individual WordPress sites into the hundreds of millions and billions of pageviews.

In the modern era of the cloud, best in class architecture allows you to expand or contract on-demand. This is a key part of being elastic — if it takes weeks (or even days) to bring a new box online that’s better than nothing, but it’s really not where you want to be.

### Challenges

The common challenges running an elastic, horizontally scalable, and highly available architecture are:

* **Load Balancing:** something needs to distribute traffic across the available PHP App servers. Open-source tools like nginx, haproxy, and pound can fill this role, but you can also solve this via hardware (e.g. an F5 appliance) or with a cloud-based load-balancer (e.g. Amazon’s ELBs).
* **Shared Media:** One of WordPress’s most important functions is managing media — images, documents, etc — that go along with posts. These are placed in the `uploads` area of `wp-content`, but in order to make WordPress horizontally scalable, you must find a way for uploads to be available to all PHP App servers. Open-source tools like GlusterFS, NFS, and Ceph are common answers, and Amazon’s EFS is an option in that cloud ecosystem.
* **Consistency:** A classic downfall for clusters is a lack of consistency. If not all the environments at each layer have the same characteristics and configuration, that will compromise elasticity and create maddeningly illusive bugs. Likewise, changes to the application itself — e.g. a WordPress core update — must be deployed consistently, which requires some kind of orchestration and workflow. These are challenges solved by systems administrators and DevOps practitioners, using tools such as Chef, Puppet, Ansible, and Capistrano. There are also cloud tools, such as AWS’s CloudFormation, or OpenStack’s HEAT that can help.

<!--- Do not edit below this line. Automatically pulls in resources. -->

[social_links]

[link-library categorylistoverride="5"]