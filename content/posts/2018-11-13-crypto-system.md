---
layout: posts
title: Crypto System
linktitle: crypto-system
date: 2018-11-13T10:59:49.653Z
tags:
  - WCF
  - 'C#'
  - Information Security
categories:
  - DEVELOPMENT
---
## Intro

Hello this is my first post! I got a project to build the crypto system that will watch one folder and crypt all files that are inside. The system will have array of bytes as input and the output will be written to file. We have the freedom to choose the technology in which we want to develop the system.

## Implementation

My implementation includes **Client**, **Library**, and **WCF Crypto Service. **As for client it includes the following classes. 

![crypto-storage-class](/img/firsss.png)

### Storage class

This class is responsible for the collection of segments received from WCF service. It is an abstract class used to generate singletons for decrypted segments and for crypted segments. This class collects the segments and puts them in dictionary, and afterwards it is checked for collected segments.
