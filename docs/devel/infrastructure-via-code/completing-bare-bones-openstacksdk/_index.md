---
imageFeatured: /assets/images/cover/pexels-sharon-mccutcheon-1148399.jpg
slug: completing-bare-bones-openstacksdk
aliases:
    - /projects/experimental-learning/infrastructure-via-code/completing-bare-bones-openstacksdk/
    - /develop-design/infrastructure-via-code/completing-bare-bones-openstacksdk/
    - /devel/infrastructure-via-code/completing-bare-bones-openstacksdk/
    - /devel/completing-bare-bones-openstacksdk/
title: "ARCHIVED: Completing Bare Bones Openstack SDK"
date: 2021-06-07T11:30:33-04:00
pubishDate: 2021-06-08T15:47:23-04:00
author: Daniel F. Dickinson
series:
    - infrastructure-via-code-openstack
tags:
    - archived
    - devel
    - experimentation
    - infrastructure-via-code
    - jinja
    - learning
    - openstack
    - projects
    - python
    - sysadmin-devops
    - templating
description: "A bare bones OpenStackSDK-based deployment of instances"
layout: list-content
weight: 10500
imageFeaturedAlt: "A stack of various titled books on a light blue table or chair"
---

## Preface

### Some Thoughts

* At this point we should think about what is required to meet our [Target Requirements](../_index.md#requirements-targetted).
* We're going to put off a number of considerations as they depend on robust use of 'userdata' as we will be exploring the use of [Jinja](https://jinja.palletsprojects.com/) to template userdata later in the series.
* At this point we're still concentrating on bringing up instances (and deleting old instances if needed).
* We're also not making a 'Zero Downtime' project, where making changes is expected to result in no visible (even brief) disruption in service; that is overkill for our requirements.

### What We Need for Our Infrastructure (That We Don't Have Yet)

* Use of OpenStack Security Groups
* Handling creation of instances on both public and private networks
* Handling userdata for instances only on a private network (requires use a 'config drive')
* Attaching existing volumes
* Userdata (as mentioned, that's for later in the series)

You might notice that we are not concerned about creating volumes 'automatically'. That is because for our environment volumes are only used for permanent data. We are also not creating 'server farms' for large scale web apps. In addition, volumes come with additional fees (even if not all that large), so we want to keep volume creation manual.

### Code

The scripts described on this page are available in a Git repo @ <https://github.com/danielfdickinson/ivc-in-the-wtg-experiments>.

## Table of Contents

### [Improving the Script](improving-the-script.md)

### [Adding Security Groups](adding-security-groups.md)

### [A Sufficient Complete Bare Bones Script](a-sufficiently-complete-bare-bones-script.md)

## Final Thoughts (To Date)

As you can see the experiments have gone surprisingly smoothly, and we've been able to concentrate in iteratively improving our script. Since this is an experimental process we haven't been using TDD or CI (Test Driven Development or Continuous Integration). Adding those will require some thought as it will need to be able to spin up instances during the test process, and may not be something we want to do on a public cloud offering.

For those who read this, we hope find the process we've shown proves informative, useful, and interesting. Of course we're not done yet, so we hope you will keep watching for update.

----

Credit for cover photo of a stack of various title books on a light blue table or chair: [Sharon McCutcheon](https://www.pexels.com/@mccutcheon?utm_content=attributionCopyText) from [Pexels](https://www.pexels.com/photo/selective-focus-photo-of-pile-of-assorted-title-books-1148399/?utm_content=attributionCopyText)
