---
slug: halting-infrastructure-via-code-project
aliases:
    - /posts/halting-infrastructure-via-code-project/
title: "Halting Infrastructure via Code Project"
date: 2021-06-25T02:29:12-04:00
publishDate: 2021-06-25T02:29:12-04:00
author: Daniel F. Dickinson
tags:
    - experimentation
    - learning
    - openstack
    - projects
    - python
    - site-news
description: "Why we have halted work on the Infrastructure via Code Learning Project"
summary: "Why we have halted work on the Infrastructure via Code Learning Project"
---

The following summarizes why we have halted work on the [Infrastructure via Code Learning Project](../devel/infrastructure-via-code/_index.md):

While our internal tests (using private data that would need to be replaced with dummy data) of a full config were successful, frustrations with 'our' OpenStack hosting provider (and researching other Canadian OpenStack providers suggests that there aren't others doing a better job, and that my current provider is the one with the greatest chance of 'business continuity') has led to the conclusion that it's not a viable cloud alternative for us.

Therefore we are not continuing with this project.

In addition it is our finding that this approach involves more effort than if Terraform were a viable option, so if we were to continue with public cloud infrastructure we would prefer services with which we can successfully use Terraform.
