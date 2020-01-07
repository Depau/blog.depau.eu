---
layout: post
title: Why I use Arch, Wayland/SwayWM and why I don't sometimes
tags: archlinux wayland sway linux flame
---

I wrote this post to share my opinions on GNU/Linux distributions, my
setup, how I use it, how I got there and what I think is still wrong.
I hope somebody may find it interesting or useful.

First of all, a very short distro-hopping history:

- 2010: Ubuntu
- 2016: Arch Linux

Very short.

## How I started with GNU/Linux

*(skip this if you're interested in my current setup/opinions)*

### Windows days

I used to use my brother's old desktop back when I was little. I ran
Windows XP, not enough RAM to run Windows Vista though it was already
out at the time.

Eventually some family friend gave me a bunch of old desktops the
company he worked for had replaced, so I upgraded to Windows 7 as soon
as it was released in 2009. I never really used Windows Vista.

I was aware of GNU/Linux: in fact I used to read this magazine on
computery stuffs, one of those that came with DVDs with software to
try. It was mostly Windows-centric, though sometimes it would talk
about Ubuntu and its derivatives.

When it did talk about Ubuntu, it usually also came with an ISO of the
Ubuntu derivative in question in the DVD. So I tried Ubuntu 6.06, then
some later Kubuntu version, probably 8.04.

I was amazed, I really liked it, especially Ubuntu with GNOME 2. Not
really KDE cause **it's bloated AF** and it would lag on that thing.

Then... I eventually switched back to Windows. For a stupidly simple
reason: Internet connection. We did have 7mbit ADSL, but my room was
too far away from the router, in order to connect to the Internet I
would have to move the router closer, make ridicolous USB extension
cables for the Wi-Fi dongle. I even built a cantenna. Then I'd have
to run `apt-get update`, and hope the link would stay up long enough
for it to download the packages.

With Windows it was much easier because I could simply not update it
(security 👌💯) and if I needed stuff from the internet, I could just
use my brother's computer or the library's and use a USB drive to
copy it to my computer

### Ubuntu

In 2010 though, when I started high school, I got a gift: a laptop.
Needless to say it's much easier to move it close to the router.
I initially used it with Windows 7, but after not so long I installed
Ubuntu on it, and eventually stopped using Windows completely within
a few months.

What made me do the full switch is that I realized that on GNU/Linux
I could actually make the computer do whatever I wanted.
I started learning shell scripting and Python — self taught.

While I've never really done any distro-hopping, I did a lot of
desktop hopping.

I started with GNOME 2 on Ubuntu 10.10 *Maverick Meerkat*. Then
Ubuntu switched to Unity. I did like it but it was way too unstable.
So I ran away and switched to KDE 4, which was quite stable at the
time. When Unity got more stable, I switched to it until I stopped
using Ubuntu. I also tried XFCE, i3wm, Enlightenment, LXDE, GNOME
Shell, but I every time I eventually switched back to Unity.

I did try Arch Linux, but building packages from the AUR was painful
with that cheap laptop, using prebuilt packages from PPAs was much
more convenient.

### Arch Linux

I switched to Arch in 2016 when I bought my new laptop (ThinkPad X1
Yoga, 1st gen). Building packages with a faster computer doesn't take
too long, so why not? I started with GNOME as it was the environment
I was most familiar with, and I kept it until last year.

## Why I quit Ubuntu

When I started using Arch, I realized how much Ubuntu was getting in
my way. Ubuntu has a lot of tiny patches and customizations which,
I must say, are definitely not bad. For example:

- Apache and Nginx on Ubuntu/Debian have a very nice default config:
  you just drop in your additions and you're ready to rock
- `update-alternatives` is quite convenient
- I don't think `snap` is bad (I use it on Arch too)

and there are more things I like, I just can't think of all of them
right now.

However:

- I'm a big boy, I don't need nano as the default editor, or regular
  `vi` replaced with `vim`. I'm fully capable of typing `vi`, `vim`,
  `nvim` or `nano` when I need any of those. Also what's the thing
  with `vim.tiny` and all? Why is there a
  [tiny vim](https://packages.ubuntu.com/eoan/vim-tiny)?
- The `venv` module is in Python3's standard library. Can somebody
  tell me why the hell Ubuntu decided it was a good idea to split
  it into its own package? Hey thanks for making me save
  [11KB](https://packages.ubuntu.com/eoan/python3-venv).
- They made a whole infrastructure for
  [generating the MOTD](https://packages.ubuntu.com/eoan/update-motd).
  I once had to replace it on a shared computer and I had to
  reverse-engineer the fucking thing to understand how to remove the
  freaking Kubernetes ads.
- Why is it that when I install a package that provides a systemd
  service it gets enabled automatically? I'm a big boy, I can turn
  on SSH by myself if I need it.

But most importantly:

**WHY IS MAKING A DEBIAN PACKAGE SO HARD?** It's all like *hey I heard
you like macros, I put macros in your macros so you can script while
you script*.

It's a nightmare, there are tons of macros for every existing build
system, I'm yet to find a package that actually runs `cmake` (or
whatever is needed) without involving a macro that does the same
thing plus who knows what else. There's something like 20 different
build tools that build a package in a slightly different manner.
My toilet paper has better instruction than any of those tools,
and no page on their wikis can apparently agree on which one is the
right one to use.

Also good luck finding a MOTU/Debian developer that will maintain
your package, they'll stare at you sitting on top of a pile of paper
on which all the macros are printed (therefore very tall), and tell you
to read the fucking documentation (*well they say "the code is the
documentation", right?*).
Then each one of them will tell you all the extra requirements you must
meet for having them sign your package and upload it into the repos,
which hopefully doesn't involve sucking their dick.

I used to use `checkinstall` whenever I could but I would find myself
running `sudo pip/make install` way more often than I wanted to.

Also apt/dpkg is slow as hell, for whatever reason 🤷‍♂️

Summary:

- Unwanted/unneeded "goodies"
- Gets in your way
- Overly complicated package management system

## Why I use Arch Linux

On Arch, everything is **easier**. Well not easy as in *my grandma
could do it*, maybe **sane** is a better way to describe it.

Everyone probably knows the Arch Wiki is the best fucking thing since
sliced bread; the Gentoo Wiki is the second best thing.

If you have a little bit of knowledge, you can do whatever you want.
If you don't, the Wiki is there, read every single sentence and the
knowledge will permeate your body. **Seriously**. It's concise (unless
I'm the author of the page), not repetitive, clear.

You may say Arch Linux has a reputation of breaking suddenly.
**Does it break? YES.**

How does it break though? Most of the times it's the user's fault,
and it's because they have done a **partial upgrade**. If there's
breaking changes in some library's API/ABI, you will have to also
update all the dependencies (or rebuild the packages that depend
on that library, if you built them locally).

However, any experienced user will spot when this happens, and it's
an easy fix. Also, it's in the Arch Wiki. 

Maybe it will be a headache the first few times, then when it happens
you'll know it's *that* and you'll fix it without even thinking
about it.

I've never ever reinstalled Arch Linux on my laptop. Not even once.
I've been running and updating the same installation since when I
switched to it. I was not very experienced back then. If I could do
it you can too.

Once you're over this, it's just beautiful. If there's a bug,
you can ask upstream about it, no need to see if the bug was caused
by a downstream patch.

**You are in charge of deciding what goes into your system**, no
package is ever pushed down your throat.

Making packages for Arch is often easier than running
`sudo pip install`, `sudo make install`. **The package manager is
on your side, not against you.**

Summary:

- Simple, minimalistic in every aspect
- You are in charge
- Does't treat you like a baby
- Pacman is fast, making packages is easy

## Why Wayland

I've used X.org on my new computer for a few months, then switched
to Wayland (still back when I used GNOME Shell). Yes, there are
a few inconveniences, you can't expect something that's less than
10 years old replace a well established technology that's been there
from the beginning.

However, using X.org with a HiDPI display is simply a nightmare. It's
just not worth it, especially if you plan to use an external display.

## Why Sway (or i3)

Switching to Sway was very painful at first. I made the switch when
I had enough of GNOME eating up RAM and crashing for no apparent
reason.

I started with a friend's configs and scripts, printed a keyboard
shortcut cheatsheet I could look at whenever I couldn't remember one,
took a few days to customize all the configurations and set up a Git
repo to sync them.

It does have many issues: for instance, Xwayland programs are blurred
on HiDPI displays to begin with, so I made sure 99% of my programs
were running in Wayland-native mode. However:

- Java programs don't like Wayland that much (and have issues with
  the way Sway handles windows even on Xwayland), and I use JetBrains
  IDEs
- Up until a few months ago, the only Wayland-native browser I could
  find was Epiphany (GNOME Web), which is quite crappy. (Now Firefox
  kinda works, Chromium also sort of does if you build it with some
  flags enabled)

Other than that, once you get used to it, a tiling window manager is
much more convenient than a regular floating one. If you're used to
have tons of terminal tabs open, you can now stop using the tabs and
have the window manager do it for you. You can have tabs, or tiles,
switch among them, tile them in another orientation, move them
between displays fast.

And it works with the mouse too! That's something that surprised me
at first, I don't know if that's a thing on i3 but on Sway you can
hold your mod key and drag a window around to visually tile it in a
different location. Or drag it with the right mouse button to resize
it. You can also have floating windows which work pretty much like on
other WMs.

I often have five or more terminals open at the same time, and it's
very useful to be able to move them among workspaces, maybe have an
eye on `htop` while on the terminal next to it I'm deploying a
service, then move them around as needed or move one to a workspace
on its own when more focus is desired.

Summary:

- Has issues, but they're manageable (also development is very
  active)
- Increased productivity
- Lightweight

## Why not $DISTRIBUTION?

### Fedora

Pros:
- SELinux
- Making RPM packages is not hard
- Red Hat is investing a lot on bringing stuff like cast, firmware
  upgrades to GNU/Linux; big thumbs up for that

Cons:
- Package manager is slower than fucking APT
- Narrow selection of third party software
- Flatpak (I hate it)
- I can get all the good things on Arch (except for SELinux),
  without the bad things

### CentOS/RHEL

Pros:
- None, I hate every single time I have to touch a system running
  one of these two distros.

Cons:
- Literally no software
- **Not even FUCKING HTOP**
- What about ncdu?
- Bash? Oh okay at least it does have that.
- Linux kernel from 5 years ago
- Systemd from 5 years ago (and Poettering works for Red Hat IIRC)
- No btrfs support (But they have ZFS? Mmh too bad a couple months
  ago we had a customer who found a corrupted volume in production
  after a power failure, which is something I would expect a
  filesystem to be robust against)
- No literally why the hell are there sooo many people who like it??
  You tell me it's all super tested and stable. Well Ubuntu LTS is
  just as stable, but the kernel and Firefox are reasonably up to date
  and htop is available.

### Manjaro

Cons:
- You can install it without actually learning how to install Arch.

## What I don't like about Arch Linux

As you may suspect, I am very satisfied with the way Arch Linux works.

However, there is one thing that I **hate** about Arch, that I think
Ubuntu does better:

The kernel is overwritten when you update it 😩

On Ubuntu you have a kernel metapackage, then a package with a different
name for every kernel version. When there's a new kernel in the repos
the metapackage is updated to depend on the new kernel.

This way, when you update the kernel, you also get to keep the old one
unless you remove it.

This has a few advantages:

- You can rollback if a kernel update is broken
- Kernel modules for the running kernel are still there when you
  update it.

On Arch, there's a single kernel package that is updated in a rolling
fashion. It is updated veeeery often, it's not too uncommon to get a
kernel update every day, sometimes twice a day.

The fact that it overwrites itself means that when you update it you
have to reboot, otherwise you won't be able to load new modules.

*Forget that USB drive you plugged in, you gotta reboot* ***now***!

In fact, in Arch Linux's infrastructure servers they themselves work
around this by manually upgrading the kernel
([source](https://github.com/archlinux/infrastructure#updating-servers)).

On my servers I run pretty much everything in Docker containers, so
I don't really care which distro I'm running, as long as it has htop,
WireGuard, btrfs, ncdu. I use Arch on the machines I interact with
the most often, Ubuntu on the other ones.

## Neofetch

My rice:

![Rice.jpg]({{site.baseurl}}/images/2020-01-06-why-i-use-arch/neofetch.jpg)
