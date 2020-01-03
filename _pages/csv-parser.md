---
layout: single
title: csv-parser
permalink: /csv-parser
defaults:
  # _pages
  - scope:
      path: ""
      type: pages
    values:
      layout: single
      author_profile: true
---

> CSV (Comma Separated Values) parser
>
> October 2017
>
> [https://github.com/pmusgrave/csv-parser](https://github.com/pmusgrave/csv-parser)

Believe it or not, this started out as a take home exercise for a coding interview. The exercise stipulated that I was unable to use any external libraries, and unfortunately node.js (my language of choice at the time) doesn't have a CSV parser built into its standard library. This parser module ended up being a self-contained unit however, and so I split it out into its own repository and have ended up using it in projects many times since then. It has both synchronous and asynchronous versions for different situations and input sizes, following the node.js idiom.