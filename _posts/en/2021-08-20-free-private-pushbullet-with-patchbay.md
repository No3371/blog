---
layout: post
title: "Free & Private PushBullet with PatchBay"
tags: foss patchbay qol
published: true
language: en
---

[PatchBay](https://patchbay.pub) is a free and public service that "patch" Http `GET` and `POST` together. For example, you `GET` from `https://patchbay.pub/123` and POST "321" to `https://patchbay.pub/123`, the `GET` side will receive "321".

Sounds boring, eh? But it could be the most clever thing I've seen these years, and it's free for anyone to use without any authentication, which enable a lot of possibilities.

I've made several personal tools based on PatchBay, for example, PushBullet:

{% gist 1f16e99fc1b49cdd4be25adc9aaab025 %}

The powershell script takes 1 parameter: the channel name. Channel Name is the only input to PatchBay that decide where you `GET` from/`POST` to, so as long as no one share the same channel name with you, we can say the channel is yours.

As you may have noticed, the script actually use `https://patchbay.pub/pubsub/`, which is the pubsub mode of PatchBay, this means all PC running this script will receive data POSTed to the pubsub channel, not just 1 PC.

I mainly POST stuff I wanna read later with curl from my joc PC to my home PC, if I really need it, I can also POST from my Android phone, working with PatchBay feels really nice and easy, because you can do Http `GET` and `POST` everywhere as long as you are connected.

The reason why I don't use the actual PushBullet but this is that, I don't want to login on my job PC, I'm the type that feels insecure and cares alot about my privacy. For people like me, things like PatchBat is really awesome, though it's not actually "secure", but its login-less nature is trully useful.

---

EDIT 21/09/22
It seems patchbay.pub is down :sad: