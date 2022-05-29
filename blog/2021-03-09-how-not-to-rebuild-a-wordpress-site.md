---
imageFeatured: /assets/images/cover/Rebuilding_of_Tuwima_Street_06,_Łódź_July_2013.jpg
slug: how-not-to-rebuild-a-wordpress-site
aliases:
    - /2021/03/09/how-not-to-rebuild-a-wordpress-site/
    - /how-not-to-rebuild-a-wordpress-site/
    - /post/how-not-to-rebuild-a-wordpress-site/
    - /posts/how-not-to-rebuild-a-wordpress-site/
author: Daniel F. Dickinson
date: '2021-03-09T06:58:40+00:00'
publishDate: '2021-03-09T06:56:06+00:00'
tags:
- frontend
- sysadmin-devops
title: How Not to Rebuild a WordPress Site
summary: "I exported the site and then removed it, and created a new 'wildtechgarden.ca' instance with my hosting company, unfortunately…"
description: "I exported the site and then removed it, and created a new 'wildtechgarden.ca' instance with my hosting company, unfortunately…"
featuredImageAlt: "Photo of a street formed with stone blocks during reconstruction"
---

I rebuilt [Wild Tech "Garden"](https://www.wildtechgarden.ca/) because I was having problems with the 'Redirection' plugin, but the author, John Godley, insisted the problem couldn't be the plugin (it may or may not have been the plugin per se, but given the configuration used by my hosting company the plugin didn't work as it was expected to for 'Site Aliases' when I switched the primary domain from wildtechgarden.com to wildtechgarden.ca with wildtechgarden.com needing to be redirected to wildtechgarden.ca). I therefore tried other methods to fix the issue[^1]. I used a plugin to replace all internal database references (GUID) to 'wildtechgarden.ca' from 'wildtechgarden.com'. Because that is not a recommended procedure, I then exported the site, and then removed the site and created a new 'wildtechgarden.ca' host with my hosting company.

After that I reinstalled the plugins and imported the exported file. That's where I discovered the first issue: the media library was not importable through this process (to be fair to WordPress there was a warning alluding to this, although I didn't realize quite what was meant by the notice). Fortunately I had copies of all the original media files and could add them back. The problem this created was that the paths the media changed as a result, but I did not initially realize this and ended up with a number of 'alt texts' instead of images on various pages and posts. The formatting of many of those posts and pages is still not ideal, but that's really a separate issue with how I organized the blocks when I was first learning WordPress, not all that long ago.

I've had a more successful exports and imports when splitting two of my sites into a total of four sites. In that case the import has an option to import the media from the other site. What I am still not clear on is how (or if) I can export, remove a site, and recreate the site by importing the data, but not any of the PHP files, including plugins (i.e. reinstalling plugins, and using the import data as if I was entering the posts for the first time (but with the original publication dates), and including the media.

That would be, in my mind, the preferred way to deal with a possibly compromised site, because one is doing a pure data import instead the current 'site recovery' which involves restoring backed up copies of all files and the database; which if you restore after the site was (possibly) compromised you haven't eliminated the compromise. It wasn't why I was doing it at the time, but I think the inability to do that, along with some other complications, is making me rethink my use of WordPress vs a static site generator and forms submission service.

So far the upshot of this is to not expect a simple Export/Import process with WordPress, especially when it comes to the Media Library, if one wants to rebuild a site at the same domain, rather than a domain move, with the previous domain still active.

[^1]:
    This failed to get 'Redirection' 'Site Alias' to work correctly, so 'Redirection' at least in combination with my hosting service's configuration was the actual problem, not the switch of domain name (which I have confirmed with another site).

    As I have decided to go for 'plugin minimization' which is considered a WordPress best practice, I have stopped using 'Redirection' (which I was able to get to do what I wanted, just not the through the method that the 'help' messages insist is the way to do it, which is the 'Site Alias' mechanism) and simply use a server configuration file.

----

Credits for cover photo: [Zorro2212](https://commons.wikimedia.org/wiki/User:Zorro2212), [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/), [via Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Rebuilding_of_Tuwima_Street_06,_%C5%81%C3%B3d%C5%BA_July_2013.jpg)
