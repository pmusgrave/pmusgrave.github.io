---
layout: single
title: Software Utility Libraries
permalink: /utils
defaults:
  # _pages
  - scope:
      path: ""
      type: pages
    values:
      layout: single
      author_profile: true
---

> Various algorithm, data structure, and helper utilities. Mostly in C, but also a lot of Javascript.
>
> On and off since May 2017
>
> [https://github.com/pmusgrave/utils](https://github.com/pmusgrave/utils)

Ever since I first started programming, I've had this vision of my own personal library of code, exemplifying the best possible code reuse. I think the ideal case is a collection of things I've built on my own, that are as easy to plug together as external libraries. This is nowhere near that ideal, and I've only started working on it recently, but it's something I keep coming back to and adding pieces to gradually as I build them, and I hope that over time it becomes as useful as I envision it to be. Yes, of course one can just use external libraries someone else has written and get a project up and running, but I think there's a tangible benefit to curating your own library.

In its current state, it's mostly a collection of algorithm and data structure implementations. Sorting algorithms, searching algorithms, binary search trees, graphs, an FFT implementation, etc. One thing I've been working on recently that's worth highlighting is the C++ implementations. These are nice because I'm building in unit tests right from the start this time around, and implementing all of the libraries with templates so that they work with any data type. I've also added in the commands to export these as static library files as part of the make build process, which makes it substantially easier to drop these into other projects as I need to because the static library files are automatically generated.