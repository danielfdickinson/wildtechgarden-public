---
slug: moving-a-postgresql-server
aliases:
    - /docs/sysadmin-devops/self-host/moving-a-postgresql-server/
    - /sysadmin-devops/self-host/moving-a-postgresql-server/
    - /deploy-admin/moving-a-postgresql-server/
title: "Moving a PostgreSQL Server"
date: 2021-05-19T22:04:42-04:00
publishDate: 2021-05-20T07:32:04-04:00
tags:
- database
- linux
- self-host
- sysadmin-devops
summary: "At some point you may need to upsize your PostgreSQL server, particular if you have implemented one on a old Raspberry Pi."
toc: true
---

## Preface

At some point you may need to upsize your PostgreSQL server, particular if you have implemented one on a old Raspberry Pi. This article discusses moving your server to a new home.

## Create the New Server

Before you can move the old data to a new server, you need a new server.  The [PiSQL](2021-05-11-pisql.md) article is mostly applicable (although you will do your initial base OS configuration different than from a Raspberry Pi setup) if you are using Debian or Ubuntu to host the new server, so use that, or the guide of your choice, to stand up a new PostgreSQL server.

## Transfer the Old Server's Data to the New

### Stop All Services That Use the Old Server

This could involve multiple hosts, but we don't want new data to be written to server as it will be lost.

### Dump the Old Data

On the old server:

1. ``sudo su -``
2. Change to a directory with a large amount of space.
3. ``sudo -u postgres pg_dumpall -c --if-exists >oldpgdata.sql``

### Copy the Old Data to the New Sever

Copy the file ``oldpgdata.sql`` to the new server.

### 'Restore' the Data Into the New Server

```bash
sudo -u postgres psql -f oldpgdata.sql postgres 2>&1 | tee restore.log
```

Check the restore.log for any relevant errors (non-existing databases to drop, 'postgres', and 'template1' already existing are expected).  If there are none, you should be able use the databases.

## Use the New Server

Point your existing services at the new server instead of the old.

## Configure Backups

As usual, configure backups of the databases (see PiSQL guide, for example).

## Decommission Old Server

You should now be able to shut down the older server for good.
