---
imageFeatured: /assets/images/cover/monitor-1307227.jpg
slug: web-design-after-all
aliases:
    - /2021/03/29/web-design-after-all/
    - /web-design-after-all/
    - /post/web-design-after-all/
    - /posts/web-design-after-all/
author: Daniel F. Dickinson
date: '2021-03-29T11:43:35+00:00'
publishDate: '2021-03-29T11:43:34+00:00'
tags:
- debug
- devel
- frontend
- theme
title: Web Design After All
summary: "I've ended up doing some frontend web design after all, and have also enjoyed working with the Hugo static website generator."
featuredImageAlt: "An illustration of three monitors with codes on them, with a metropolitan skyline at dusk in the background, with a globe covered in binary digits in the background"
---

I've ended up doing some frontend web design after all (this isn't something I was planning on spending time on, but I'm not really happy with WordPress (especially the risk of compromise, the lack of adequate built-in automatic backups, and it not being as privacy oriented as static web sites usually are). I have also enjoyed working with the [Hugo](https://gohugo.io) static website generator in the past, and designing HTML layouts and custom CSS is an interesting challenge.

The result is the screenshot you see above — and that's just the theme I built for doing debugging and testing of issues when working with Hugo, and especially the styling is what I describe as 'a silly little style thrown in for free'. The main point of that particular development effort though, was not the creation of a theme, but of debugging tools.

The result is the theme itself as well as another debug tool that it incorporates (see below), which is designed to make it easy to add in minimal changes to create samples of problems that crop up, in a less complex theme than a full blown one.

[**AUTHOR'S NOTE**: _Edited 2021-10-23 to reflect changes in reality_]

~~`https:\/\/github.com/danielfdickinson/hugoMinimalTestTheme`~~ had the theme (a newer, better, version is in <https://github.com/danielfdickinson/hugo-minimal-test>) and I had also created a demo website for the theme ~~`https:\/\/hugo-minimal-test-theme-demo.wildtechgarden.ca/`~~. ~~The new demo website for the minimal test~~ is less beautified, but I also have ~~\[a new Demo Site Theme]\(`https://hugo-dfd-demo-site-theme.wildtechgarden.ca`)~~ which has the 'silly little style' that made it look more pleasant.

Another interesting tool that was suggested to me, and which I have built into the theme (as well as making it available as a module for others who wish to use it) is a set of [Hugo Debug Tables](https://github.com/danielfdickinson/hugo-debug-tables) which one can view on the [debug tables demo website](https://hugo-test-debug-tables.wildtechgarden.ca). The debug tables provide a comprehensive set of information about the variables that are in play when using the Hugo site generator, on each and every page.

My next step is to build the HTML layouts (without CSS) for a full-featured but hopefully well designed and easy to use. After that I hope to be able experiment with a variety of CSS styles that turn the site into magic.

And finally, convert all my sites to the new themes that are the result of all that effort.

----

Credit for cover photo: [Gerd Altmann](https://pixabay.com/users/geralt-9301/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=1307227) via [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=1307227)
