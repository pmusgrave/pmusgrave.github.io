---
layout: single
title: DAC
permalink: /dac
defaults:
  # _pages
  - scope:
      path: ""
      type: pages
    values:
      layout: single
      author_profile: true
---

> Firmware for an audio USB + AK4490 Digital to Analog Converter using PSoC 4 L-Series
>
> May 2018
>
> [https://github.com/pmusgrave/DAC](https://github.com/pmusgrave/DAC)

A lot of my personal projects are motivated by improvements I'm interested in making to my own personal setup. I've been interested in audio for many years and have refined my music listening setup throughout that time. One of the biggest improvements to sound quality you can make in your system comes in the digital to analog conversion stage. The vast majority of DACs on the market are overpriced for what they do, or make dubious claims to convince the audiophile market. And since I'd already built headphone amps in the past and spent entirely too much time researching what headphones to use, I wanted to make my own DAC to get high quality sound for a fraction of the price.

The firmware for this project started out as example code from Cypress Semiconductor, and I modified it to work with the DAC IC I chose. The microcontroller handles USB enumeration and audio transmission, sets the bit rate, and sends I2S clock and data signals to the DAC through DMA. Mainly, I just had to modify the register definitions and initial configuration from whatever codec the example code was using to the AK4490, layout a PCB, and plug it in. I use it every day and it sounds great.

{% include google_analytics.html %}