---
layout: page
title: JRNL
permalink: /jrnl
---

> An encrypted journaling web application
>
> June 2021
>
> Check it out [here](https://jrnl.pmusgrave.dev/)

Journaling is good for you. Privacy is also good for you. So private journaling should be twice as good for you.

The web application is fairly standard database CRUD application development. Encryption was implemented with [CryptoJS](https://www.npmjs.com/package/crypto-js). Journal entries are sent with HTTPS to the backend server, which then encrypts everything using AES and stores encrypted entries in a Postgres database.

{% include google_analytics.html %}

