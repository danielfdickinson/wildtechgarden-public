---
imageFeatured: /assets/images/cover/bird-4905732.jpg
slug: alpine-vultr-oh-my
title: "Alpine Vultr—Oh my!"
date: 2022-07-10T06:36:05Z
publishDate: 2022-07-10T06:36:05Z
author: Daniel F. Dickinson
tags:
    - content
    - devel
    - open-source
    - self-host
    - site-news
description: "This site now lives on an Alpine instance via Vultr.com public cloud. No more Azure Blobs (Microsoft) for me!"
imageFeaturedAlt: "Vulture soaring above mountains"
summary: "This site now lives on an [Alpine](https://alpinelinux.org) instance via [Vultr.com](https://www.vultr.com) public cloud. No more Azure Storage Blob web hosting (Microsoft) for me! And though it wasn't a financial decision, I save money!"
---

## Preface

In [a post in April where I talk about being 'up to tech'](2022-04-19-i-have-been-up-to-tech.md), even before [making much of this site's source content source code public](2022-05-29-its-raining-content.md), I mentioned that I was making changes to me systems, and had planned changes to my systems. Well, this site now lives on an [Alpine](https://alpinelinux.org) instance via [Vultr.com](https://www.vultr.com) public cloud. No more Azure Storage Blob web hosting (Microsoft) for me! And though it wasn't a financial decision, I save money!

Aside from having decided to switch my workstations back to Linux as the primary operating system instead of [a more Windows-centric approach](../deploy-admin/a-more-windows-centric-approach/_index.md), I have decided to ditch Microsoft 365 as well as the use of Microsoft's Azure (public cloud).

## Why I quit Microsoft (365 Personal and Business, and Azure)

1. Even though [I did not sell my soul in my decision to use Windows and Microsoft 365](2021-07-03-no-i-have-not-sold-my-soul-v2.md), I was never totally comfortable with
that decision because of what I view as Microsoft's history of treating small customers (consumers, and SOHO/KOHO—Small office, home office, and kitchen office, home office to use a Covid inspired acronym) as sources of revenue (and now data), and nothing more.
2. After getting a notification that gave the 'option' of having personalized (i.e. data-collected and getting targeted based on that) and or non-personalized ads when Microsoft starts showing ads in their consumer desktop applications (you read that right, for consumers they intend to have apps like Word show ads in the desktop—not free web app—version), I was unhappy.
3. In the Business version of Microsoft 365, they have made it very difficult to migrate your email away from Outlook to another provider. I _despise_ vendor lock-in.
4. One of my major reasons for switching to Microsoft 365 was the feeling that I had to do so for compatibility with other people, especially organizations.
   1. This may once have been true, is not very much the case any longer.
   2. If nothing else, the rise of Google Suite (and the popularity of Mac books) forces most organization to be more cross-platform compatible.
   3. Organization also need to be able to deal with folks whose main interface is a mobile device.
   4. When using Microsoft for email it is actually significantly more challenging to communicate on certain open source technical mailing lists, especially systems level ones like the Linux kernel mailing lists, most Linux distribution development mailing lists, and most embedded Linux development mailing lists (and embedded Linux is still huge).
   5. I object to having choose software I don't like as much because someone else is okay with vendor lock-in, so I've decided, "Je refuse!"
5. The main advantage, for me, for the Microsoft desktop apps like PowerPoint is the included transitions and stock images. I've pretty quickly run into the limitations of what doesn't incur extra costs, however, so that turns out to be less of a selling feature than I expected, and nowadays there are many sources of stock images, including commercial vendors with reasonable rates.
6. I actually prefer a lot of the open source apps I use to the Microsoft (or other commercial vendor) alternatives.
7. While not directly Microsoft 365, Microsoft has been 'monkeying' with [GitHub](https://github.com) in ways that I think make it less productive and more 'social-media'-esque, and I am getting increasingly nervous about Microsoft trying to lock users into GitHub (did I mention my dislike of vendor lock-in?)
8. I'm sick of Microsoft's increasing level of data collection; IMO they are getting more data hungry than Google without the great tech.
9. Aside from hardware support[^1], my experience is that Linux has fewer bugs and definitely is many less annoyances.
10. The basic Microsoft CDN (which is only way to have SEO-friendly domain redirects when using Azure Storage Blog Web Hosting) has a few limitations that I can easily overcome with a basic web server instance on my own VPS, and I really don't need a CDN for the size/kind of site I have.

## And I save

Even though it wasn't about the money, my current combination of domain and email hosting with [Teksavvy Solutions for Business](https://business.teksavvy.com), and doing my own web and other hosting on [Vultr](https://vultr.com), and using open source software for my office suites and other apps, is less than half what it cost to use Microsoft products.

## Conclusion

In my opinion Microsoft would have to have major increases in quality (not features I don't want), ditch data collection and skip the ads, and really 'up their game' for me to go back. I somehow don't foresee such an eventuality.

--------

Credit for cover photo of a vulture soaring over mountains to [Manuel Dario Fuentes Hernández](https://pixabay.com/users/drfuenteshernandez-7757554/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=4905732) via [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=4905732).

[^1]: Which has more to do with hardware companies only making drivers for Windows and refusing to provide information that would enable developers to create drivers for Linux, than any inherent fault in Linux.
