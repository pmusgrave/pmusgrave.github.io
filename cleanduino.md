---
layout: default
---

# Cleanduino

> Clean documentation for the Arduino development boards.
>
> 2019-11-22
>
> [https://github.com/pmusgrave/cleanduino](https://github.com/pmusgrave/cleanduino)

I was recently working on a project where I need to quickly test a microcontroller's peripheral. I decided to use an Arduino Uno to test out communication with my target hardware because it's a well-tested and standardized development board that's easy to spin up quickly and I have tons of them on hand. And so naturally, I pulled up the Arduino Uno schematics and pulled up a datasheet for the ATMega329P to figure out what pins I needed and how to configure my peripheral and start testing.

However, I found the Arduino schematics unnecessarily convoluted and difficult to follow. Poorly drawn schematics are bad for a number of reasons. Primarily because they add developement time. Clean schematics are just as important as clean code (and how many books have been written about clean code?).

It's not my intention to insult the Arduino project maintainers, but the fact is that Arduino has become the de facto entry point into the world of electronics, and I think the documentation should be the best of what the industry has to offer. It should be a welcoming introduction to hardware for newcomers and should be clean, easy to read, and easy to dive into.

So I thought I'd use the Arduino schematics to highlight a few documentation best practices. The beauty of open source is that it's possible to do such modifications. I chose to redraw the schematics in KiCad because I don't use Eagle, but I would welcome pull requests with other formats. 

### The Problem

Mainly, I think where the Arduino schematics fall short is that they try to fit too much on one schematic page. There is no reason to constrain your schematics to a single page, particularly when doing so forces a more crammed visual layout with lots of crossing wires. 

Additionally, separating portions of your circuit onto multiple schematic pages is a very effective way of modularizing your design. It becomes immensly more clear what a circuit block is doing if it is isolated to its own page. This cuts down on the cognitive load of mentally splitting a schematic into sections, and then trying to understand each section. Multiple pages does that work for you, and cuts down on the time and effort to understand the broad picture of what your circuit is doing at a glance.

### The Solution

KiCad's hierarchical schematic design takes a little getting used to, and a lot of people prefer flat schematics. But I tend to like it because of the reasons I just mentioned. When you first see a circuit, you need to understand it at the highest level of abstraction. Then once you're clear on the top level hierarchy, you can dive into the lower level details.

### References

I've really only scratched the surface on this topic, so here is some more information I found helpful.

[Rules and guidelines for drawing good schematics](https://electronics.stackexchange.com/questions/28251/rules-and-guidelines-for-drawing-good-schematics/28255#28255)

[Guide to Drawing Clean Schematics with Virtuoso](https://www.egr.msu.edu/classes/ece410/mason/files/guide-schematictips.pdf)

[EEVBlog's Creating a Nice Readable Schematic](https://www.youtube.com/watch?v=R_Ud-FxUw0g)
