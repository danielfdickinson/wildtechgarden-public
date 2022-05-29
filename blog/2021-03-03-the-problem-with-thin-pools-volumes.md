---
imageFeatured: /assets/images/cover/ELCASET-TAPE.jpg
slug: the-problem-with-thin-pools-volumes
aliases:
    - /2021/02/20/the-problem-with-thin-pools-volumes/
    - /the-problem-with-thin-pools-volumes/
    - /post/the-problem-with-thin-pools-volumes/
    - /posts/the-problem-with-thin-pools-volumes/
author: Daniel F. Dickinson
date: '2021-03-03T21:30:39+00:00'
publishDate: '2021-02-21T03:21:24+00:00'
tags:
- linux
- sysadmin-devops
title: "The Problem with Thin (Pools & Volumes)"
summary: "Linux LVM thin pools and volumes initially seem to be a great way maximize the use of hard drive space, but …"
description: "Linux LVM thin pools and volumes initially seem to be a great way maximize the use of hard drive space, but …"
featuredImageAlt: "A magnetic cassette tape"
---

Linux LVM thin pools and volumes initially seem to be a great way maximize the use of hard drive space by using only the space that is actually allocated to files. There is a major fly in the ointment though. Thin pools cannot be reduced in size.

With normal (thick) LVM volumes one creates a volume of certain size, and that space is not available for use by any other volume. With a thin pool you create a wrapper volume (called a pool), for which you set a maximum size, however that space is not 'set aside' but remains available for creating other volumes. When you create a thin volume inside the pool, you again set a maximum size, and again the space is still available for use elsewhere.

Of course once you put actual data in the thin volume (and therefore pool) the space that is actually being used is no longer available for use elsewhere. (And once allocated the space is always allocated, even if zeroed, when using 'spinning' disks). If you have created maximum greater than the actual size of storage, this is known as 'over-provisioning'. This means that if all volumes we used to their maximum you would get an 'out of space' condition before the full size of all the volumes was reached.

With a thick volume, volumes for which one is not using the full size, and if the filesystem one is using supports shrinking, then one can shrink the filesystem, and then reduce the LVM logical volume to the new size. With thin volumes resizing a volume does not necessarily work (one may end up with a warning that the volume maps a larger size than is allocated). In addition even if one shrinks the volumes in a thin pool one cannot shrink the pool itself.

That's rather a problem for flexible space management because it means that one can end up in a situation where the only way to rebalance the space used by the various volumes is to copy all the data from the existing volumes to other storage, remove the offending volume(s) and create volumes that fit your new reality.

Therefore, my recommendation is to not use thin pools and volumes unless has a specific application or use case for which it will work for you.

----

Credit for photo: [Akakage1962](https://ja.wikipedia.org/wiki/%E5%88%A9%E7%94%A8%E8%80%85:Akakage1962), [Creative Commons Attribution 3.0 Unported](https://creativecommons.org/licenses/by/3.0/deed.en), [via Wikimedia Commons](https://commons.wikimedia.org/wiki/File:ELCASET-TAPE.jpg)
