---
layout: single
title: Chess
permalink: /chess
defaults:
  # _pages
  - scope:
      path: ""
      type: pages
    values:
      layout: single
      author_profile: true
---

> A 2-player chess program.
>
> [https://github.com/pmusgrave/games](https://github.com/pmusgrave/games)

Chess was one of the first substantial programs I ever wrote, back in high school when I was first learning how to code, and it was one of the first things that really got me hooked on programming. The final project for the course was to make a game, and I got started on the project weeks and weeks before it was due. It was all I could think about. I spent so long perfecting the algorithm for attack logic. When I finally ran out of time and had to turn in the project, it was brittle and had a lot of bugs. The attack algorithm worked, but I spent so long on it that the rest of the program suffered.

The codebase available here on github is not that first chess program, but it's one that I rewrote in a weekend recently. I came back to chess intentionally, to revisit a problem that used to challenge me. It felt like a personal vendetta, an unsolved problem somewhere in the back of my mind. I wanted to see what it would feel like to write chess knowing what I know now. I'm personally pleased with the result, despite the imperfections in this second iteration, and it felt really satisfying to come back to it with more design knowledge. It took me about a day this time, it has a significantly better and more modular object oriented design, and it revitalized that sense of enthusiasm I used to feel about programming. This gave me a lot of ideas of ways to build on chess that I might come back to in the future, such as network play, an AI, better graphics, etc.