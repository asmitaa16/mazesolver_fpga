---
layout: default
title: The main Module
nav_order: 3
---

# The FINAL boss!

After configuring all our sensors and generating PWM signals, it's the right time to finally start building on the main algorithm that is supposed to be solving the maze! The journey is gonna be amazing, we promise!

There are quite a lot of tried and tested methods to solve a maze. To name a few, we have simple wall-following algorithms, search-based algorithms like Depth-First Search and Breadth-First-Search, path-planning based ones like A* or Djikstra's and the ones we like the most- Flood fill and Tremaux's algorithm. 
But here's the catch, we used none of them (LOL). Lemme be frank, we were first awed by the flood fill algorithm and made the arrays and wrote up the logic for updating values in the arrays as the bot traversed the maze, but it was highly expensive computationally and competition deadline constraints left us with little time for spending long hours on optimisation. 
So the plan changed. Our target now was to write a simple yet efficient algorithm for our bot to solve the maze. We had another constraint up our sleeves- the competition rules required us not to take the shortest path but to build an algorithm that visits as many of the dead ends as possible (8 did we manage to visit out the 9) and complete the whole exploration in a limit of 200 steps.

