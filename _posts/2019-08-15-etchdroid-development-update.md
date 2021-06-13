---
layout: post
title: August 2019 EtchDroid Development Update
tags: etchdroid android development
---

As promised in [last post]({{ site.baseurl }}{% link _posts/2019-05-18-etchdroid-development-update.md %}), EtchDroid development has resumed 🎉

<!--more-->

![Git history]({{site.baseurl}}/images/2019-08-15-etchdroid-development-update/gitg.jpg)

The reason why I had to put the development on hold (other than other personal reasons - remember: this is just a hobby project), is that I was basically stuck on a super boring part.

I have a lot of features in mind for EtchDroid, with the main goal of being able to make installers for any recent operating system.

The problem is that, while newer GNU/Linux distros only need you to copy the image bit-by-bit to whatever medium you prefer, things are a lot more complicated for OSes like Windows and macOS.

To summarize, this is what needs to be done to create OS installers for the various OSes:

- Recent GNU/Linux:
	-  `dd if=myfavoritedistro-btw-i-use-arch.iso of=/dev/blockdevice`

- Windows and older GNU/Linux (such as [Damn Small Linux](http://www.damnsmalllinux.org/)):
	- Mount the ISO (UDF filesystem)
	- Format the USB drive (any filesystem supported by both Windows and UEFI ⇒ basically only FAT32; NTFS can be used if you provide a signed UEFI driver)
	- Mount the USB drive
	- Copy files from the ISO to the USB drive
	- Windows only: if the `setup.wim` file is larger than 4GB, it needs to be split with `wimsplit`
	- Install a BIOS bootloader

- macOS (get ready for it):
	- [Mount](https://github.com/darlinghq/darling-dmg) the DMG
	- You'll find the installer application inside; take `$app/Contents/SharedSupport/BaseSystem.dmg` from inside of it and flash it to the USB drive
	- Resize the HFS+ filesystem in the USB drive to the maximum
		- I haven't found any free software tool that's able to resize HFS+, which means... additional steps:
		- Delete it
		- Recreate it but larger
		- Mount `BaseSystem.dmg`
		- Mount the newly created filesystem
		- Copy the content of `BaseSystem.dmg` into it
	- Copy the `SharedSupport` from the main DMG into the USB drive inside the installer app

While I definitely would like to hear from Apple why the fuck did they come up with this, that's not the point. This is how things are right now and we gotta cope with it.

The problem is that these three ways of doing things are completely different. This means that I'd need to implement three separate procedures.

*But are they really so different?*

GNU/Linux images are obviously the simplest, but making Windows installers is actually not that hard.

There are a couple challenges to overcome, such as mounting UDF and FAT filesystems in userspace without assistance from the kernel.

However there is a bigger, more challenging problem: if the app is not modular enough, I could implement anything but it will became a huge pile of spaghetti, with duplicate code coming out from everywhere and a nightmare to maintain.

## Finding a solution
After thinking about it for months, I've come up with a possible structure that should be good enough. But before getting to it, I want to go through the reasoning behind it.

We have a lot of things in common within the three procedures. First of all, they are *procedures*: [*divide et impera*](https://en.wikipedia.org/wiki/Divide_and_rule)

We can divide each problem in smaller steps, which then chained together provide the end result.

Maybe each step can provide info on what work has already been done, so it can be resumed in case of USB disconnection, ran out of battery, app crashed, etc.

## The solution (hopefully)
Currently EtchDroid has a base Android Service that is subclassed multiple times. What it does in a few words is take a USB drive, an image file, open them somehow and copy data from the latter to the former.

For the new back-end, I'm making a single, base service that doesn't actually do I/O. What it does is take a serializable `JobProcedure` that contains all the required `JobAction`s and the data to work on.

Each `JobAction` has a method that provides a `JobWorker` implementation. The services iterates over all the `JobAction`s, obtains their worker and makes it work, then every 5 seconds ask it for a "checkpoint" that is stored in a database in case it's needed later.

In order to get progress notifications, each worker is in turn attached to a `ProgressBroadcastForwarder` class. This class receives progress updates from workers and sends it in a broadcast, allowing it to be displayed in the notification and in a GUI.

Moreover, instead of making use of specific interfaces, each target is adapted to an appropriate common interface.

For example, instead of reading from an `InputStream` and writing to the block device directly, why not make `InputStream` and `OutputStream` wrappers so I can reuse the same code and make it work the other way around (dump an image from a USB device, or decompress a DMG)?

## That's a lot of buzzwords, tl;dr?

Having this structure makes it easy to add new features. If I wanted to add support for a new OS, I only need to:

- update the UI
- add all the required workers to perform each step
- generate a procedure to run them all

That's it for this update, I'll go back to work on it.

If you have any suggestions or questions, please send me an email! The address is in my homepage, [depau.eu](https://depau.eu).

### Bonus: EtchDroid development rig 😂

![EtchDroid setup]({{ site.baseurl  }}/images/2019-08-15-etchdroid-development-update/etchdroid-dev-env.jpg)
