---
layout: posts
title: Crypto System
linktitle: crypto-system
date: 2018-11-13T10:59:49.653Z
tags:
  - WCF
  - 'C#'
  - Information Security
  - File System Watcher
  - Threading
categories:
  - DEVELOPMENT
---
## Intro

Hello this is my first post! I got a project to build the crypto system that will watch one folder and crypt all files that are inside. The system will have array of bytes as input and the output will be written to file. We have the freedom to choose the technology in which we want to develop the system.

## Implementation

My implementation includes **Client**, **Library**, and WCF **Crypto Service**. As for client it includes the following classes. 

![crypto-storage-class](/img/firsss.png)

### Storage class

This class is responsible for the collection of segments received from WCF service. It is an abstract class used to generate singletons for decrypted segments and for crypted segments. This class collects the segments and puts them in dictionary, and afterwards it is checked for collected segments.

**Update: 23/11/2018**

- - -

### File System Watcher

I've used the FSW in my user controls that will propagate any change to the parent holding form. There are two user controls used for crypting and decrypting of files. When files are added to the crypt/decrypt queue the controls are updated with proper messages. Problems with FSW where that event handlers are called before the file is physically copied into the folder. So the system is still copying the contents of the file and my program starts reading it so I had to do `Thread.Sleep(100)` for it to be able to wait for files to get into the watched folder.

**Update: 06/12/2018**

- - -

### Knapsack

I've worked on Knapsack for my crypto system and for now I have string crypting and decrypting working. I am using a general and superincreasing knapsack to generate the public and private key as described in Information Security by Stamp. For parallelization I am using the `Parallel` class from `Threading` namespace. I am using integer array representation for each byte crypted.

![Knapsack crypting and decrypting](/img/knapsack.png)
