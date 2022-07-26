---
slug: msmtp-scripts
aliases:
    - /projects/defunct/msmtp-scripts/
    - /deploy-admin/msmtp-scripts/
    - /sysadmin-devops/self-host/msmtp-scripts/
author: Daniel F. Dickinson
date: '2020-09-23T00:21:00+00:00'
publishDate: '2020-09-23T00:21:00+00:00'
title: 'REMOVED: msmtp-scripts'
description: "A POSIX-shell queue for msmtp email relay"
tags:
  - archived
  - projects
  - sysadmin-devops
toc: true
weight: 90000
---

## PROJECT NO LONGER HAS PUBLIC REPOSITORIES

I have given up on the project as msmtp-queue from the msmtp package proper ought to do well enough for what this project was doing. Further, I have concerns about the security and viability of the msmtp-scripts approach, especially for non-root daemons or any email-emitter running in a restricted (e.g. SELinux confined) environment. I now just use Postfix as a simple mail forwarder.

## Installation Instructions

### Ubuntu

**NB**: This will no longer work as I have removed the PPA

{{< highlight sh >}}sudo add-apt-repository ppa:cshoredaniel/msmtp-scripts-current-daily
sudo apt-get update
sudo apt install msmtp-scripts-mta
systemctl enable --now ms-mta-queue-runner.timer
{{< /highlight >}}

optionally:

```sh
sudo apt install ms-mta-smtpd-systemd
```

or:

```sh
sudo apt install ms-mta-smtpd-xinetd
```

### Debian

**NB**: This will no longer work as I have removed the PPA

Add the following to ``/etc/apt/sources.list.d/msmtp-scripts.list``

{{< highlight sh >}}deb <http://ppa.launchpad.net/cshoredaniel/msmtp-scripts-current-daily/ubuntu> xenial main
deb-src <http://ppa.launchpad.net/cshoredaniel/msmtp-scripts-current-daily/ubuntu> xenial main
{{< /highlight >}}

or for stable series builds, add

{{< highlight sh >}}deb <http://ppa.launchpad.net/cshoredaniel/msmtp-scripts-stable/ubuntu> xenial main
deb-src <http://ppa.launchpad.net/cshoredaniel/msmtp-scripts-stable/ubuntu> xenial main
{{< /highlight >}}

Obtain the PPA’s GnuPG keys.

For current-daily: <https://keyserver.ubuntu.com/pks/lookup?fingerprint=on&op=index&search=0x4E24895B5E8671D17D821DD62CFCAB7524EA5361>
Or for stable: <https://keyserver.ubuntu.com/pks/lookup?fingerprint=on&op=index&search=0x4E24895B5E8671D17D821DD62CFCAB7524EA5361>
Assuming you have saved the key as msmtp-scripts.asc, do

{{< highlight sh >}}sudo apt key add msmtp-scripts.asc
sudo apt update
sudo apt install msmtp-scripts-mta
systemctl enable –now ms-mta-queue-runner.timer
{{< /highlight >}}

optionally:

```sh
sudo apt install ms-mta-smtpd-systemd
```

or:

```bash
sudo apt install ms-mta-smtpd-xinetd
```

### CentOS 7

**NB**: This will no longer work as I have removed the COPR

{{< highlight sh >}}yum install yum-plugin-copr
yum copr enable cshoredaniel/msmtp-scripts-ci
yum swap postfix msmtp-scripts-msmtpq-ng-mta
systemctl enable --now ms-mta-queue-runner.timer
{{< /highlight >}}

optionally:

{{< highlight sh >}}yum install msmtp-scripts-ms-mta-smtpd-systemd
{{< /highlight >}}

or:

{{< highlight sh >}}yum install msmtp-scripts-ms-mta-smtpd-xinetd
{{< /highlight >}}

**NB**: For stable series builds use ``yum copr enable cshoredaniel/msmtp-scripts``
instead of ``yum copr enable cshoredaniel/msmtp-scripts-ci``

### Fedora 30 & Rawhide

**NB**: This will no longer work as I have removed the COPR

{{< highlight sh >}}dnf copr enable cshoredaniel/msmtp-scripts-ci
dnf swap postfix msmtp-scripts-msmtpq-ng-mta
systemctl enable --now ms-mta-queue-runner.timer
{{< /highlight >}}

optionally:

{{< highlight sh >}}dnf install msmtp-scripts-ms-mta-smtpd-systemd
{{< /highlight >}}

or:

{{< highlight sh >}}dnf install msmtp-scripts-ms-mta-smtpd-xinetd
{{< /highlight >}}

**NB**: For stables series builds use ``dnf copr enable cshoredaniel/msmtp-scripts``
instead of ``dnf copr enable cshoredaniel/msmtp-scripts-ci``

## Post-Install

You will will need to create a configuration files for msmtp (the
SMTP client that msmtp-scripts uses). For
msmtpq-ng-mta (fedora/enterprise linux) /
msmtp-scripts-mta (debian/ubuntu) the default location where you
need to add the file is ``/etc/msmtprc``

See ``man 1 msmtp`` for what needs to be included in the file.

### Description

#### Overview

These scripts are wrappers around the msmtp SMTP client that add additional
functionality.

The primary purpose is to allow the use of msmtp as replacement for
sendmail with including queueing, and the option to require that email
be confirmed after some delay before sending it out.

Most of the scripts are modified from the msmtpq script originally from
the msmtp project.

#### Use Cases

* Embedded devices where a user does not have a full blown mail server on their local network and we don’t want to lose mail due to lose of connectivity to the internet.
  * Specifically we’re here for the use case when the mail is non- critical so if a major event (i.e. total power loss, resulting in loss of queue in RAM) happens it’s not the end of the world, but you’d still prefer not to lose the mail to a temporary internet issue. In that case other solutions may be overkill or, like ssmtp, you’ll lose mail if the outgoing mail server is unreachable at the time.
    * But: If mail loss is an issue, it would be better to have a way to host a turnkey mail server for local and vpn mail only, on the local network
* Devices where space is at a premium but where mail service is wanted
* As a replacement for system mail queue on ‘standard’ distros
  * Doesn’t have the problem of losing mail that embedded systems with queue in RAM do.
  * It is quite small and avoids having a bulky and complex mail system just to get system messages.
  * The downside is that you have to watch out for permissions issues (e.g. SELinux issues) since the queuing mail happens as the user or process which is generating the mail.

#### Additional Notes

* Was initially created as a quick hack and although progress has
been made on adding somewhat proper CI.
  * Tests are pretty ad-hoc at the moment
* Written in POSIX shell and that is unlikely to change as the
effort required to write in something like C is in far in excess of
the need for the application.

## WARNING: Tests modify your root filesystem

* The tests are designed for throwaway containers such as Travis and
therefore feel free to modify the root filesystem. You shouldn’t
run them on a production system.
