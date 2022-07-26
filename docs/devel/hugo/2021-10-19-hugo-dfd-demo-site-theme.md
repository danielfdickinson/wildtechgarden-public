---
imageFeatured: /assets/images/cover/screenshot-aqua-theme.png
slug: hugo-dfd-demo-site-theme
aliaes:
    - /develop-design/web-design-web-devel/hugo-dfd-demo-site-theme/
    - /devel/hugo-dfd-demo-site-theme/
title: "ARCHIVED: Hugo DFD demo site theme"
date: 2021-10-19T05:52:30Z
publishDate: 2021-10-19T05:52:30Z
author: Daniel F. Dickinson
tags:
    - devel
    - docs
    - projects
    - web-design
    - web-devel
    - website
description: "Hugo theme module for demo sites for hugo modules"
summary: "Hugo theme module for demo sites for hugo modules"
# This is 'borrowed' from another of my sites, so don't canonicalize it here.
pageCanonical: false
toCanonical: https://github.com/danielfdickinson/hugo-dfd-demo-site-theme
featuredImageAlt: "Screenshot of a basic website theme with aqua colouring"
imageAddWrapper: false
weight: 9990
---

A theme for [Hugo](https://gohugo.io) module demo sites by [Daniel F. Dickinson](https://www.wildtechgarden.ca/).

## Status

ARCHIVED: This repo is unmaintained and may not be suitable for any purpose except historical record.

## GitHub Repository

<https://github.com/danielfdickinson/hugo-dfd-demo-site-theme>

## Features

* exampleSite (for demo deploys and/or documentation)
* Netlify-ready
  * Cache resources folder (exampleSite)
  * HTML Validation
  * Check internal links
  * HTML Minification
* Good default archetype for new Markdown pages (better than default Hugo)
* Likewise for new HTML pages
* Minimal while looking good
* Fast & light
* Responsive
* Hugo module
* TODO: #3 On mobile replace menu bar 'buttons' with a hamburger menu (CSS only; no JS)
* TODO: #4 SEO improvements (like setting canonical URL)
* TODO: #5 microformats (OpenGraph/Twitter Cards/schema/etc)
* TODO: #6 Add dark theme and auto dark/light based on browser preference

## Using the Theme

1. Create a hugo site

   ```bash
   hugo new site hugo-test-dfd-demo-site-theme
   cd hugo-test-dfd-demo-site-theme
   ```

### Using Hugo Modules (preferred)

1. Initialize the Hugo module system: ``hugo mod init github.com/<your_user>/<your_project>`` (assuming you are using github, of course).
2. Import the theme in your ``config.toml``

   ```toml
   [module]
     [[module.imports]]
        path = "github.com/danielfdickinson/hugo-dfd-demo-site-theme"
   ```

3. Change back to the site directory
4. Get the module

   ```bash
   hugo mod get github.com/danielfdickinson/hugo-dfd-demo-site-theme
   hugo mod tidy
   ```

5. To test the result, run the local Hugo server

   ```bash
   hugo server -b http://localhost:1313/
   ```

### Using downloaded copy of the theme (e.g. ZIP from the Git repo)

1. Make a themes directory and switch to it

   ```bash
   mkdir themes
   cd themes
   ```

2. Obtain a copy of the latest development version of the theme e.g. ([a theme Zip file from the Git repo](https://github.com/danielfdickinson/hugo-dfd-demo-site-theme/archive/refs/heads/main.zip))
3. Copy/extract the theme into hugo-dfd-demo-site-theme in the themes directory
4. Change back to the site directory
5. To test the result, run the local Hugo server

   ```bash
   hugo server -t hugo-dfd-demo-site-theme -b http://localhost:1313/
   ```

### Using git submodules (deprecated)

1. Make a themes directory and switch to it.

   ```bash
   mkdir themes
   cd themes
   ```

2. In the themes directory, add hugo-dfd-demo-site-theme as a submodule

   ```bash
   git submodule add -f https://github.com/danielfdickinson/hugo-dfd-demo-site-theme
   ```

3. Change back to the site directory
4. To test the result, run the local Hugo server

   ```bash
   hugo server -t hugo-dfd-demo-site-theme -b http://localhost:1313/
   ```

 Enjoy!

## Site and Page Params

| Param | Default | Description |
|-------|---------|-------------|
| debugTablesInFooter | false | Show Debug Tables in Footer |
| hidePageFooter     | false | Hide entire page footer infobar (currently copyright and powered by) |
| hidePageHeader     | false | Hide enter page header |
| hidePageTaxonomies | false | Hide taxonomies bar that normally appears near bottom of page |
| hideTopBarMenu     | false | Hide main menu in page header |
| hidePoweredBy      | false | Hide 'Powered By …' in page footer infobar |
| hideSitePageNavigation | false | Hide site navigation bar (e.g. Next page) |
| useBaseURL         | false | Add \<base href="…"> element; breaks footnotes and TableOfContents |

## CSS Classes

Under ``assets/css/hugo-dfd-demo-site/``
Custom CSS should go in: ``assets/css/custom/`` directory

### Naming

Two types of classes available:

* Element classes (e.g. details-demo-site)
  * By actual use of element not the HTML element type (e.g. ``details``, ``list``, ``table-cell``) — sometimes an \<li> might be used with ``details`` when
  there is no additional information, but the item is a part of a list of details.
  * May include a hyphen in the element type part
  * Always end in ``-demo-site`` to denote they are 'demo site' classes
* Feature Classes
  * E.g. ``demo-warningold`` which is wrapped around the old browser warning.
  * Always begin with ``demo`` and a hyphen. The second word is a usually single word (no hyphens).

### Feature Classes

| Class                       | Description                                 |
|-----------------------------|---------------------------------------------|
| demo-mainmenu               | Wrapper around the main menu |
| demo-scrollable             | Added to a wrapper around a scrollable region |
| demo-warningold             | Wrapper around old browser warning; visible by default; hidden if necessary browser support is present |

### Element Classes

| Class                       | Description                                 |
|-----------------------------|---------------------------------------------|
| bar-demo-site              | Added to any 'bar' across the page (e.g. a heading bar) |
| code-demo-site             | Added to any element intended to show source code or content (as source) |
| copyright-info-demo-site   | Wrapper around copyright info (e.g. \<div>) |
| current-menu-is-demo-site  | In a menu list, the current page or item |
| details-demo-site          | Added to any element that can contain additional details with a disclosure widget |
| footer-infobar-demo-site   | Wrapper around page footer (infobar) (e.g. \<div>) |
| header-demo-site           | Added to any _page_ header (e.g. \<header>) |
| heading-general-demo-site  | Added to any general heading (e.g. non-\<hX> that is a heading)
| link-wrapper-demo-site     | A wrapper around links (e.g. \<span>) |
| linkbar-demo-site          | Wrapper around a 'bar' of links (e.g. \<div> or \<nav>) |
| list-demo-site             | Added to any list container element (e.g. \<ul>) |
| list-item-demo-site        | Added to any list item that doesn't use a disclosure element (.eg. \<li>) |
| list-item-label-demo-site  | A label for a list item (allows label to be hidden via CSS, for example for the page navigation we use symbols instead of the labels, by default) |
| main-demo-site             | Wrapper around main article (e.g. \<main>) |
| menubar-demo-site          | A menu 'bar' (horizontal on desktop list of items/'buttons' for a menu); TODO: use as hamburger menu on mobile |
| nav-site-page-demo-site    | Wrapper around page-level site navigation (e.g. Next page); typically a \<nav> |
| nav-taxonomies-demo-site   | Wrapper around page-level taxonomies list; typicall a \<nav> |
| none-demo-site             | An empty item in a list that is usually links (e.g. when there is no 'Next page') |
| powered-by-wrapper-demo-site | Wrapper around 'Powered By' info in page footer (.e.g \<div>) |
| pre-demo-site              | Added to any element to be used as preformatted text |
| section-demo-site          | Added to any master wrapper element (e.g. \<section>) |
| section-list-demo-site     | Wrapper around a list in sections (e.g. \<ul> for list of pages in a section) |
| summary-demo-site          | Added to any element which contains the summary for a ``details-demo-site`` element |
| table-demo-site            | Added to any table |
| table-row-demo-site        | Added to any table row |
| table-cell-head-demo-site  | Added to any table heading cell (e.g. \<th>) |
| table-cell-demo-site       | Added to any regular table cell (e.g. \<td>) |
| title-top-level-demo-site  | Added to top level page title (e.g. \<h1>) |

### From Debug Tables

| Class | Purpose | Notes |
|-------|---------|-------|
| section-debug-hugo | Wrapper around debug tables | _From ``hugo-debug-tables``_: Hidden by default; visible if necessary browser support is present; only applicable if you have imported ``hugo-debug-tables`` (not the default) |

### From Chroma (Syntax Highlighting)

| Class | Description |
|-------|-------------|
| .highlight | Wrapper around syntax highlighted code blocks (e.g. a \<div> around \<pre>\<code>) |

See <https://github.com/alecthomas/chroma> for more information and <https://xyproto.github.io/splash/docs/> for a style gallery

For Demo Site we additionally prefix the ``.chroma`` styles with ``.main-demo-site .highlight``.
