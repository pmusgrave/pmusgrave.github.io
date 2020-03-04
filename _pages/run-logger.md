---
layout: single
title: IoT GPS Run Logger
permalink: /runlogger
defaults:
  # _pages
  - scope:
      path: ""
      type: pages
    values:
      layout: single
      author_profile: true
---

> Low-power device to log distance and time when you run using GPS. Automatically synchronizes run data to the cloud through an MQTT broker when connected to WiFi.
>
> February 2020
>
> [https://github.com/pmusgrave/run-logger](https://github.com/pmusgrave/run-logger)

This is a device that logs your distance and time when you walk or run. This device uses a GPS module to track position, and includes an ESP32 WiFi/BLE microcontroller to synchronize data to the cloud automatically, using an extremely simple and familiar user interface. Just like a classic stopwatch, this has a simple 3-button, start, stop, reset interface.

Yes, I know you can use a smartphone app to log your distance when you run. Smartphones have a few drawbacks in my opinion:
1. They are expensive. I have dropped phones plenty of times and I don't want to risk that amount of wear on my phone when I exercise. Even if you don't drop the phone, exercise obviously produces a lot of sweat, and this moisture causes a lot of additional wear on phones. A lower cost solution gives me peace of mind that I won't be damaging a costly smartphone.
2. They are relatively heavy. It might not seem like much, but when you're running a long distance, any extra weight tends to add up over time.
3. They are relatively large and bulky. Again, it might not seem like much, but I personally dislike having a phone jostle around in my pocket in these situations. The less encumbrance the better.

Additionally, I think this is better than step-counting products like Fitbit because using a GPS module makes this extremely accurate, to within the tolerance of GPS measurements. Fitbit essentially only gives you a rough idea of how far you went. And having an Internet connection built-in means it's very simple to log data and give yourself insights to your fitness progress over time.

For now (and this is subject to change), I'm using a Raspberry Pi as an MQTT broker to handle messages from the device and send them to a Node.js script, which handles communicating with my logging database (postgres). Then I tied this into my [Iot Dashboard](/iot-dashboard).

Regarding distance measurement accuracy, there is a tradeoff in how often to sample the GPS coordinates. GPS has an inherent tolerance to its position measurements of about 10m, which means that each position sample increases the error by 10m in the worst case. Sampling too often means the error distance would be greater than what you've actually moved in that time period, and your overall distance measurement will be very inaccurate. Sampling less often helps with this because you will have moved further in that time period, which means the GPS tolerance is a smaller percentage of distance traveled. However, this isn't perfect, because the device must sample frequently enough to track the running route accurately. For instance, if you run in a loop and the sample rate is such that it samples at the same point in the loop, the device would think your distance traveled is 0. So it has to sample often enough to accurately account for any route.

For a 10 minute mile pace (6 mph), each second corresponds to 2.68m traveled. To get the GPS error low enough, say 1% error rate, one would need to travel 1000m per sample, and therefore the sample rate should be 1 sample every 373 seconds. However, I think sampling every 373 seconds is entirely too slow, due to the poor route accuracy mentioned above, and I think it makes sense to trade off a bit of distance accuracy for route accuracy. How low can this go? Well, again this gets tricky when thinking about anything other than a straight line path.

Additionally, in practice, the GPS tolerance introduces error in every direction in a 10m radius around the current position, and so what actually happens is that some of the error averages out, and a huge percentage of samples only introduce error closer to the cosine of the angle between the actual position and the measured position. On a test run, I sampled every 10 seconds, and this resulted in a 3 mi run coming out as 2.82 mi, which is 94% accurate, whereas a 10 second sampling rate might imply 62% worst case accuracy. So it seems the sampling rate can go much lower than a worst case analysis would imply. I'm currently beta testing it and sampling every 10 seconds, and this has been acceptable so far for my purposes on the routes I use.

{% include google_analytics.html %}