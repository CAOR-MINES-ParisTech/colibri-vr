---
layout: default
title: Camera model
permalink: /core-components/camera-model
parent: Core components
nav_order: 1
---

# Camera model

* * *

## Overview

In the toolkit, real-world cameras are represented using custom `Camera model` components, that can be added to GameObjects. These components have several key parameters:
- Position: a `Vector3` representing the position of the camera in world space.
- Rotation: a `Quaternion` representing the orientation of the camera in world space.
- Field-of-view: a `Vector2` representing the horizontal and vertical field-of-view of the camera, in degrees.
- Pixel resolution: a `Vector2Int` representing the horizontal and vertical pixel resolution of the camera, in number of pixels.
- Index (in the camera setup): an `int` representing the camera's index in the camera setup.

Note that the position and rotation parameters are stored in the `Transform` component to which the camera model is attached.

## Projection type

The camera model supports two projection types: perspective and omnidirectional. A camera is considered omnidirectional if its horizontal field-of-view is set to a value of 360 degrees. In this case, the corresponding images are expected to be 360° equirectangular images, and the camera model's vertical field-of-view is set to be equal to 180 degrees.

## Visual representation

Cameras are represented in Unity's Scene view using gizmos. Perspective cameras use the "frustum" gizmo, while omnidirectional cameras use the "sphere" gizmo.

Two color schemes can be used. The default color scheme displays all cameras in cyan, except the currently selected one, which is colored yellow. An alternative color scheme can be toggled, in which each camera is assigned a different color, enabling users to better understand the contribution of each camera to the blending field during rendering.

<p align="center">
      <img src="https://github.com/caor-mines-paristech/colibri-vr/raw/master/docs/illustrations/Fountain.png" alt="" width="480" height="360"><br><i>Camera models (Fountain dataset) represented with gizmos, using the two color schemes.</i>
</p>

* * * 

* * * 
{: .bg-blue-000 .mb-4 }

Frequently asked questions
{: .label .label-blue }

### Can I use any real camera to capture the source photographs?

Any real camera can be used to capture the input photographs, so long as the external tools used during processing are able to effectively estimate camera parameters and undistort the images.

Our recommendation is to perform these steps via COLMAP, which provides a thorough [list of camera models to choose from](https://colmap.github.io/cameras.html), and should thus be able to handle image sets captured by most types of cameras. COLIBRI VR's interface enables launching COLMAP's methods from within Unity.

Note that we do require the images to be undistorted for rendering, and therefore do not include any radial distortion parameter in the camera model.

### How is the camera model related to Unity's built-in Camera component?

COLIBRI VR's camera model and Unity's `Camera` component do not have the same role: the `Camera` component's goal is to render to a display, whereas our camera model is simply used to store a set of parameters.

Nonetheless, we did implement methods to transfer a COLIBRI VR camera model's parameters to and from a Unity `Camera`. This is useful for example when using the [Acquisition](https://caor-mines-paristech.github.io/colibri-vr/core-components/acquisition) tool to capture images from synthetic scenes. 

* * * 
{: .bg-blue-000 .mt-1 }
