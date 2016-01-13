---
ID: 22
post_title: Development and Workflow
layout: page
published: true
---

# Scalable and Agile Workflow

## Measure Twice. Cut Once. Revert as Needed.

One of the big challenges with WordPress at Scale is the developer experience. The best production infrastructure in the world doesn’t matter much if the website doesn’t have the right design and functionality, or if you are constantly suffering from downtime because of deployments, or if shipping hits bottlenecks that can hold things up for weeks on end.

Agile development workflows are a whole discipline, and this page is by no means comprehensive. However, everybody knows the era of Cowboy Coding is coming to a close, and there are two industry standard best-practices that are increasingly common with professional WordPress teams.

Anyone interested in developing for Scale should strongly consider adopting both **Pull Requests** and **Continuous Integration.** To achieve these, you need to have every change to the website codebase tracked in version control, preferably Git, widely considered the industry standard. You’ll also need workflow documentation, and ideally some automation, to follow the processes correctly.

**Pull Requests** were popularized by GitHub — but are also an important part of Git Flow — and they mean having developers collaborate on a branch in version control, allowing them to work without stepping on other people’s toes. When code in a branch is deemed ready to go, a pull request is created, which allows for a line-by-line review.

(diagram goes here)

In a perfect world, developers can also stand up a running website for the branch under development. This allows normal acceptance testing or QA on a running copy of what’s proposed in the pull request, creating a much more transparent process which is friendly for project managers and site owners. The pull request can also be integrated with a continuous integration service, such as Travis CI, to run automated tests on the codebase to ensure its quality before it is allowed to be merged and deployed.

**Continuous Integration** minimizes the amount of divergence between branches and production, as well as a structured flow for final QA before a deploy to production. This means having feature branch teams pull from the main version control branch (usually “master”) as soon as possible, as well as being able to frequently clone content back from the Live environment to their development or testing spaces.

(another diagram)

In the Continuous Integration workflow, code changes tracked in version control are deployed “out” from left to right, through Test to the Live environment. The content of the site (database, uploads, etc) are cloned “back” from right to left. It’s the bulletproof way to deploy to a running website.

There should be standard processes (or better yet scripts) that describe how a developer freshens their workspace, and how a test environment is prepared. Developers need to be able to do their work against a recent “snapshot of reality”, and you definitely want to test against an up-to-date copy of production data before you deploy.

Finally, every release should be tagged so you have a record of changes to production. Deploying off tags is essential in a scalable environment: you need to know that a deploy is the same across all PHP Application environments.

## Environmental Consistency

Because of the cost — both for servers, but also in maintenance complexity — of running a horizontally scalable cluster, it’s still common for the “production” instance to be unique. That creates unfortunate tradeoffs.

If you only have one production instance, that means that development, acceptance testing, and any load or performance tests are being done on a different architecture, be that a developer’s laptop or a separate “staging” server. Inevitably that leads to bugs that manifest only in production, unexpected performance regressions, and protestations that “it worked on my machine.”

The way to deal with this is to have as much consistency as is reasonable. Tools like Vagrant — the VVV project — and the emerging model of containers can help to minimize these gaps when it comes to local development environments. When it comes to online development or staging environments, try to minimize the compromises you make. Ultimately, perfect consistency may not be feasible, but understanding where there are differences, and what impacts are expected, can help you to mitigate consistency risks.

**Challenges**

*   **Site Configuration:** the configuration of WordPress sites is in a tricky in-between state. Frequently you’d like to deploy config changes along with code, but most configuration is stored in the wp_options table in the database. The best answer is to utilize the WP-CFM plugin, which allows you to export configuration to JSON, and track it in version control along with code. Still, this can be a challenge.
*   **Local Development:** while the quality of virtualization tools is progressing, they are still complex and require their own upkeep; losing a day of productivity due to local dev problems is always a pain. In addition, it’s very difficult to represent a scalable multi-server environment on a developer’s laptop, so some compromises here are inevitable.

*   **Setup Cost:** for many teams without an existing platform or scripts, setting up a best practice workflow is a costly investment of time, which may or may not be supported by the project budget. Unfortunately many projects suffer because the proper tooling isn’t put into place, resulting in stressful deployment windows.

[do_widget_area]

[link-library settings="1" categorylistoverride="13"]