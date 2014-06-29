# idea.makery.ch Website

This is the website source that is used for the [idea.makery.ch](http://idea.makery.ch). It uses the fantastic [mixture.io](http://mixture.io) as its underlying technology. Mixture greatly simplifies my life!

This readme describes the set up of the mixture project and the relevant settings for this project. For a complete description of what you can do with mixture read the [mixture docs](http://docs.mixture.io/).


## Color

Main Color: #e91e63

See http://www.google.com/design/spec/style/color.html


## General Settings

### Mixture Settings (mixture.json)

* `projectName` and `projectDescription` (is only used for the displayed name in mixture).
* `routes` are necessary for blog paging and blog tags to work. It defines which route takes which template file for rendering. 
* `convertHtml` must be defined for the *Convert to HTML* feature of mixture. 
  * We set `relativePath` to `false` so that paths are kept as they are and not converted to relative paths. We use website-relative paths everywhere in the project and we keep them that way for convertion. Relative paths might also work, except for the 404 page when it is shown from a subdirectory. 
  * The `default` property must be set to `index`. This creates a subfolder for each page containing an `index.html` file. This enables us to use GitHub Pages with *nice* urls like `http://code.makery.ch/blog/my-blog-entry/`. (Otherwise, the url would be `http://code.makery.ch/blog/my-blog-entry.html` or other not so nice alternatives.)

Most other settings in `mixture.json` are left on their defaults.


### GitHub Settings (.githubsettings)

The file `.githubsettings` contains information about the GitHub `username`, `password` (GitHub Token automatically encrypted, encryption is unique to the application and account), `repoUrl`, `branch`, etc.


### CNAME

* For publishing with a custom URL on GitHub pages, the `CNAME` file must contain the domain name.


### Create Icons

* Don't forget to create a favicon.ico file.



## Theme

The `theme` folder contains all sass, css, fonts, and javascript that make up the stylinig of the page.

The `sass` folder contains a the main styling file called `style.scss`. This file imports all other files: the `custom-variable`, `fonts`, and `bootstrap`. The sass files are automatically preprocessed and minified and copied into the `css` folder.

The `css` folder contains some additional css files for the code styling with *prettify*.



## Templates

The `templates` folder contains all liquid templates for individual pages.

* Normal liquid pages: They are based on a layout file and contain custom html content. 
* RSS liquid page: Generates an `rss.xml` file. There is also an RSS file for each tag (e.g. `rss-something1.xml`). The tag-specific rss files are referenced from the filtered blog pages (e.g. page `/blog/tag/something1/`).


### Layouts

Every page inherits a layout file from the `templates/layouts` subdirectory. Those  are the currently used layouts:

* `layout.liquid`: The default layout.
* `post.liquid`: For blog posts. Includes a post header with date and tags and disqus comments at the end.


### Includes

Includes are small templates that are included inside layout files. Some of the includes must likely be customized:

* `header.liquid`: Contains the logo and tagline.
* `navigation.liquid`: Contains the main navigation.
* `footer.liquid`: Contains the footer with feed and email subscriptions, copyright and attribution.



## Models

There is an in-built global mixture model, accessible via the `mixture` namespace.

We're also using a custom global model called `global` inside the `models` folder. This model contains the website title, intro, google anayltics id, domain, email, and more. 

It's important to define all the `tags` that are used. This list of tags is used by the `archive.liquid` template to display all possible tags. 


## Collections

Collections is the place where articles and blog posts are written. Every subdirectory corresponds to a collection. The `blog` collection is reserved for blog posts. All other collections are used for articles.


### Blog Collection

At the beginning of each (markdown) blog post we must define meta information about the post in a YAML format:

```
---
layout: post
title: My Example Post
date: 2014-05-03 00:00
slug: my-example-post
description: "This is the place where we can put a description in one or two sentences."
image: /assets/blog/14-05-03-my-example-post/some-image.png
published: true
comments: false
tags:
- Something1
- Something2
---
```

* `layout`: Defines the layout that is used (see above).
* `title`: The post title.
* `date`: The date of the blog post.
* `slug`: The url that will be used together with the collection name. The example above will result in the following url `/blog/my-example-post/`.
* `description`: (optional) The description is used for the meta description tag on the page (is displayed by search results). It can also be used in other places on the blog as a short summary.
* `image`: (optional) Used as meta information for the Open Graph in the website (is displayed in Facebook, Google+, etc. when the post is shared).
* `published`: Must be set to true for the post to be published.
* `comments`: (optional) If true, the disqus comments are included. The disqus *shortname* is taken from the global model. The disqus *identifier* is the url of the blog post without the domain. The disqus *url* is the url with the domain. If you want to override any of those settings you can add the following sub-properties of `comments` instead of writing true: 
  * `shortname:`
  * `identifier:`
  * `url:`
  * `title:`
* `tags`: (optional) The tags of this blog post.


#### Filename

It's a good practice to use a filename combined with date and slug. The example above would have the filename `14-05-03-my-example-post.md`.


#### Asset Directory

I like to put all assets belonging to a blog post inside one separate folder. The assets for the blog post `14-05-03-my-example-post.md` would thus be under `/assets/blog/14-05-03-my-example-post/`.


## Template License

This template is released under the MIT License (see LICENSE file). If you use the template, I would love to hear about how you're using it and it'd be great if you could include some form of attribution. 