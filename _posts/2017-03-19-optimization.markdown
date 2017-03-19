---
title: Introducing the Optimization Module
subtitle: A logistical optimization module for Itinero.
layout: post
type: draf
author: 'Ben Abelshausen'
featured: 
---

The Itinero project got started as a logistical optimization project for newspaper delivery. Nowadays we seperate the optimization code, meaning, the code that calculates in what order a sequence of points have to be travelled along to get the best travel time. In this [first version](https://github.com/itinero/optimization) we only do this for one vehicle at time. For those that know this stuff, we're talking about the [Travelling Salesman Problem (TSP)](https://en.wikipedia.org/wiki/Travelling_salesman_problem).

## Supported Problems

At the moment we support the following problem types:

- TSP: The regular TSP, see above.
- STSP: The selective TSP, only a subsets of points is included in the solution.
- TSP-TW: The TSP where some points have a time-window. Think stores that have opening hours for example.

An example solution, from a sequence of points to a solution route:

![](/img/blog/tsp.png)
*A fastest route along a sequence of points.*

Now this is ideal for simple logistical optimization problems, or routes along several POI's. 

## U-turns

Another thing we did is add support for U-turn prevention. While this is something we already have in the Itinero routing engine itself, there is also a need to implement this at the level of the optimization code. 

We aske the question: Is it allowed or a good idea to make U-turns at the points we are travelling along. Sometimes it will be, if for example we have to make longer stops at each point, but most of the time, for example for newspaper delivery or waste collection it's best to avoid U-turns. This is especially true when travelling with big trucks.

So we implemented U-turn prevention in all of the supported optimization problems, and example is here for the TSP. This is the same sequence of points except with a cost given to U-turns:

![](/img/blog/uturns.png)
*A fastest route along a sequence of points, taking into account the cost of U-turns.*

Check out the project and it's documentation on [GitHub](https://github.com/itinero/optimization)! Get [in touch](http://www.itinero.tech/#contact) with us if you questions or want to see some extra features added!