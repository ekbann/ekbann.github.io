---
layout: post
title:  "Programming Like It's 1993"
date:   2024-03-01 12:44:36 -0300
categories: macintosh c retro programming
---
### Macintosh II, Mac OS 7.5.5, and THINK C 6.0

![THINK C](/assets/img/thinkc.gif "THINK C")

## Before You Begin...

I went to college from 1991 to 1996. What did computers look like in 1994? A mid-range PC typically had a clock-doubled 486DX2-66, 8 MB of RAM, and a 320 MB hard disk. We're going to explore an equivalent Apple Macintosh machine from that era.

## Your First THINK C Program

Welcome, child! Come in, come in! I have so few visitors to this little hut. Pull up a chair, and I’ll put on some tea.

I can see from the wedge of machined aluminum you cradle, its outer surface festooned with glyphs and incantations, that you, too, are a *programmer*. Things have changed so much over the years. What’s that? Oh, you noticed one of my antiques:

An elegant machine from a more enlightened age. A 32-bit processor built by… well, I suppose the details don’t matter. Impossibly slow and cramped compared your starkly modernist folio. Ah, but I see in you a spark of curiosity! Perhaps, perhaps…

I’m afraid my device is too fragile for the roughousing of a novice- it has spent so many years feeling only my touch. Recall, however, the proofs of our saint Turing. We could teach your new machine some old tricks!

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
$ cc setup/tool.c -o setup_t
$ ./setup_t -t mc64 > setup.sh
$ chmod +x setup.sh
$ ./setup.sh
$ make
$ mv minivmac.app/ ../
$ cd ..
```
At last, we need an artifact which brings with it the spirit of the machine. The read-only memory of another like mine, deftly flensed from aging silicon and transfigured into pure electrical potential:
```
$ wget https://sites.google.com/site/minivmacapplicationsv6/disk-images-and-roms/vmac.rom -O vMac.ROM
$ open minivmac.app
```
It lives!

Your nascent servant hungers
Your nascent servant hungers

## Finding Yourself

See how the emulated screen scintillates on your modern LCD, the reserved orderliness of 1-bit gray struggling to escape from meddling subpixels and anti-aliasing. *Soon, old friend*. A plaintive glyph leads us toward our next task. We must assemble a disk image with an operating system. To begin, we require a living specimen from which we may take cuttings.

The seventh system brought with it multitasking, which will make it more familiar to your sensibilities. An older version, stripped of inessential baubles, will maximize the resources available to your personal aspirations.
```
$ wget https://sites.google.com/site/minivmacapplicationsv6/systems-os/System7.zip
$ unzip System7.zip -d System7
```
Feed `System7.DSK` to your homunculus, and see how eagerly it springs into motion:

System folder, in exquisite miniature
System folder, in exquisite miniature

Next, create an empty vessel. 80 megabytes will prove ample:
```
$ dd if=/dev/zero of=devboot.dsk bs=83886080 count=1
```
The Macintosh will shyly accept this offering, and transform its internal structure into something more useful.

Transfiguration
Transfiguration

Copy the donor *System Folder* (the one on *Disk Tools*) into our new boot volume (*DevBoot*, in our examples), by dragging it from its current location to the destination disk’s icon. From the *Special* menu, choose *Shut Down*. There, there, Macintosh. Rest your head. A final command will make the disk we created the default. The time for rest ends. Reawaken!
```
$ mv devboot.dsk disk1.dsk
$ open ./minivmac.app/
```
Four megabytes, with cleverness, is sufficient for many tasks…

Precious Bytes
Precious Bytes

## Forge and Hammer

You have a machine now. But is it *truly* yours until it has executed a program of your own devising? The native tongue of the Macintosh is Pascal, once a favored tool for instructing the arts of computer science. Alas, as Unix has trampled all opposition, its own systems language has, in nepotistic glee, monopolized the minds of countless students. Ominously taking its name from the speed of light, C has become a mental cage that traps so many…

Oh, I do apologize. These battles were fought long ago. It’s far too late for tears. Sometimes I lose myself.

You know C, of course. Perfectly understandable. It is in the air that surrounds us, now, and you would be innocent to think it has always been so. To begin your exploration of the Macintosh it would be best to start on some familiar ground. Retrieve the installation disks for THINK C 5.0 from the *Macintosh Repository* (the `.zip` versions) while I get the kettle.

Of the four disk images, the most important items are the compiler on disk 1 and the self-extracting archive of headers and libraries on disk 2.

Nothing shall be restrained from us, that we shall endeavor to do
Nothing shall be restrained from us, that we shall endeavor to do

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
