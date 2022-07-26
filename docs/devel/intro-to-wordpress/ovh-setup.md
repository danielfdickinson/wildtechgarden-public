---
slug: ovh-setup
aliases:
    - /docs/archived/intro-to-wordpress/ovh-setup/
    - /develop-design/web-design-web-devel/intro-to-wordpress/ovh-setup/
    - /devel/intro-to-wordpress/ovh-setup/
author: Daniel F. Dickinson
date: '2021-03-03T22:06:01+00:00'
publishDate: '2021-01-29T21:48:06+00:00'
title: OVH Setup
description: "Setting up a WordPress instance on OVH"
series:
    - intro-to-wordpress
tags:
    - archived
    - sysadmin-devops
    - web-design
    - website
    - wordpress
---

1. With OVH, after picking a domain you pick your CMS (in our case WordPress).
2. Pay for the service (one month or one year)
3. After that you will need to need to wait what seems like forever for the order to be processed and your WordPress instance to be created and initialized. It can take an hour or more, or less than 15 minutes, depending on how busy the hosting service is, so be prepared to be patient.
4. And finally, your instance will up with a default configuration.
5. If you’ve chosen the professional plan or higher you are good to start.
   1. With the personal plan I recommend making some tweaks to the default install.
      ![OVH Web Hosting General Information tab showing PHP version](../../assets/images/2021/01/index-11_1-png-1-1024x456.png)
       1. If ‘Global PHP Version’ is <7.4, ‘Modify configuration’.
          ![OVH Web Hosting Modify Settings Dialogue](../../assets/images/2021/01/index-12_2-png-1.png)
       2. Use PHP 7.4 (requires OS 'stable64')
       3. The settings shown theoretically will slow your website down, but unless you are famous you likely won’t notice, and they are more secure.

6. Because the author already has a WordPress instance, and the knowledge is useful, here is how to create an extra WordPress **sub**domain.
   1. From the multisite tab, add a subdomain for hosting
      ![OVH Web Hosting Multisite Tab](../../assets/images/2021/01/index-13_1-png-1.png)
      ![OVH Choosing domain and subdomain for hosting](../../assets/images/2021/01/index-13_2-png-1.png)
   2. Choose a new directory in which to store the new instance
        ![OVH Add a subdomain settings dialogue](../../assets/images/2021/01/index-13_3-png-1.png)
        ![OVH Add a subdomain confirmation](../../assets/images/2021/01/index-14_1-png-1.png)
   3. You'll see there is now an entry for the subdomain in the 'multisite' listing
      * This creates the sub-domain, but we still need to add WordPress.
        ![OVH Multisite with new subdomain added](../../assets/images/2021/01/index-14_2-png-1.png)
   4. You need to know the database password, which means you need to set it to a known password
      ![OVH change database password](../../assets/images/2021/01/index-15_4-png-1-1024x573.png)
   5. Now add the new 1-click module
      ![OVH Add a 1-click module](../../assets/images/2021/01/index-15_1-png-1-1024x222.png)
   6. You'll need to choose advanced mode
      ![OVH select WordPress 1-click module](../../assets/images/2021/01/index-15_2-png-1.png)
   7. Enter your database password
         ![OVH database password dialogue](../../assets/images/2021/01/index-15_3-png-1.png)
   8. Set your WordPress administrator name, password, and the language of the install
      ![WordPress additional information](../../assets/images/2021/01/index-16_2-png-1.png)
   9. Confirm your settings
      ![OVH add a WordPress module dialog confirmation](../../assets/images/2021/01/index-16_1-png-1.png)
   10. You will receive an email once the WordPress instance is ready. In the meantime, I recommend generating your SSL certificate.
      ![OVH generate SSL certificate](../../assets/images/2021/01/index-17_1-png-1-1024x269.png)
   11. Now that you have received the email stating that your instance is ready, you can proceed to the actual WordPress setup.
      ![OVH WordPress installed email](../../assets/images/2021/01/index-17_2-png-1.png)

**ALERT**: Change the admin password, now!
