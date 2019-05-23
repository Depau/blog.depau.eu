---
layout: post
title: An update on EtchDroid development status
tags: etchdroid android development
---

*tl;dr:* Project is **not** dead.

I wanted to write a little post on the status of [EtchDroid](https://github.com/EtchDroid/EtchDroid), my Android app to flash OS images to USB drives from Android.

As you may see from the git history, I haven't done a lot lately. That's mainly because I've been very busy: I'm still not done with my college degree and I just got a new job.

EtchDroid *will* continue to exist and I *will* find some time to work on it this year; hopefully I'll port it to other platforms too (not iOS).

In fact, I have some improvements I'd like to do:

- Fix the annoying Android 9 bug ([#10](https://github.com/EtchDroid/EtchDroid/issues/10))

  Mainly because it's very annoying, but also because I run Android 9 on *my motherfucking phone*. I can't even use my own app!
- Rewrite internals ([#15](https://github.com/EtchDroid/EtchDroid/issues/15))

  At my [last workplace](https://www.bottega52.it/) I learned **a lot** on how to write better code that is maintainable and portable, which are things that I want in EtchDroid. Part of this is already done in the [`develop`](https://github.com/EtchDroid/EtchDroid/commits/develop) branch.
- Add support for Windows ISOs ([#5](https://github.com/EtchDroid/EtchDroid/issues/5))

  Arch Linux is my daily driver but I do need Windows occasionally. WoeUSB is great but my phone is way lighter than my laptop if I need it for someone else.
- On-the-fly download and flash ([#14](https://github.com/EtchDroid/EtchDroid/issues/14))

  Possibly with a repository of GNU/Linux distros.
- Resumable flashes
- A little redesign

  I have some usability improvents in mind ;)

- macOS installer support ([#6](https://github.com/EtchDroid/EtchDroid/issues/6))

  macOS installer is kinda weird, so don't hold your breath.

No ETAs. I'll probably be able to get something done in the summer, but I won't promise. If you would like to help, [pull requests](https://github.com/EtchDroid/EtchDroid/pulls) are always welcome ;)

Last but not least I would like to thank everyone who contributed.

A bunch of people [contributed translations](https://etchdroid-l10n.depau.eu/projects/etchdroid/app/). We now have:
- Italian (me)
- German ([Jakob Senkl](https://github.com/fyr77))
- French ([Yassine Imounachen](https://github.com/yassineim))
- Turkish ([Can Berberoglu](https://github.com/Exodus1831))
- Spanish ([Carlos Sánchez](https://github.com/c-sanchez))

A big thanks to all the people who sent donations [on PayPal](https://paypal.me/DavideDepau) or became patrons [on Patreon](https://www.patreon.com/depau):
- Robbie
- Murat Deniz
- Taylen
- David
- Praveen
- Kittipat
- Mohamad
- Kurt
- Mihali
- Alex
- Nemanja
- Vasyl
- Moritz

See you on GitHub ;)
