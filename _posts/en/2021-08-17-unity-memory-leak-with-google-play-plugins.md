---
layout: post
title: "Unity Memory Leak With GooglePlay Plugins"
tags: unity pitfall
published: true
language: en
---

So it seems if you have Google Play Plugins in your Unity project and you have **Auto Resolution On Build** toggled on in Play Service Resolver (Android), everytime you build, some junk is left in the heap and counted in ManagedHeap.UsedSize.

Unity will try to GC.Collect from time to time and that makes Editor freeze without any of the leak gets collected, FeelsBadMan.

Unity 2018.4.35f1

GooglePlayPlugins 1.5.0