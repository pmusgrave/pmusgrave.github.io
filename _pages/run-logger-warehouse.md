---
layout: page
title: Run Logger Analytics
permalink: /run-logger-analytics
---

> Extensions to my [GPS Run Logger](/runlogger) backend
>
> May 2021
>
> Check it out [here](https://github.com/pmusgrave/run-logger)

I extended the backend portion of my GPS runlogger project by writing a data warehousing script that stores everything in a local MySQL database and an additional script that gives me some analytics on my running performance. For whatever reason, when I started all of these projects, I decided to keep track of my run data in Google Calendar (a terrible idea). It does have some nice qualities (it almost looks like a free offsite cloud database if you squint), and actually works as a sort of data entry application. But I have no hesitation in saying it was a bad idea and I should fix it. Regardless of this technical debt, I wanted to store my data in a more permanent form that I have more control over, and the most straightforward way to do this was to write an ETL script to get my existing data using the Google Calendar API.

{% include google_analytics.html %}

