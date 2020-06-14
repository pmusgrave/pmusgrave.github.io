---
layout: page
title: LED Driver
permalink: /led-driver
---

> RGB LED strip driver
>
> December 2018
>
> [https://github.com/pmusgrave/LED-driver](https://github.com/pmusgrave/LED-driver)

This was a bit of an experiment to get some exposure driving strips of RGB LED lights. I used an ATMega328P microcontroller's PWM outputs drive three low side MOSFET switches, where the duty cycle of the PWM outputs is controlled by a potentiometer. This allows smooth continuous control of Red, Green, and Blue lights independently, which allows the user to set the lights to any color they choose. Fairly straightforward.

I also added a Raspberry Pi server that sends signals through GPIO to allow remote control of the LED color. Using a Raspberry Pi allows significantly more flexible control over the color because anything can act as a modulation source for the RGB values. One could modulate the light based on the time of day and automatically turn them off at night, for instance.

{% include google_analytics.html %}