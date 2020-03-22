---
layout: default
title: Rendering methods
permalink: /structural-elements/rendering-methods
parent: Structural elements
nav_order: 4
---

# Rendering methods

* * *

## Overview

To display an input set of images as an object in 3D space, COLIBRI VR renders the associated [geometric proxy](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies) using a given rendering method. This section describes the general concepts behind the different rendering methods implemented in the project.

## Textured surfaces

- **Description**: Proxies are rendered by retrieving color information from associated texture maps (2D textures onto which 3D meshes' triangles are mapped out). This is arguably the most common way of displaying specific color data on 3D geometry.
- **Most relevant for the geometric proxies**: [global mesh](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies#global-mesh) (texture map is estimated by blending the source images together), [focal surfaces](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies#focal-surface-meshes) (texture maps are the source images).
- **Advantages**: Texture maps are often a compact way of storing color data. Rendering from a texture map is fast.
- **Inconvenients**: The quality of the rendered view depends on the quality of the mapping and on the texture's resolution. View-dependent effects such as specular reflections are not rendered (they are averaged out in the texture instead).

<p align="center">
      <img src="https://github.com/caor-mines-paristech/colibri-vr/raw/master/docs/illustrations/PyriteTexture.png" alt="" width="480" height="360"><br><i>Pyrite global mesh rendered as a textured surface.</i>
</p>

## Unstructured lumigraph rendering

- **Description**: Proxies' color values are blended from the *n* most relevant input photographs based on the output camera's current viewpoint, so as to effectively render view-dependent effects such as specular reflections. The method is based on computing camera blending weights (i.e. values that quantify the relevance of each camera's color contribution in this specific point) in each vertex in real-time. The original algorithm was presented in <a href="#buehler2001">[Buehler et al. 2001]</a>.
- **Most relevant for the geometric proxies**: [global mesh](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies#global-mesh).
- **Advantages**: View-dependent effects are effectively rendered.
- **Inconvenients**: The method can be quite performance-intensive. Rendering artifacts, notably ghosting, are common.

<p align="center">
      <img src="https://github.com/caor-mines-paristech/colibri-vr/raw/master/docs/illustrations/PyriteULR.png" alt="" width="480" height="360"><br><i>Pyrite global mesh rendered using unstructured lumigraph rendering.</i>
</p>

## Angle- and distance-based blending

- **Description**: Per-view proxies are blended where they overlap, with blending weights computed based on angle and distance factors. The distance factor is used to ensure that higher-resolution images are given a higher weight. The angle factor is used to to select images in which the direction of the captured rays closely match the direction of the ray for which color is currently being computed. A soft z-test is used during blending. This method is mostly inspired by the work of <a href="#overbeck2018">[Overbeck et al. 2018]</a>.
- **Most relevant for the geometric proxies**: [per-view meshes](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies#per-view-meshes), [focal surfaces](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/geometric-proxies#focal-surface-meshes).
- **Advantages**: View-dependent effects are efficiently rendered for per-view proxies.
- **Inconvenients**: Rendering artifacts, notably ghosting, are common.

<p align="center">
      <img src="https://github.com/caor-mines-paristech/colibri-vr/raw/master/docs/illustrations/PyritePerView.png" alt="" width="480" height="360"><br><i>Pyrite per-view meshes rendered using angle- and distance-based blending.</i>
</p>

* * *
* * *

## References
{: .d-inline-block }
References
{: .label .label-purple }

<a name="buehler2001"> [Buehler et al. 2001] </a> C. Buehler, M. Bosse, L. McMillan, S. Gortler, and M. Cohen. *Unstructured Lumigraph Rendering.* In 28th Annual Conference on Computer Graphics and Interactive Techniques - SIGGRAPH '01. ACM Press, 2001. doi: [10.1145/383259.383309](https://doi.org/10.1145/383259.383309)

<a name="overbeck2018"> [Overbeck et al. 2018] </a> R. S. Overbeck, D. Erickson, D. Evangelakos, M. Pharr, and P. Debevec. *A System for Acquiring, Processing, and Rendering Panoramic Light Field Stills for Virtual Reality.* ACM Transactions on Graphics, 37(6):1–15, Dec. 2018. doi: [10.1145/3272127.3275031](https://doi.org/10.1145/3272127.3275031)
