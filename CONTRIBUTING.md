This repo is linked to the [scalewp.io](https://www.scalewp.io) website. The core website content is managed here to facilitate contributions from the community. 

While we do some amount of discussion in issues, the best contributions start with a concrete suggestion in the form of a pull request.

Pull requests merged to master go directly to the site.

### Editing existing pages

Pull requests can be made on any files within this repository. Please fork the repository and name your branch based on the change you are making.

The WordPress site to which this repository connects uses the [GitHub Flavored Markdown for WordPress](https://github.com/makotokw/wp-gfm) plugin to render text. So the markdown formatting used in this repository by GitHub should match that seen on the WordPress site.

#### Shortcodes

Many of the files within this repository use WordPress shortcodes for related links and share widgets. Leave those sections as-is when making Pull Requests.

#### Images

Images are added within the git repository within the top-level `diagrams` folder rather than from the WordPress user interface. Images can be linked using GitHub's 'raw' submain using urls like https://raw.githubusercontent.com/pantheon-systems/wordpress-at-scale/master/diagrams/simple_cluster.png. For an example, see [the Elastic Architecture page](https://github.com/pantheon-systems/wordpress-at-scale/blob/master/_pages/elastic-architecture.md). 

### Adding pages

Here is an example of text that would go in `/_pages/new-file.md`.

```
---
post_title: New File
layout: page
published: true
---

New Text goes here

## You can use headings.

```

The new page will be picked up by the WordPress site once the new file is merged to master. This sync happens through the [WordPress GitHub Sync plugin](https://wordpress.org/plugins/wp-github-sync/). The page will have a numeric ID once WordPress saves it in the database. Following this save, the WordPress GitHub Sync plugin will write back to this repository on GitHub to include the numeric ID and permalink as part of the YAML Frontmatter at the top of the .md file.

#### Properties to include

When adding a new file include the following properties in the YAML Frontmatter at the top of the .md file.

* `post_title` - The name of the post needs to correspond to the name of the .md file (See the next section on "Naming the file")
* `layout` - This value should simply be `page`.
* `published` - This value should simply be `true`. The [WordPress GitHub Sync plugin](https://wordpress.org/plugins/wp-github-sync/) does allow for the syncing of unpublished content but our configuration does not include such pages.

#### Naming the file

The new file on GitHub must have a name that matches the title within the post. WordPress GitHub Sync names files based on title and will delete mismatched files which makes git history harder to track. [The enforcement of this matching is currently manual step in the PR process](https://github.com/pantheon-systems/wordpress-at-scale/issues/2). The name of the file should be the same as the title with all special characters removed and spaces converted to hyphens.

### Resource links

Currently we are tracking the resource links only in the WordPress database. You'll notice the code for the resources page is just a [collection of shortcodes](https://github.com/pantheon-systems/wordpress-at-scale/blob/master/_pages/resources.md). However, we are very open to including more resources of value. Please [file an issue](https://github.com/pantheon-systems/wordpress-at-scale/issues/new?labels=resource) if you have a resource suggestion.
