---
layout: default
title: Disk-based blending
permalink: /shader-implementations/disk-based-blending
parent: Shader implementations
nav_order: 3
---

# Disk-based blending

* * *

## Overview

This blending method can be used to render per-view proxies (depth-based meshes and focal surface meshes) in a way that displays captured view-dependent effects such as specular highlights.

## Rendering operations

The method is inspired by the work presented by <a href="#overbeck2018">[Overbeck et al. 2018]</a>. The per-view proxies are rendered one after the other, using a shader that blends their color values adaptively for the current viewpoint, in order to render view-dependent effects. To correctly perform this sequence of operations, the method relies on command buffers.

## Vertex and fragment

* * * 
* * * 

## References
{: .d-inline-block }
References
{: .label .label-purple }

<a name="overbeck2018">[Overbeck et al. 2018]</a> R. S. Overbeck, D. Erickson, D. Evangelakos, M. Pharr, and P. Debevec. A System for Acquiring, Processing, and Rendering Panoramic Light Field Stills for Virtual Reality. ACM Transactions on Graphics, 2018, [doi: 10.1145/3272127.3275031](https://doi.org/10.1145/3272127.3275031).
