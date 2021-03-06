---
title: Introducing the Optimization Module
subtitle: A logistical optimization module for Itinero.
layout: post
type: blog
author: 'Ben Abelshausen'
featured: blog/optimization-animated.gif
featuredbig: blog/optimization-header.png
---

The Itinero project originally started as a logistical optimization project for newspaper delivery. We built a new and improved version on top of the current [routing core](https://github.com/itinero/routing). In [this first version](https://github.com/itinero/optimization) we support routes for one vehicle at time, check out the [Travelling Salesman Problem (TSP)](https://en.wikipedia.org/wiki/Travelling_salesman_problem) for more information. We use a combination of Genetic Algorithms, local search and Guided Neighbourhood Search to get good results very fast.

## Supported Problems

At the moment we support the following problem types:

- TSP: The default travelling salesman problem.
- Directed TSP: The TSP with costs for turns.
- TSP-TW: The TSP with time window constraints.
- Directed TSP-TW: The TSP-TW with costs for turns.
- STSP: The selective travelling salesman problem, generates routes with as much locations as possible with a maxium travel time.
- DirectedSTSP: Identical to the STSP but with u-turn prevention.

An example solution, from a sequence of points to a solution route:

<img src="/img/blog/optimization-tsp.png" style="max-width: 100%;"/>  
*A fastest route along a sequence of points.*

**U-turns**

Another thing we did is add support for U-turn prevention. While this is something we already have in the Itinero routing engine itself, there is also a need to implement this at the level of the optimization code. 

We ask the question: Is it allowed or a good idea to make U-turns at the points we are travelling along. Sometimes it will be, if for example we have to make longer stops at each point or when using a bicycle, but most of the time, for example for newspaper delivery or waste collection it's best to avoid U-turns. This is especially true when travelling with big trucks.

So we implemented U-turn prevention in all of the supported optimization problems, an example is shown here for the TSP. This is the same sequence of points except with a cost given to U-turns:

<img src="/img/blog/optimization-tsp-uturns.png" style="max-width: 100%;"/>  
*A fastest route along a sequence of points, taking into account the cost of U-turns.*

**Support for multiple vehicles**

This is ideal for simple logistics problems, or shortest routes along several POI's, but we are planning to expand to routing calls with multiple vehicles soon.

Check out the project and it's documentation on [GitHub](https://github.com/itinero/optimization)! Get [in touch](http://www.itinero.tech/#contact) with us if you have questions or want to see some extra features added!
