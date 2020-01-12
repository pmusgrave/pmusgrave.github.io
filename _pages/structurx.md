---
layout: single
title: Structurx Structual Engineering CAD Software
permalink: /structurx
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
> Contract position, April 2019 - August 2019
>
> private repository

I designed and built structural engineering CAD software in C# using the .NET WPF framework. This software automates and streamlines the workflow for a lot of repetitive tasks in structural engineering.

There are a few main components to this project which I designed to be as modular as possible. First, much of the workflow involves entering structure dimensions and distance measurements into forms, which are subsequently used to perform engineering calculations. I designed a form validation module that uses regular expressions to prevent invalid data entry and display values in the correct format, regardless of the input format. For instance, the user can input values in a variety of distance formats, such as 1ft 2in, 1' 2", 1 foot 2 inches, etc, and the form validator will convert all values to one particular format. This module can be parameterized to validate many types of inputs, and it is used throughout the software.

The .NET WPF framework has a very similar design process as other data binding frameworks used on the web and elsewhere, such as React, Vue, or Angular. This architecture simplifies the design considerations and keeps data synchronized between the user interface and backend.

Additionally, there is a 3D graphics component which is used to display the structure as the engineer works on the project. The 3D pane is synchronized to the backend data model, so that changes in either the backend forms or frontend 3D models are synchronized automatically, bidirectionally.