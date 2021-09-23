---
layout: post
title: "Unity: iOS PVRTC Compression Requires Square Textures"
tags: unity pitfall
published: true
language: en
---

Today my collegue noticed that same animation looks different on iOS and Android, after digging around for a short period, we figured that the related atlas has different imported size on Android & iOS.

It seems that by default, Unity select PVRTC compression format for iOS to support older devices (~2013). PVRTC format requires square textures, **if the texture is not square, Unity stretch it without warning you.** For not-so-old (2014~) iOS devices, ATSC is recommened and it supports non-square textures.

[Source](https://docs.unity3d.com/Manual/class-TextureImporterOverride.html):

>iOS and tvOS
>For Apple devices that use the A8 chip (2014) or above, ATSC is the recommended texture compression format for RGB and RGBA textures. This format allows you to choose between texture quality and size on a granular level: all the way from eight bits/pixel (4x4 block size) down to 0.89 bits/pixel (12x12 block size). If support for older devices is needed, or you want additional Crunch compression, then Apple devices support ETC/ETC2 formats starting with A7 chip (2013). For even older devices, PVRTC is the compression format to use. On iOS, Unity’s default texture compression format is PVRTC, for the broadest possible compatibility. ASTC is preferred, but is not supported on A7 devices (the very first Metal-enabled devices) and will be unpacked at runtime.