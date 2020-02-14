---
layout: default
title: Acquisition
permalink: /core-components/acquisition
parent: Core components
nav_order: 2
---

# Acquisition

* * *

## Overview

The `Acquisition` component is used to capture sets of images from synthetic Unity scenes. Using the component's graphical user interface, users can select:
- the parameters of the acquisition setup (shape, number of cameras)
- the parameters of the acquisition cameras (projection type, field-of-view, resolution, range)
- whether to capture geometric data (per-view depth, global geometry)

The images, as well as setup and camera parameters, are then stored to a directory specified by the user.

<p align="center">
      <img src="https://github.com/caor-mines-paristech/colibri-vr/raw/master/docs/illustrations/BunnyAcquisition2.png" alt="" width="1280" height="720"><br><i>Graphical user interface of the Acquisition component.</i>
</p>

## Acquisition setup

- `Type`: This parameter can take two values:
  - `Grid`: Cameras will be evenly arranged on a rectangular grid, facing the local `+Z` direction. The width and height of the grid is defined by the `Transform` component's `X` and `Y` scale parameters.
  - `Sphere`: Cameras will be evenly arranged on an ellipsoid. Facing direction is specified by another parameter, `Direction`, which can be set to either `Inwards` or `Outwards`. The length of each of the ellipsoid's axes is defined by the `Transform` component's `X`, `Y`, and `Z` scale parameters.
- `Per row/H arc`: This parameter defines the number of cameras per row of the grid / per horizontal arc of the ellipsoid.
- `Per column/V arc`: This parameter defines the number of cameras per column of the grid / per vertical arc of the ellipsoid.

## Camera parameters

- `Prefab`: A prefab of an object with a Unity `Camera` component must be specified here. This can for instance be used to capture the images with postprocessing effects.
- `Camera projection`: This parameter can take two values: `Perspective` for a standard pinhole camera, `Omnidirectional` for a 360-degree camera (captured images will be equirectangular).
- `Resolution`: This parameter defines the width and height of the captured images, in pixels.
- `Field-of-view`: (Only if `Perspective`) This parameter defines the horizontal and vertical field-of-view of the acquisition cameras, in degrees. Note that only the horizontal field-of-view can be modified: the vertical field-of-view is computed automatically based on the image resolution and horizontal field-of-view.
- `Range`: This parameter defines the clipping planes of the acquisition cameras: a camera will not capture objects nearer than its near plane, or farther than its far plane.

## Geometry acquisition

- `Per-view depth`: If this parameter is toggled, the acquisition process will also store a depth map for each captured image.
- `Global mesh`: If this parameter is toggled, the acquisition process will also store the meshes in the scene as a single global mesh.

## Output data directory and capture button

The final section of the component's graphical user interface enables the user to select the output directory, and to launch acquisition at the click of a button. Note that the output directory should be seen as the root directory of the dataset, not the "images" folder itself (see the [File structure](https://caor-mines-paristech.github.io/colibri-vr/documentation/file-structure) page).

* * *
* * *

## FAQ
{: .d-inline-block }
Frequently asked questions
{: .label .label-blue }

### Why is the capture button greyed out?

The acquisition process can only be performed from within play mode. Launch play mode to be able to click on the button.
