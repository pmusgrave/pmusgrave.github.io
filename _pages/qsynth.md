---
layout: single
title: QSYNTH
permalink: /qsynth
defaults:
  # _pages
  - scope:
      path: ""
      type: pages
    values:
      layout: single
      author_profile: true
---

> Work in progress
>
> August 2019 - Present
>
> private repository

My second, significantly more ambitious, hardware synthesizer. This synth uses an STM32F4 microcontroller with DSP instructions to implement a [direct digital synthesizer](https://en.wikipedia.org/wiki/Direct_digital_synthesis). An additional ARM microcontroller handles MIDI communication, either over USB or through DIN connectors, as well as front panel control. The sound engine for this synthesizer uses 32-bit 44.1kHz audio, and it has an external AK4490 digital to analog converter IC to significantly improve sound quality. Up to 32 voice polyphony was obtained with this approach. Or more accurately, I suppose it isn't truly polyphonic, but some kind of hybrid since each voice can be articulated independently, but there is a single filter. (I've heard the term [variophonic](https://www.youtube.com/watch?v=xab1w9f5h10) used to describe this approach, but I'm not sure whether the term has caught on yet.) For the filter, I used an SSI2144 four pole low pass filter.

Direct digial synthesis is a pretty fascinating approach, and I was excited to get a digital synthesizer working. I actually experimented with several different implementations of the same design, including a large excursion into FPGA territory, before finally settling on the STM32F4. I'm planning to come back to the FPGA eventually because I think that approach has a lot going for it. Ultimately, I was spending a lot of time trying to get a floating point pipeline to work on the FPGA, because getting sufficient headroom when multiple voices are playing simultaneously with fixed point math is computationally challenging (especially since I'm not a Verilog expert). The STM32F4 however has single cycle multiply-accumulate instructions and a floating point math unit, so I was able to write familiar old C code and get things up and running much more smoothly.

{% include google_analytics.html %}