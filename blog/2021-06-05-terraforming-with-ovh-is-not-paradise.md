---
imageFeatured: /assets/images/cover/pexels-sergio-souza-1781990.jpg
slug: terraforming-with-ovh-is-not-paradise
aliases:
    - /post/terraforming-with-ovh-is-not-paradise/
    - /posts/terraforming-with-ovh-is-not-paradise/
title: "Terraforming OVH Is Not Paradise"
date: 2021-06-05T18:43:06Z
publishDate: 2021-06-05T18:43:06Z
tags: ["linux","sysadmin-devops","system administration","infrastructure"]
summary: "Using Terraform with OVHcloud, I hit issues that affect both OVH API and OpenStack API. There are 'Resource Not Found' issues…"
imageFeaturedAlt: "Picture of an island in a 'bowl' view"
---

I've been experimenting with [Terraform](https://www.terraform.io) to manage a number of Public Cloud Infrastructure instances (virtual machines) on [OVHcloud](https://ca.ovh.com/manager/). Initially it went relatively well. I did have a rough spot where the error messages I was getting failed to let me know that the tokens I was using didn't have enough privileges for the tasks I wanted perform (I was trying to follow the principle of using tokens with the least privileges possible as is considered best practises). That was frustrating, but it's part learning what to expect from a platform.

Despite that little wrinkle I was pretty happy with the way Terraform was managing my OVH instances. That has changed because I hit an issue that affects both OVH API and OpenStack API on OVH. For OpenStack on OVH there are 'Resource Not Found' issues [which seem to be experienced by others as well](https://community.ovh.com/en/t/is-ovh-public-cloud-orchestration-and-openstack-working/5595/3). For the [OVH Terraform provider plugin there are issues with id's being changed](https://github.com/ovh/terraform-provider-ovh/issues/76).

If I was a paying support customer and presumably had access to knowledgeable support I'd probably try working with them to resolve the issues, however at the moment I am in a miniscule budget and don't have access to more than the free support tier, and I find dealing with them _extremely_ frustrating, and for an issue this complex, I not going to try banging my head against that brick wall.

So now I'm experimenting with using the the Python bindings for the OVH API and the OpenStackSDK and writing Python code to manage my instances as code. I took a brief look for alternatives, but none was sufficiently compelling for me to try it versus managing things more directly.

I'm actually wondering if the problem is that Terraform (and potentially other similar offerings) make the mistake of assuming that because the API returns a unique id for a particular resource, that the resource will always have that same unique id, when in fact the id is subject to change. For example, if OVH does some backend work, does that potentially result in an id change in certain OpenStack resources? I'm not clear on whether the OpenStack API promises that an id is permanent for the life cycle of a named resource, or only that it is unique until the resource is modified in some fashion.

If the former, then OVH is breaking an OpenStack API promise; if the latter, Terraform has made a faulty design assumption, and it's doomed to fail on OpenStack.

In any event, from this I have learned that I'm not going to rely on the id remaining the same. In addition, avoiding that assumption allows me to use the Horizon and OVH Control Panel (web interfaces for OpenStack and OVH) without fearing that making changes there will break my management system.

We shall see — if I succeed I will be publishing details in the [Wild Tech "Garden"](https://www.wildtechgarden.ca).

----

Credit for cover photo: [Sergio Souza](https://www.pexels.com/@serjosoza?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) via [Pexels](https://www.pexels.com/photo/photography-of-island-1781990/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)
