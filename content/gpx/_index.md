---
title: "ORB and GPX: two standards, one roadbook"
lead: "For nearly two decades, GPX (GPS eXchange Format) has been the lingua franca of GPS data exchange."
---

_TL;DR: Yes, you can encode a full roadbook using GPX extensions; no, you probably shouldn’t._

Cyclists, hikers, pilots, delivery fleets, commuters, and rally drivers all rely on GPX because it is universal. A GPX file created on one device will almost always load on another. That universality comes from a deliberately simple focus on geometry: points, tracks, and routes. It is a strength for interoperability, but also a constraint for domains that deviate from a linear sequence of coordinates.

A roadbook does not begin with latitude and longitude. It begins with what a participant must do and be aware of: turns, hazards, tulip symbols, distances, timing notes, neutralisation zones, alternate paths, and the structure of stages. Some of these instructions have precise coordinates; some have only approximate locations; some do not meaningfully have a location at all. GPX can attach arbitrary semantics through `<extensions>`, and software that understands a given namespace can interpret them. But every route point in GPX is, by definition, a point on the earth’s surface. Even a purely logical instruction has to be dressed up with a `lat` and `lon` to exist in a `<rtept>`. That is perfectly valid GPX, but it is a geometric mould being used to house non-geometric concepts.

This is where OpenRoadBook enters the picture. ORB is a dedicated schema that models roadbooks explicitly: instruction types, hazards, tulips, branches, metadata, and validation rules are first-class concepts. Geometry can be attached where it is useful, and omitted where it is not. Instructions are not required to be points on a map. YAML is used as the concrete format, not because authors are expected to write roadbooks by hand, but because it keeps the data transparent and easy for tools to read, manipulate, and validate against the published schema. The schema — the model of stages, branches, and instructions — is what matters.

This also affects structure. In GPX, the closest way to represent a roadbook is through one or more `<rte>` elements and their `<rtept>` children. However, a GPX route is only an ordered list of points. Stages, alternative sections, and other higher-level groupings must be expressed indirectly, for example by defining an extension like `<orb:stage>` that refers to several `<rte>` elements by ID. That works, but it effectively introduces a second model on top of GPX: one model for geometry, another for the roadbook itself. In ORB, stages and branches are first-class containers in the schema.

ORB is not intended to replace GPX, because the two formats do not serve the same purpose. The result of following the instructions in a roadbook can be encoded in a GPX track; that GPX track alone cannot be used to reconstruct a roadbook. This implies that a roadbook is a semantic superset of any GPX file. For that reason, the ORB standard makes no attempt to define a mapping between ORB and GPX.

ORB tooling may offer GPX export as a convenience, producing one or more routes, tracks, or waypoints derived from the geometric interpretation of a roadbook, with or without additional metadata. Such exports are inherently lossy projections intended for compatibility with conventional GPS devices, not alternative representations of the roadbook itself.

The ORB standard remains focused on defining the roadbook model itself, and avoids prescribing how to project it onto geometry-only formats.
