---
layout: default
title: Geometric proxies
permalink: /structural-elements/geometric-proxies
parent: Structural elements
nav_order: 3
---

# Geometric proxies

* * *

## Overview

In order to render an input set of images as an object in 3D space, image-based rendering methods often rely on an associated *geometric proxy*. In the current version of $TEMP-PROJECT$, the final shape of this proxy is always a 3D mesh, i.e. an explicit collection of 3D points and connecting triangles: intermediate representations (depth maps, focal surfaces) are therefore always converted to an explicit 3D mesh before rendering. Meshes are practical in that they are the default objects used by Unity for rendering, meaning for instance that it is easy to render them with shading and built-in collision handling.

The project relies on three different types of proxies: *global mesh*, *per-view meshes*, and *focal surface meshes*.

## Global mesh

The scene's geometry is perhaps most intuitively represented as a single, all-encompassing mesh: this is the *global mesh* representation. Global meshes are practical in that they regroup all of the dataset's dense geometric information inside a single object. However, they can be quite heavy to store and load, and therefore require effectively handling the trade-off between making the mesh more accurate or more performance-friendly.

<p align="center">
      <img src="https://github.com/DinechinGreg/temp-project/raw/master/docs/illustrations/Calcite.png" alt="" width="480" height="360"><br><i>A global mesh created from images of a calcite mineral.</i>
</p>

## Per-view meshes

A second type of proxy stores the scene's geometry on a *per-view* basis, typically in the shape of one depth map per input image. Per-view rendering, in which only the proxies relevant for the current viewpoint have to be displayed, can be considerably faster and produce higher-quality results. However, there remains the question of achieving an efficient conversion from depth map to per-view mesh.

<p align="center">
      <img src="https://github.com/DinechinGreg/temp-project/raw/master/docs/illustrations/Snow.png" alt="" width="480" height="360"><br><i>A per-view mesh created from a 360-degree image (Snow dataset).</i>
</p>

## Focal surface meshes

For some projects, dense geometry may be deemed to costly to recover: rendering should be done using only the image data. In those cases, images are instantiated in the 3D scene by projecting them on their *focal surfaces*, i.e. a plane for a perspective image, a sphere for a 360° image. $TEMP-PROJECT$ therefore includes solutions based on rendering underlying plane and sphere meshes corresponding to the input photographs' focal surfaces.

<p align="center">
      <img src="https://github.com/DinechinGreg/temp-project/raw/master/docs/illustrations/LegoKnights.png" alt="" width="480" height="360"><br><i>Images from the Lego Knights dataset, projected on their focal surfaces.</i>
</p>
