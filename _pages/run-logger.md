---
layout: single
title: IoT Run Logger
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

Additionally, I think this is better than step-counting products like Fitbit because using a GPS module makes this extremely accurate, to within the tolerance of GPS measurements, which vary by a few meters in the worst case. Fitbit essentially only gives you a rough idea of how far you went. And having an Internet connection built-in means it's very simple to log data and give yourself insights to your fitness progress over time.

For now (and this is subject to change), I'm using a Raspberry Pi as an MQTT broker to handle messages from the device and send them to a Node.js script which handles communicating with my logging database. I'm just logging runs as Google Calendar events, so the Node.js script uses the Google Calendar API to create a new event whenever new MQTT messages are published from the device. If this were to be used by other people, I would probably need to swap out the logging system for something better. Google calendar works for my needs because all I really want to know is distance, time, and date, and glancing over my Google calendar is good enough for me. But a more complete log would make it easier to visualize run times and graph performance over time.

At the time of writing, I'm still waiting on a GPS module to arrive in the mail, which means that it cannot automatically record distance just yet. The rest of the application is complete and unit tested though, so at the moment it functions as a full-featured Internet connected stopwatch, and publishes an MQTT message and a Google calendar event when a run is completed.

{% include google_analytics.html %}