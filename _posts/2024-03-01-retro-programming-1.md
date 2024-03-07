---
layout: post
title:  "Programming Like It's 1993"
date:   2024-03-01 12:44:36 -0300
categories: macintosh c retro programming
---
### Macintosh II, Mac OS 7.5.5, and THINK C 6.0

![Mac II](/assets/img/dither_it_mac2.jpg "Mac II")

## Before You Begin...

I went to college from 1991 to 1996. What did computers look like in 1994? A mid-range PC typically had a clock-doubled 486DX2-66, 8 MB of RAM, and a 320 MB hard disk. We're going to explore an equivalent Apple Macintosh machine from that era. I never owned a Macintosh during my college years but my sister did, how lucky she was. The Apple Macintosh II series was released in 1987 and had a healthy run until 1993. The Mac OS 7 operating system debuted in 1991, and the version we use (7.5.5) in our system was released in 1994. Symantec's amazing THINK C version 6 was released in 1993. So, let's go back in time and revisit the good old days!

I shamelessly plagiarized the colorful metaphors used in John Earnest's article from [Beyond Loom](https://beyondloom.com/blog/thinkc.html) and adapted the instructions to the slightly more modern system above.

## Your First THINK C Program

![THINK C](/assets/img/thinkc.gif "THINK C")

Welcome, child! Come in, come in! I have so few visitors to this little hut. Pull up a chair, and I’ll put on some tea.

I can see from the wedge of machined aluminum you cradle, its outer surface festooned with glyphs and incantations, that you, too, are a *programmer*. Things have changed so much over the years. What’s that? Oh, you noticed one of my antiques:

An elegant machine from a more enlightened age. A 32-bit processor built by… well, I suppose the details don’t matter. Impossibly slow and cramped compared your starkly modernist folio. Ah, but I see in you a spark of curiosity! Perhaps, perhaps…

I’m afraid my device is too fragile for the roughousing of a novice- it has spent so many years feeling only my touch. Recall, however, the proofs of our saint Turing. We could teach your new machine some old tricks!

## The Host Machine

Install Debian 12 (netinst).

Install admin tools.
```
apt install zip unzip curl sudo htop 
```

Install sound drivers.
```
apt install alsa-utils pulseaudio
alsactl kill quit
alsactl init
pulseaudio --kill
pulseaudio --start
aplay /usr/share/sounds/alsa/noise.wav
alsamixer
```

Install dev tools.
```
apt install git make gcc emacs fpc
apt install xorg libx11-dev
```

Install toys.
```
apt install fortune cowsay lolcat toilet figlet neofetch
```

## Soul and Simulacrum

Let us begin by weaving a lucid dream; the bones and sinews of my antique. Teach your contraption the language of the Motorola 68000. The timings of raster beams and serial protocols. As is so often the case, another of our order has already made most of the necessary alignments and gestures- we need only tap into that lifestream.

First, a ward of salt, inscribed with the true name of our subject. This name still has power in today’s world, does it not? Take care, child, not to break the perimeter:
```
$ mkdir Macintosh
$ cd Macintosh
```
Next, retrieve the means of our communion:
```
$ wget https://www.gryphel.com/d/minivmac/minivmac-36.04/minivmac-36.04.src.tgz
$ tar -zxvf minivmac-36.04.src.tgz
$ cd minivmac
```
As suits its manifold nature, this body must be instructed as to the form it should take via a configuration tool which must, itself, be compiled.
```
$ gcc setup/tool.c -o setup_t
```
To use the full resolution of your  machine, use the following configuration:
```
$ ./setup_t -t lx64 -m II -hres 1344 -vres 768 -depth 3 -fullscreen 1 -sound 1 -speed a -em-cpu 2 -iid 1 > setup.sh
```
or for those with bad eyesight like myself, use the following configuration instead:
```
$ ./setup_t -t lx64 -m II -hres 512 -vres 384 -depth 3 -magnify 1 -fullscreen 1 -sound 1 -speed a -em-cpu 2 -iid 1 > setup.sh
```
And now we can finally compile Mini vMac:
```
$ . /setup.sh
$ make
$ mv minivmac ../
$ cd ..
```

## Forge and Hammer

At last, we need a few artifacts which brings with it the spirit of the machine. The read-only memory of another like mine, deftly flensed from aging silicon and transfigured into pure electrical potential:

We must assemble a disk image with an operating system. To begin, we require a living specimen from which we may take cuttings.

The seventh system brought with it multitasking, which will make it more familiar to your sensibilities. An older version, stripped of inessential baubles, will maximize the resources available to your personal aspirations.

You have a machine now. But is it *truly* yours until it has executed a program of your own devising? The native tongue of the Macintosh is Pascal, once a favored tool for instructing the arts of computer science. Alas, as Unix has trampled all opposition, its own systems language has, in nepotistic glee, monopolized the minds of countless students. Ominously taking its name from the speed of light, C has become a mental cage that traps so many…

Oh, I do apologize. These battles were fought long ago. It’s far too late for tears. Sometimes I lose myself.

You know C, of course. Perfectly understandable. It is in the air that surrounds us, now, and you would be innocent to think it has always been so. To begin your exploration of the Macintosh it would be best to start on some familiar ground. Retrieve the installation disks for THINK C 6.0 from the ethereal world of [Macintosh Repository](https://macintoshgarden.org/apps/symantec-think-c-60) while I get the kettle.

```
$ wget https://github.com/ekbann/ekbann.github.io/blob/main/assets/dat/THINKC-DEV.zip
$ unzip THINKC-DEV.zip
```
- `disk1.dsk` is a 100MB clean install of System 7.5.5.
- `disk2.dsk` is a 30MB THINK C 6.0 development system.
- `disk3.dsk` is a 30MB empty disk for your development files.

Now we awaken the sleeping beast!
```
$ ./minivmac
```

It lives!

## Self-Actualization

THINK C uses project files. Create one.

In the spirit of keeping things familiar, at least at first, we will make use of the `ANSI` library, which provides a simulated terminal and implementations of the familiar `printf()`, `scanf()`, and other friends from `stdio`. The built-in text editor can also be used to create a source file and add it to the project. Watch the motions of my hand:

No need to feel ANSI; your tea is ready
No need to feel ANSI; your tea is ready

Then you need only compose a completely ordinary C89 program, with no strange tricks or idioms whatsoever:

No lies, only fibs
No lies, only fibs

Observe that even from within the warm embrace of `ANSI` compatibility the signature of `main` must be `void`, and there is no `argc` or `argv` to be seen. Furthermore, this `printf()` does not tolerate invocation without at least a single argument beyond its format string. The familiar “down-to” operator `-->` behaves just as you expect.

From the *Project* menu, choose *Run*, or begin spooling command-R into your muscle-memory, and watch as your first program blossoms:

Have Macintosh, Will program
Have Macintosh, Will program

A humble beginning, yes. Perhaps it is too early to see just what makes this little world satisfying, but I must confess, all this talking has left me a bit weary. You have what you need to start, and you can borrow a volume from my bookshelf if you’d like to venture further on your own.

It’s cold outside, but the fire here is warm. You’re welcome to stay as long as you like. So nice to have a visitor.
