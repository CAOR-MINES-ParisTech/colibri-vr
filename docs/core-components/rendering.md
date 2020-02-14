---
layout: default
title: Rendering
permalink: /core-components/rendering
parent: Core components
nav_order: 4
---

# Rendering

* * *

## Overview

The `Rendering` component is used to load the assets in the processed bundle and render them in the scene using the specified blending method.

<p align="center">
      <img src="https://github.com/caor-mines-paristech/colibri-vr/raw/master/docs/illustrations/TerrainsRendering2.png" alt="" width="1280" height="720"><br><i>Graphical user interface of the Rendering component.</i>
</p>

## Rendering methods

### Textured surfaces

- `Textured focal surfaces`: This renders the [focal surface meshes](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies#focal-surface-meshes) geometric proxy using the [textured surfaces](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/rendering-methods#textured-surfaces) rendering method.

- `Textured per-view meshes`: This renders the [per-view meshes](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies#per-view-meshes) geometric proxy using the [textured surfaces](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/rendering-methods#textured-surfaces) rendering method.

- `Textured global mesh`: This renders the [global mesh](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies#global-mesh) geometric proxy using the [textured surfaces](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/rendering-methods#textured-surfaces) rendering method.

### Unstructured lumigraph rendering

- `Unstructured lumigraph rendering on global mesh`: This renders the [global mesh](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies#global-mesh) geometric proxy using the [unstructured lumigraph rendering](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/rendering-methods#unstructured-lumigraph-rendering) rendering method.

### Angle- and distance-based blending

- `Disk-blended focal surfaces`: This renders the [focal surface meshes](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies#focal-surface-meshes) geometric proxy using the [angle- and distance-based blending](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/rendering-methods#angle--and-distance-based-blending) rendering method.

- `Disk-blended per-view meshes`: This renders the [per-view meshes](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies#per-view-meshes) geometric proxy using the [angle- and distance-based blending](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/rendering-methods#angle--and-distance-based-blending) rendering method.

## Evaluation methods

- `Cb+Cr`: This compares the rendered view with the original image using the [Cb+Cr](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/evaluation-methods#cbcr) evaluation metric.
