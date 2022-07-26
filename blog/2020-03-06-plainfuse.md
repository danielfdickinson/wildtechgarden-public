---
imageFeatured: /assets/images/cover/grass-branch-needle-plant-wood-hay-1217380-pxhere.com.jpg
slug: plainfuse
aliases:
    - /project/plainfuse/
    - /projects/web-design/plainfuse/
    - /develop-design/web-design-web-devel/plainfuse/
    - /devel/plainfuse/
author: Daniel F. Dickinson
date: '2020-03-06T11:00:00+00:00'
publishDate: '2020-03-06T11:00:00+00:00'
title: 'REMOVED: Plainfuse'
description: "Was a rewrite of 'Fuse.js' (fuzzy search) in ECMAScript 5 with no external dependencies (even for development)"
tags:
    - archived
    - devel
    - projects
    - web-design
toc: true
imageFeaturedAlt: "A pin in a bed of hay, symbolizing searching for the proverbial needle in a haystack"
---
## REMOVED Project

Plainfuse was a fork of [Fuse.js](https://fusejs.io/) (fuzzy search) by [Kiro Risk](https://github.com/sponsors/krisk) due to concerns I had with difficulties auditing the minified Javascript (which at the time was the only output version available), combined with a desire for ES5 / IE11 support, which was not present at the time.

As such I converted Fuse.js to 'plain' ES5. The source code for plainfuse is no longer available.

## Old README

### Overview

plainfuse is a javascript standalone fuzzy-search, with zero dependencies. It is forked from [Fuse.js](https://github.com/krisk/Fuse) to create a plain javascript build with no babel, webpack or typescript (build-time) dependencies, as well as convert to ES5 as the JS version.

The only build dependency is ‘concat’ and that is for a lack of other
good (and simple) cross-platform options for combining files.

For testing there are more dependencies because we use Jest tests (from
upstream) to verify operation of dist/plainfuse.js.

### Apache-2.0 Modified Notice

This is the notice required by the Apache 2.0 license that this README.md is modified by Daniel F. Dickinson compared to the upstream version. In fact most files have been modified, removed, or are Daniel F. Dickinson’s new work. The ‘LICENSE’ file has been replaced with a copy of <https://www.apache.org/licenses/LICENSE-2.0> which is the original license text, which one is not supposed to modify (one puts the boilerplate in one’s own files, not modifying the LICENSE file).

### Installation

### As a Hugo Module

**NB**: This no longer works as repo has been removed.

```sh
hugo mod get <https://git.wildtechgarden.ca/danielfdickinson/plainfuse.git>
```

### NPM

**REMOVED**: I have removed this project from npm, along with my user account, so this will not work.

plainfuse can be installed using NPM

{{< highlight sh >}}$ npm install plainfuse{{< /highlight >}}

### Examples

#### Searching by ID

{{< highlight Javascript >}}var books = [{
'ISBN': 'A',
'title': "Old Man's War",
'author': 'John Scalzi'
}, {
'ISBN': 'B',
'title': 'The Lock Artist',
'author': 'Steve Hamilton'
}]
var options = {
keys: ['title', 'author'],
id: 'ISBN'
}
var plainfuse = new PlainFuse(books, options)
plainfuse.search('old')
{{< /highlight >}}

#### Weighted search

{{< highlight Javascript >}}var books = [{
title: "Old Man's War fiction",
author: 'John X',
tags: ['war']
}, {
title: 'Right Ho Jeeves',
author: 'P.D. Mans',
tags: ['fiction', 'war']
}]
var options = {
keys: [{
name: 'title',
weight: 0.3
}, {
name: 'author',
weight: 0.7
}]
};
var plainfuse = new PlainFuse(books, options)
plainfuse.search('Man')
{{< /highlight >}}

{{< highlight Javascript >}}[{
"title": "Right Ho Jeeves",
"author": "P.D. Mans",
"tags": ["fiction", "war"]
}, {
"title": "Old Man's War fiction",
"author": "John X",
"tags": ["war"]
}]
{{< /highlight >}}

#### Searching in arrays of strings

{{< highlight Javascript >}}var books = [{
'title': "Old Man's War",
'author': 'John Scalzi',
'tags': ['fiction']
}, {
'title': 'The Lock Artist',
'author': 'Steve',
'tags': ['thriller']
}]
var options = {
keys: ['author', 'tags']
};
var plainfuse = new PlainFuse(books, options)
fuse.search('tion')
{{< /highlight >}}

{{< highlight Javascript >}}[{
"title": "Old Man's War",
"author": "John Scalzi",
"tags": ["fiction"]
}]
{{< /highlight >}}

#### Searching in arrays of objects

{{< highlight Javascript >}}var books = [{
'title': "Old Man's War",
'author': {
'name': 'John Scalzi',
'tags': [{
value: 'American'
}]
}
}, {
'title': 'The Lock Artist',
'author': {
'name': 'Steve Hamilton',
'tags': [{
value: 'English'
}]
}
}]
var options = {
keys: ['author.tags.value'],
};
var plainfuse = new PlainFuse(books, options)
fuse.search('engsh')
{{< /highlight >}}

{{< highlight Javascript >}}[{
"title": "The Lock Artist",
"author": {
"tags": [{
"value": "English"
}]
}
}]
{{< /highlight >}}

----

Credit for cover photo of a pin in a bed of hay, symbolizing searching for the proverbial needle in a haystack from an unknown form user via [PxHere](https://pxhere.com/en/photo/1217380).
