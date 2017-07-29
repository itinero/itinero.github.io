---
title: Stable release
subtitle: A first supported version of Itinero
layout: post
type: blog
author: 'Ben Abelshausen'
featured: blog/itinero-1-0.png
featuredbig: blog/itinero-1-0-overview.png
---

We have released v1.0 of Itinero! Get it now via [nuget](https://www.nuget.org/packages/Itinero) or check [github](https://github.com/itinero/routing). We are very proud of this and we tried to limit features to get to v1.0 fast but we could have done better, this release contains a lot of new stuff when comparing with the state of the project back when it was called [OsmSharp](http://www.osmsharp.com/). 

An overview of some of what we chose to include in this release:

#### Different routing algorithms

We support all the classics like Dykstra, A* but also Contraction Hierarchies. We expanded all these to enable support for edge-based routing and advanced turn restrictions. This means we use a modified Contraction Hierarchy at the core of the routing engine.

#### Highly configurable routing profiles

Using lua, a scripting language, we can support a wide range of routing profiles. Users of the Itinero can configure almost any vehicle type. We also support using cycle networks or any OpenStreetMap route relation type. 

We include some default OSM-based profiles:

- [Car](https://github.com/itinero/routing/blob/develop/src/Itinero/Osm/Vehicles/car.lua): A default car profile that support the usual suspects, shortest and fastest profiles, but in addition to that also [a profile](https://github.com/itinero/routing/blob/develop/src/Itinero/Osm/Vehicles/car.lua#L186) that calculates routes giving priorities to roads with higher classifications.
- [Bicycle](https://github.com/itinero/routing/blob/develop/src/Itinero/Osm/Vehicles/bicycle.lua): A default bicycle profile, with again the usuals, shortest and fastest. There are two special bicycle profiles: _balanced_, giving a higher priority to cycling infrastructure, and _networks_ that aggressively follows the many cycle networks mapped in OSM.
- [Pedestrian](https://github.com/itinero/routing/blob/develop/src/Itinero/Osm/Vehicles/pedestrian.lua): A default simple pedestrian profile, may be expanded later to also include walking networks.

#### Routing database

Originally the concept of a routing database, or RouterDb, was introduced because preprocessing source data can take a while and we don't want to repeat this process every time we want to use the routing engine. As a side effect however it has proven to be very useful to separate the data processing from the actual routing code.

There is no dependency on the type of source data used meaning everything is configured in the RouterDb. Even the vehicle profiles are in the RouterDb. No dependency on OSM or a shapefile reader is required, no other dependencies are required to support different vehicles either, and the process of building a routerdb can be done in a separate process.

To read more about the RouterDb concept, check the [docs](https://github.com/itinero/routing/wiki/RouterDb).

#### Memory mapping and mobile devices

Anything Itinero can do is also possible on mobile devices using Xamarin. We use a very simple type of _memory mapping_. This enables Itinero to load a RouterDb by opening it but not loading it entirely into memory. Routeplanning is obviously slower but still gives you very good offline routing performance on mobile devices.

#### Advanced logistical optimization facilities

This project was originally focused on logistical optimization. That's still partly the case and this is why we also decided to include advanced support for usecases in this domain in the initial release.

One of these features is a very fast matrix calculation algorithm, that supports:

- Calculating time and distance simultaneously.
- Full turn-restrictions support.
- Direction-based start and endpoints: for cases where you need to be sure about the direction at start of endpoints.
- Direction-enabled matrices: Calculate matrices 4-times as large as regular weight matrices but containing directional information.

All this enables advanced logistical use cases and optimizations where there is a need for distance and time constrains at the same time or where there is a need for U-turn prevention.


#### Shapefile support

In addition to traditional support for OSM-XML and OSM-PBF files as a source of data, we also support using shapefiles. Most proprietary networks are delivered in this form.

#### Shortcuts

We implemented the concept of shortcuts. This was to support basic and static intermodality support for for example a bike-sharing system. We figured if the bike locations are fixed, so are the shortcuts. We can add these shortcuts to the RouterDb, introduce a bike-share vehicle profile, and include this in a Contraction Hierarchy. 

This results in lightning fast routingplanning for a combination of walking and cycling for example. No reason this cannot apply also to a car-sharing scheme or anything else with fixed shortcuts.

## Get started

The main usecase we target at the moment is using Itinero as a library. To get started check out the core project on GitHub:

[https://github.com/itinero/routing](https://github.com/itinero/routing)

Alternatively get started you can try setting up Itinero as a service using the routing-api project:

[https://github.com/itinero/routing-api](https://github.com/itinero/routing-api)

## The future

Even though we included a lot already, there are many more ideas for the future. We put up [a roadmap](https://github.com/itinero/routing/wiki/Roadmap) with some future ideas, the most important being:

- Dynamic weights, think live traffic.
- Full public transit routing support, some stuff is [already done](https://github.com/itinero/transit).
- Support for dynamic constrains like maxweight or widths. Think one Contraction Hierarchy with constraints.
- Elevation support: Elevation data in the output but also elevation-aware routing.

See something you can use, want your ideas or usecase on this list or are you interested in getting support for Itinero [get in touch](http://www.itinero.tech/#contact), it's what we do!

