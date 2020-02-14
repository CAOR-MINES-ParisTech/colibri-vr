---
layout: default
title: Core components
permalink: /core-components
nav_order: 4
has_children: true
has_toc: false
---

# Core components

* * * 

Using COLIBRI VR, users should be able to go from an input set of photographs to an interactive rendered scene in VR. This is implemented by way of several core components.

- The [Camera model](https://caor-mines-paristech.github.io/colibri-vr/core-components/camera-model) component is used to store camera parameters. It is used in every step of the processing and rendering pipeline.
- The [Acquisition](https://caor-mines-paristech.github.io/colibri-vr/core-components/acquisition) component can be used to create an sample input dataset, by capturing images from a synthetic Unity scene. This can be useful for testing.
- The [Processing](https://caor-mines-paristech.github.io/colibri-vr/core-components/processing) component is used in a preliminary offline step to process the source images into a scene representation ready for rendering, stored as an asset bundle.
- The [Rendering](https://caor-mines-paristech.github.io/colibri-vr/core-components/rendering) component is used at render time to load a processed scene representation into the scene and render it with the selected blending method.
