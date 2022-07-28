---
imageFeatured: /assets/images/cover/hard-drive-enclosure.png
slug: backing-up-is-hard-to-do
aliases:
    - /2020/11/29/backing-up-is-hard-to-do/
    - /backing-up-is-hard-to-do/
    - /post/backing-up-is-hard-to-do/
    - /posts/backing-up-is-hard-to-do/
title: Backing Up is Hard to Do
author: Daniel F. Dickinson
date: '2020-11-30T02:17:00+00:00'
publishDate: '2020-11-30T02:17:00+00:00'
summary: "In my opinion, Windows is deceptively clear and smooth, but when once one really
shines a light on it, one finds significant imperfections. Linux may feel a
little less polished, but is more what you see is what you get (or better) —
there are imperfections for a power user / developer like me, but those
idiosyncrasies are minor compared to the more problematic ones found in Windows."
description: "I went all in with Windows/MS365 and discovered why I love Linux. Take, for example, the 'backup story'"
tags:
- data-and-security
- infrastructure
- linux
- opinion
- sysadmin-devops
- windows
- windows-and-linux
cover:
  image: hard-drive-enclosure.png
  alt: "Four bay hard drive enclosure on a wooden desk"
  relative: true
featuredImageAlt: "Photo of a 4-bay 3.5\" hard drive enclosure and power supply on a tan-coloured wooden table"
---

## Going All-In With Windows Showed Me Why I Love Linux

In my opinion, Windows is deceptively clear and smooth, but when once one really
shines a light on it, one finds significant imperfections. Linux may feel a
little less polished, but is more what you see is what you get (or better) —
there are imperfections for a power user / developer like me, but those
idiosyncrasies are minor compared to the more problematic ones found in Windows.

Case in point is Windows ‘File History’, and the story of backing up Windows in
general.

### Learning Why I Prefer Linux; The Hard Way

I discovered these (and other issues) the hard way. I was becoming disenchanted
with the way my systems were setup and had switched my desktop and laptop to
‘normal’ Windows 10 Pro. I made that choice because I had found out that Windows
10 had improved the Windows Subsystem for Linux story, and because, especially
for the laptop it was the easiest way to be compatible with random offsite
situations.

Because that worked reasonably well, but I was needing to add some more
development, virtualisation, and automation capabilities that weren’t working so
well with standalone workstations, and a full Windows Server was not anywhere in
my budget or desire (I’ve never had that kind of required expense or complication
required by even complex Linux setups), and thinking it was time to try out Microsoft
365 and see what all the fuss was about, I decided to go with a Microsoft 365
for Business Premium option. The standard Business option didn’t offer InTune,
and for what I cared about, didn’t offer any great advantage over the retail Office
2016 licenses I already had.

I had also hoped that the included Azure Active Directory (AAD) would solve the
problems of managing Hyper-V instances from one Windows 10 Pro workstation on
another, while remaining secure (and without an excessive amount of work;
remember, I’m coming from the Linux world where this kind of thing is easy and
free) as well as making it easy to use Ansible or Puppet over WinRM for
automating system management and provisioning from one Window 10 Pro workstation
to another. Unfortunately AAD doesn’t solve the WinRM easy secure communications
problem (which is also what the Hyper-V remote management uses). It appears a
local Windows Server is required for that particular need.

That left me with what I had hoped would be another option, and enable hardening
the network / Windows systems somewhat as well as managing integration with my
Android smartphone (for the Office apps and so on). Sadly, my opinion of InTune
quickly became that it was a sprawling, disorganized mess. One could argue that
Linux administration is as well, but a) if I’m paying for a product I want it to
be better than a free option, and b) to me the disorganization generally relates
to programs that were independently designed, but at least one knows what easy
program does, and can reason where to configure particular items. With InTune
option place, while not random, was a matter of guessing which hierarchy to
follow, and there’s not a useful overall search function to find an option.

Of course looking GPO, Local Security Policy, and Settings, Control Panel etc on
Windows it’s pretty clear that Windows has, like Linux, undergone an ad hoc
growth process. However, when I’m paying for something like InTune, which is
supposed to hide that ad hoc messiness and present a unified, coherent interface,
that’s what I expect it to do.

The other problem I ran into is that the the ‘hardening’ often broke
interoperation with anything non-Windows, and even between some Windows elements.
This wasn’t what I was expecting, or paying for, so before my one month free
trial expired, I went back to Linux, and am glad I did. Taking the opportunity
to switch to Ubuntu, and make my over network less complex and more coherent,
really made me glad to be back on with Linux.

### Backups are Vital

I know everyone hears that and ignores it until they’ve been bitten at least
once, so I won’t belabour the reasons backups matter.

#### First a Little on my Backup Philosophy

1. It should occur reliably, without the need of frequent user intervention.
2. It should follow the 3-2-1 principle:
   1. At least three copies of the data (e.g. original and two backups)
   2. At least two different formats (e.g. live on disk and archived backup)
   3. At least one should be offsite (corollary: you should have at least one local backup).
3. Recover needs to ‘just work’.
4. Doesn’t confuse versioning with backup.
5. Only recording delta (changes) is not a backup. The problem deltas is if the first version of the file becomes corrupt, or inaccessible, the entire history of the file (and therefore the file) is lost.
6. Doesn’t confuse cloud (or other) replication/sync with backup.

##### Sync is not backup for the following reasons

1. A change in one location results in change in all locations. This means having multiple synced copies is not better than having only one copy.
2. Further, a cloud initiated change can remove any and all local copies.
   1. A recycle bin concept in the cloud only delays this issue, it does not remove it.
   2. A cloud provider may replicate the data (which for privacy reasons one might aske *where* the replicated data is stored), but replication is essentially an invisible sync. Human or technological errors in one location is replicated to other location, especially if it’s a ‘silent corruption’ type of issue.
   3. A cloud provider may (or may not) have multiple redundant backups in addition to replication, but  ultimately with a cloud sync based solution one loses local control of one’s data, and such it it not a backup, but placing one’s absolute trust in a third party.

#### Backing up Windows is Hard to Do

* For local backups there have been persistent rumours of removal of the
‘File History’ app, although as you can see from
[this story from the “Fall Creators Update”](https://www.windowscentral.com/microsoft-killing-file-history-windows-10-fall-creators-update),
Microsoft has not followed through (yet) on actually removing and keeping it
removed.
* The ‘Back up and Restore (Windows 7)’ application in Control Panel has been
publicly deprecated by Microsoft since Windows 8, and as seen from the title
given to it in the Windows 10 Control Panel, it’s obviously not planned as a
future proof path, and thus isn’t a real option.
* Microsoft has been heavily emphasizing ‘OneDrive’ or ‘OneDrive for Business’
as the officially supported Microsoft backup strategy for end users and even,
at least, up to small enterprises.
* File History has two fatal flaws from the point of view of the philosophy
outlined above:
  1. One has to constantly monitor the ‘Event Log’ to detect backup failures, and
 there are number of conditions under with it does fail that occur for power
 users (e.g. deeply nested directory structures make FH unhappy). It therefore
 is not particularly reliable without frequent user intervention.
  2. When using OneDrive, FileHistory doesn’t backup files that are synced by
 OneDrive. That makes it useless for keeping a local backup of files that are
 also ‘in the cloud’. In addition it conflates sync/replication with backup.
  3 File History also seems to conflate versioning with backups.
* So, there isn’t reliable, built-in backup for Windows.
* That leaves third party solutions, which usually either cost money or are inadequate for power users.

#### Backing up Linux, the Way You Want, is Easy

* The problem of backing up Linux isn’t one of lack of free (both gratis and
libre) options, but rather having (too?) many options.
* If you only want local backup and are using Ubuntu there is a backup app that
is installed by default, that is pretty reasonable, and includes local backups
(e.g. to an mounted external hard drive), a network drive (various protocols
are supported, including windows sharing (SMB) which is commonly used by NAS
devices designed to be used with Windows, and even Google Drive.
* Not all distros have a backup program installed by default, but for most Linux
distros it is easy to install the program of your choice.
* If you want to emphasize deduplication (saving space by combining identical
parts of the backup to reduce redundancy), you can make that choice. (Including
the choice to disagree with me on versioning and to using delta versioning to
save space, at the cost of reduced safety — although you are already ahead of many
with such a system in that you have at least second copy in a different location).
* Some Linux backups system support backing up to places like Google Drive or
OneDrive; others support things like Amazon S3 buckets, or using SSH/SCP/SFTP
to securely send the data to an offsite location, so it’s a matter of researching
which solution / combination of service and backup program suits your needs.

## Conclusion

For those with Linux skills there is absolutely no reason to switch entirely, or
mainly to Windows. There aren’t even all that many circumstances where one
actually require Windows for one’s own purposes, based on my experience. It’s
more likely the issue is the ability to interact with others, either in terms of
sharing things that will help them (i.e. one needs to play with Windows enough
to be able to show others how to achieve useful things on Windows, even if one
would use Linux for achieving goals for oneself, or to be able to learn from
others and translate to the Linux experience) or for sharing and collaborating
with Windows users.

In short, for myself, I will use Linux.
