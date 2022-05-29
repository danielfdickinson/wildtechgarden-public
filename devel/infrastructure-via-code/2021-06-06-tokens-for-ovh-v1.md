---
imageFeatured: /assets/images/cover/money-circle-font-currency-coin-badge-353743-pxhere.com.jpg
slug: tokens-for-ovh-v1
aliases:
    - /projects/experimental-learning/infrastructure-via-code/tokens-for-ovh-v1/
    - /develop-design/infrastructure-via-code/tokens-for-ovh-v1/
    - /devel/tokens-for-ovh-v1/
title: "ARCHIVED: Tokens for OVH v1"
date: 2021-06-06T13:50:39-04:00
publishDate: 2021-06-06T17:14:46-04:00
author: Daniel F. Dickinson
tags:
    - archived
    - devel
    - experimentation
    - infrastructure-via-code
    - learning
    - projects
    - python
    - sysadmin-devops
    - templating
description: "Generating OVH API tokens for use with Terraform and other applications."
toc: true
weight: 10100
imageFeaturedAlt: "Alan Levine: These tokens were from where my parents hung out, Gwynn Oak Park in Baltimore, where in their day it had an amusement park. The one on the bottom left is dated February 5, 1950 the day they were married (and they were not married at the amusement park). Ironically, on the flip side, the token reads \"Good Luck\"."
---

## Preface

Before finding the source of the [issues with Terraform on OVH](../../blog/2021-06-05-terraforming-with-ovh-is-not-paradise.md), a possible source of the dysfunction was thought to be with expired tokens. As such a couple of cross-platform token generation scripts using the Python bindings for the OVH API were tried.

The scripts described on this page are available in a Git repo @ <https://github.com/danielfdickinson/ivc-in-the-wtg-experiments>

## OVH API Token Issues?

The first steps were taken following the [OVH Python library README](https://github.com/ovh/python-ovh/blob/master/README.rst), and consisted of scripts to generate a token to access the ``/me`` OVH API entrypoint and listing existing tokens.

### Prerequisites

Of course the first step was to create an 'Application Key' and 'Application Secret', as outlined in that README as well as '[First Steps with OVH API](https://docs.ovh.com/ca/en/api/first-steps-with-ovh-api/)'.

Then it was necessary to create an ``ovh.conf`` file, which was kept in the same directory as the scripts:

``ovh.conf``

```ini
[default]
; general configuration: default endpoint
endpoint=ovh-ca

[ovh-ca]
; configuration specific to 'ovh-ca' endpoint
application_key=XXXXXXXXXXXXXXXX
application_secret=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
; uncomment following line when writing a script application
; with a single consumer key.
;consumer_key=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

```

### Getting a Targetted Consumer Key for the OVH API

The script below was used to get a limited 'consumer key' for the OVH API (it only had access to the /me subtree of the OVH API).

``get-me-consumer-key.py``

```python
# -*- encoding: utf-8 -*-

import ovh

# create a client using configuration
client = ovh.Client()

# Request RO, /me API access
ck = client.new_consumer_key_request()
ck.add_rules(ovh.API_READ_ONLY, "/me/*")
ck.add_rules(ovh.API_READ_ONLY, "/me")

# Request token
validation = ck.request()

print("Please visit %s to authenticate" % validation['validationUrl'])
input("and press Enter to continue...")

# Print nice welcome message
print("Welcome", client.get('/me')['firstname'])
print("Btw, your 'consumerKey' is '%s'" % validation['consumerKey'])
```

### Managing Authorized Credentials

Then the [Python script to list applications authorized to access your account](https://github.com/ovh/python-ovh#list-application-authorized-to-access-your-account) from the [OVH API Python Bindings Github Repo](https://github.com/ovh/python-ovh) was used, after adding the consumer key generated using the ``get-me-consumer-key.py`` script to the ``ovh.conf`` and installing the prerequisite module (``tabulate``) via ``pip``.

It was noticed a large number of expired but still present tokens existed so the following script was created to revoke all authorizations. It worked quite well.

``revoke-ovh-application-credentials.py``

```python
# -*- encoding: utf-8 -*-

import ovh

# create a client
client = ovh.Client()

credentials = client.get('/me/api/credential', status='validated')
for credential_id in credentials:
  client.delete('/me/api/credential/'+str(credential_id))

```

### Generating Credentials for Managing DNS and Reverse DNS

Finally a consumer key was generated to allow managing DNS (domain) and reverse DNS (ip) records.

``get-domain-ip-consumer-key.py``

```python
# -*- encoding: utf-8 -*-

import ovh

# create a client using configuration
client = ovh.Client()

ck = client.new_consumer_key_request()
ck.add_recursive_rules(ovh.API_READ_WRITE, "/domain")
ck.add_recursive_rules(ovh.API_READ_WRITE, "/ip")

# Request token
validation = ck.request()

print("Please visit %s to authenticate" % validation['validationUrl'])
input("and press Enter to continue...")

# Print nice welcome message
print("Btw, your 'consumerKey' is '%s'" % validation['consumerKey'])

```

## That Was Not the Problem

While what was learned from this exercise may be useful in the future, it didn't resolve the issues with Terraform, which had nothing to do with tokens.

----
Credit for cover photo from Alan Levine via [PxHere](https://pxhere.com/en/photo/353743): These tokens were from where my parents hung out, Gwynn Oak Park in Baltimore, where in their day it had an amusement park. The one on the bottom left is dated February 5, 1950 the day they were married (and they were not married at the amusement park). Ironically, on the flip side, the token reads "Good Luck". More on [Gwynn Oak Park](https://en.wikipedia.org/wiki/Gwynn_Oak_Park) [Here is some footage of what it \[Gwynn Oak Park\] looked like](https://www.youtube.com/watch?v=aqIcDm-EKW)
