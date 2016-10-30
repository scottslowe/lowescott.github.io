---
author: slowe
comments: true
date: 2011-11-12 13:45:47+00:00
layout: post
slug: vsphere-ha-and-vapps
title: vSphere HA and vApps
wordpress_id: 2463
categories: Explanation
tags:
- Virtualization
- VMware
- vSphere
---

This is probably obvious to most everyone, but for those who don't already know it's important to point this out: vSphere HA does **not** honor vApp startup settings. So while you can go into the properties for a vApp and define the order in which VMs will start (or stop) and the timing between those actions, vSphere HA will not recognize or honor those settings. Therefore, in a situation where an ESX/ESXi host fails and that host is running a vApp, the individual VMs in the vApp could be restarted in an entirely different order than what you specified in the vApp settings.

Be sure to plan accordingly when using vApps in your environment.
