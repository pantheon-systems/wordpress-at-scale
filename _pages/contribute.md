---
ID: 27
post_title: Contribute
layout: page
permalink: >
  http://persch-gh2-wp-microsite.pantheon.io/contribute/
published: true
---
Rules for contributing will go here.

## Editing existing pages

@todo

## Adding pages

Here is an example of text that would go in `/_pages/new-file.md`.

```
  ---
  post_title: New File
  layout: page
  published: true
  ---

  New Text goes here

  ## You can use headings.

  @todo We need a way to add images.

```

The new page will be picked up by the WordPress site once the new file is merged to master. This sync happens through the [WordPress GitHub Sync plugin](https://wordpress.org/plugins/wp-github-sync/). The page will have a numeric ID once WordPress saves it in the datbase. Following this save, the WordPress GitHub Sync plugin will write back to this repository on GitHub to include the numeric ID and permalink as part of the YAML Frontmatter at the top of the .md file.

### Naming the file

The new file on GitHub must have a name that matches the title within the post. WordPress GitHub Sync names files based on title and will delete mismatched files which makes git history harder to track. The enforcement of this matching is currently manual step in the PR process (@todo, make github issue tracking an automated test).

### Properties to include

@todo


## Adding tags

@todo


<a class="long-box" href="https://github.com/pantheon-systems/wpas">Contribute to WordPress at Scale on GitHub</a>  
