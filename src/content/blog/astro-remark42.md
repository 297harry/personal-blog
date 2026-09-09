---
title: "How to Host Remark42 on Azure"
description: "A sample post showing the frontmatter fields and the markdown features this site supports."
date: 2026-08-09
tags:
  - Astro
  - Azure
draft: true
id: "post-esi8q"
---


## Introduction
There are multiple ways to host Remark42, a lightweight and efficient comment system. As documented on the [official website↗](https://remark42.com/docs/getting-started/installation/), a small VPS will be enough. Since my Azure credits are going to expire anyway, I chose Azure Cloud to experiment a bit. It turned out that the cost is too high for a personal blog. Actually, I am considering other solutions. For curious readers who like to explore how I host Remark42, this article will show you a detailed path. I'm using Portal here.

## Deploy Azure Container App
0. Create a resource group to manage all the related resources

1. Create a container app. A few fields are highlighted below. 

Field | Value| 
---------|----------|
 Deployment Source | Container Image 
 Image Source | Docker hub or other registries 
 Image Type | Public 
 Registry login server | ghcr.io
 Image and tag | umputun/remark42:latest
 Ingress | true


 Registry server and image are derived from [docker-compose.yal↗](https://github.com/umputun/remark42/blob/master/docker-compose.yml) from installation instruction. Turning on ingress to receive a HTTP endpoint URL.

## Mount Volume
1. Create a Azure files type storage account.
2. Add classic file share. NB.There is a minimum provisioned size for the service.
3. Add SMB volume mount to the *container app environment* using storage account key. Container apps will not be able to use the volume unless it is associated with the environment.
4. Go back to the container app, and add the volume created previously with mount path `/srv/var`.


## Config Environment Variables


## Integrate with Frontend






## Food for Thought
I chose to host Remark42 on Azure Container App. It's dumb to do it. Most of its functionalities are a waste, and I will need another Storage Account to store persistent data. I rendered to a handy url provided by container app. If I host on a VM, it doesn't provide me with a default url but it will be cheaper. 

A lesson that I learnt from it is that the overall design is outweighted over convinient and sweet functionalities. It is important to consider cost-effectiveness of the chosen hosting solution.
2. 


