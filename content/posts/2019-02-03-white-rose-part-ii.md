---
layout: posts
title: White Rose - Part II
linktitle: pentesting-project-part-ii
date: 2019-02-03T13:44:33.757Z
tags:
  - vue
  - laravel
  - trello
  - ethical hacking
  - vuex
  - vue-router
  - apache
  - mysql
categories:
  - DEVELOPMENT
---
I will outline the basics of registration for pentester. Pentester has to enter some of the skills he posses and that will be shown after he bids on job. After the pentester has filled out the whole wizard form the page will refresh and wait for email to be confirmed. The app will inform the user of status of registration so far with vue-snotify notification.

{{< img-shortcode imgurl="/img/pentester-registration.png" >}}

{{< img-shortcode imgurl="/img/registration-success.png" >}}

## Pentester profile

After the email confirmation the pentester can check out his new profile. I've added few features so the pentester can easily navigate through the dashboard. On the left side is quick menu for info, inbox, profile setup, and profile preview, all so the pentester can get the setup and info quickly. There is also a menu bar in center to get the job information and other setup with ease. User can navigate to some parts of the app by clicking on profile avatar, and selecting desired feature. On the picture depicted below is part of token withdrawal from the app, I will write more about tokens in future.

{{< img-shortcode imgurl="/img/pentester-withdrawal.png" >}}
