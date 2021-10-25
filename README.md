---
title: ReadMe
permalink: /readme
---

# Making local changes
* bundle exec jekyll serve
* http://127.0.0.1:4000/admin

## Add new document to collection
* Add new page using http://127.0.0.1:4000/admin/collections/

## Add a new collection to site
* Add new entry to _config.yml
```
collections:
  software_design:
    output: true
```
Don’t forget to restart your local server after you’ve made changes to _config.yml.

* Add a folder at rool level with _<collection> name (e.g. _software_design)
The folder must be named identically to the collection you defined in your _config.yml file, with the addition of the preceding _ character.	

* Add a navigation page for collection
Add nav.md to collection folder

## Adding new post
* Add new Post using http://127.0.0.1:4000/admin/collections/posts

### Specifying catgory and tags to posts
```
---
title: SOLID Principles
layout: default
category: [Software Design]
tags: [SOLID]
---
```

### Specifying post snippet
* Use excerpt_separator

```
---
title: SOLID Principles
layout: default
category: [Software Design]
tags: [SOLID]
excerpt_separator: <!--more-->
---

# SOLID
SOLID is an acronym for five software design principles promoted by Robert C. Martin (Uncle Bob).
<!--more-->
```
