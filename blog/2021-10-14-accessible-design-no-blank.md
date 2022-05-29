---
imageFeatured: /assets/images/cover/dont-break-the-back-button-dfd.svg
slug: accessible-design-no-blank
aliases:
    - /post/accessible-design-no-blank
    - /posts/accessible-design-no-blank
title: "Accessible Design: No \"_blank\""
author:
date: 2021-10-15T00:39:08Z
publishDate: 2021-10-15T00:39:08Z
tags:
    - accessibility
    - design
    - frontend
    - technology
description: Auto-opening link in a new tab/window breaks the back button and is unnecessary.
summary: Auto-opening link in a new tab/window breaks the back button and is unnecessary (because users have the ability to make that choice for themselves).
imageFeaturedAlt: "A black backwards pointing arrow with a red 'stop' circle over the top"
---

TL;DR: With browsers having built-in "Open link in new tab"[^1] functionality, it doesn't make sense to break a basic web idiom (the back button) on a whim (of web designers who configure links to automatically open in a new tab or window). This site therefore does not open any links in new tabs/windows. If you want that, use "Open link in new tab".

As [Kyle Mackie](https://www.linkedin.com/in/kylemackie) [pointed out](https://www.linkedin.com/posts/kylemackie_accessibility-dontbreakthebackbutton-hopewecanstillbefriends-activity-6851654352583692288-8xih) on [LinkedIn](https://www.linkedin.com):

>I hate to break the news that just because you *like* links to open in new windows, that doesn’t mean it’s a good design idea.
>
>[#accessibility](https://www.linkedin.com/feed/hashtag/?keywords=accessibility) [#dontbreakthebackbutton](https://www.linkedin.com/feed/hashtag/?keywords=dontbreakthebackbutton) [#hopewecanstillbefriends](https://www.linkedin.com/feed/hashtag/?keywords=hopewecanstillbefriends)

That of course sounds like a random opinion (who is [Kyle Mackie](https://www.linkedin.com/in/kylemackie) anyway?), but it did prompt another user ([Andrew Pheonix](https://www.linkedin.com/in/phoenixandrew)) to post a link to [a blog post he wrote ten years ago with a clear explanation why opening links in a new tab is bad design](https://aphoenix.ca/blog/why-external-links-should-not-open-in-new-tabs/).

The crux of the argument is that those for whom it is most convenient (super-savvy users) don't need it[^2], for others opening new tabs invokes a degree of frustration[^3] or is "**the single worst thing** on the internet"[^4]. And the final set of users[^5] don't know what is wrong when the back button is broken, don't know how to handle new tabs, and are quite likely to give up on browsing out of sheer frustration.

Now you might be wondering what it means that the 'back button is broken'. Part of the answer is that when a link opens in a new tab[^6] then pressing the back button[^7] does not take one to the previous page, it does nothing. Especially for neophyte users, or those with limited interfaces (e.g. disabled users) this is a huge disservice. Even for a very savvy user like myself, it is irritating when I get a new tab and I didn't want it. If I want a new tab because I'm interested in following the link later (but not now), I know how to find "Open link in new tab" in a "right-click" menu[^8]. I don't need someone else deciding for me to open the link in a new window.

Conversely, if I'm actually wanting the follow the link and leave the page, there is no reason to keep the old page around. From the web site operators point of view, having me not leave when I actually leave gives them faulty analytics.

One final note: A web link that does not open a new tab might look something like ``<a href="/post">Blog</a>`` while opening in a new table might look like ``<a href="/post" target="_blank">Blog</a>``. Notice the ``target="_blank"`` when opening a new tab and you will understand from whence comes the title of this post.

[^1]:

      * For desktop users with a standard mouse and monitor setup: To open a link in a new tab in a modern browser, right-click on the link and from the menu that pops up select "Open link in a new tab" (or similar option).
      * For mobile users, hold your finger down on the link and wait until a menu pops up, then select "Open link in a tab" (or similar option; varies by browser).
      * For those using voice commands (and possibly screen readers) the methods vary by vendor, so I can't provide specific advice, but the option should be available to you (or you should replace it with one that has the feature, since your browser is probably terribly limited in other ways as well, and better options do exist).

[^2]: Such users already know how to right-click and select "Open link in new tab" if that is what they want, and it is fact mildly irritating when a new tab opens when they would rather the link be in the same tab.

[^3]: Medium-savvy users without navigation challenges

[^4]: Medium-savvy users with disabilities

[^5]: Non-savvy users, who still exist in significant numbers, especially those on the wrong side of various aspects of the 'digital divide'.

[^6]: Or even worse a new window, although most browsers nowadays don't allow that by default

[^7]: Or Esc; the usual keyboard method of using the back button

[^8]: Assuming it's not a browser where I know the appropriate keyboard shortcut
