---
imageFeatured: /assets/images/cover/pexels-sharon-mccutcheon-1148399.jpg
slug: continuing-openstacksdk-with-templating
aliases:
    - /projects/experimental-learning/infrastructure-via-code/continuing-openstacksdk-with-templating/
    - /develop-design/infrastructure-via-code/continuing-openstacksdk-with-templating/
    - /devel/continuing-openstacksdk-with-templating/
title: "ARCHIVED: Continuing OpenStack SDK With Templating"
date: 2021-06-13T19:29:29-04:00
publishDate: 2021-06-15T19:17:10-04:00
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
description: "Adding basic templates to an OpenStackSDK-based SDK deployment"
toc: true
layout: list-content
weight: 10400
imageFeaturedAlt: "A stack of various titled books on a light blue table or chair"
---

## Preface

Adding templating with the ability to add files to the instance and to run scripts during the instance deployment will get us most of the way to a complete solution for our needs, so that's what this page is about.

### Code

The scripts described in this section are available in a Git repo @ <https://github.com/danielfdickinson/ivc-in-the-wtg-experiments>.

## Section Contents

* [Just a Template](just-a-template.md)
* [Adding Basic Write Files Support](adding-basic-write-files-support.md)
* [Adding Templates to Write Files Support](adding-templates-to-write-files-support.md)

## Next Steps

* Add ``runcmd`` and ``bootcmd`` sections to ``userdata-default.yaml.jinja``
* Add the full set of required files for the desired instances
* Combine with ``create-instances.py`` script
* Add public DNS updating (required to meet some dependencies) (OVH API, not OpenStack)
* Test launch the desired instances
* Improve the code & config, test, improve, etc until satisfied  (for now).
* Add a wrap up note for this series.

----

Credit for cover photo of a stack of various title books on a light blue table or chair: [Sharon McCutcheon](https://www.pexels.com/@mccutcheon?utm_content=attributionCopyText) from [Pexels](https://www.pexels.com/photo/selective-focus-photo-of-pile-of-assorted-title-books-1148399/?utm_content=attributionCopyText)
