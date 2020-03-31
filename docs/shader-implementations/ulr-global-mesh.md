---
layout: default
title: ULR on global mesh
permalink: /shader-implementations/ulr-global-mesh
parent: Shader implementations
nav_order: 2
---

# Unstructured lumigraph rendering on global mesh

* * *

## Overview

This blending method can be used to render a global mesh in a way that displays captured view-dependent effects such as specular highlights.

## Vertex and fragment

This method is implemented as a vertex/fragment shader, following the operations described by <a href="#buehler2001">[Buehler et al. 2001]</a>. In the vertex stage, weights are computed for each of the source cameras (one for each input image), quantifying the relevance of each camera's contribution to the color of the given vertex. This is called the camera blending field: it is used in the fragment stage, where the output color is computed as the weighted contribution of the *n* images most relevant for the given fragment, where *n* is a parameter that can be chosen in the graphical user interface.

## Computing the blending field (relevance metric)

Before computing the blending weight of a given camera for a given vertex, several checks are performed. A preliminary step is to project the 3D position of the vertex into the image to obtain a 2D UV position. The first check verifies that this UV position is within the image's bounds. The second check verifies that the depth in this UV position (i.e. value of the pixel in the corresponding depth map) corresponds to the expected depth given the 3D position of the vertex: a large dissimilarity means that the vertex is probably occluded in the image by another object. The third check verifies that the 3D normal of the vertex is consistent with the orientation of the source camera, which helps more correctly detect occlusions on thin surfaces where the depth difference is small. If any of these checks fail, the blending weight is set to its lowest value, because the given image is not relevant for contributing color to the given vertex.

If the checks are validated, the blending weight of a given camera for a given vertex is computed as follows. An *angle* factor is computed, set to vary with the opposite of the absolute angle difference between two rays, (1) the ray from the render camera to the 3D point and (2) the ray from the render camera to the source camera. For instance, if this angle difference is equal to zero, then the render camera should see exactly what the source camera saw in this 3D point: the weight for the corresponding source image is set to its maximum value. Conversely, if the angle difference is high, then another source image is likely to provide more relevant information: the weight is set to a low value. Second, a *distance* factor is computed, set to vary with the inverse of the distance separating the 3D point and the source camera's position. This is used to give more weight to images that were captured by cameras closer to the point, that are more likely to have seen the point with higher resolution. The combination of angle and distance factors thus defines the final weight, which is used to select which source images are most relevant to recover color information for the given 3D point, in light of the render camera's current position and orientation.

## Interpolating between vertex and fragment

The blending field is computed in the vertex stage instead of the fragment stage in order to enhance performance. This implies that the blending weights of each camera have to be interpolated between the vertex and the fragment stage, in order to obtain blending weights in each fragment. The simplest way to perform this interpolation is to pass the values computed in the vertex stage using the built-in interpolators. However, this approach cannot work if there is a large number of source cameras, because there is only a restricted number of built-in interpolators. Because only *n* source cameras are used in the final blend, we could instead only pass the *n* most important blending weights. However, for the interpolation to work correctly in this way, we need to order the array of blending weights, and we need the weighting order to be the same in every vertex in the triangle to make sure that the interpolation is performed for the blending weights of the same source camera. We therefore add an intermediate geometry stage in our implementation, in which these operations are performed.

## Computing the blending field over several frames

Because VR requires high framerates for comfortable viewing, the graphical user interface for this method also enables spreading the computation of the blending field over several frames. Instead of computing blending weights for each of the mesh's vertices at every frame, the method adaptively diminishes the number of vertices it has to process per frame if the framerate falls below a given threshold, leaving the remaining vertices to be processed at later frames. The vertex/fragment shader is still called in any case, to ensure that the mesh is still displayed: however, the blending field will only be updated completely every *m* frames, where *m* can be specified in the GUI (it should remain quite low for this process to hardly be noticeable).

In vertices where the blending weights have not been updated, the color is given by the previous blending field, stored in a buffer. Each render camera thus has to be assigned a buffer in which to store the blending field for each vertex of the rendered mesh. To this end, this method is implemented using command buffers, and render cameras are assigned a specific script to make sure that the buffers are updated with newly-computed blending weights.

* * * 

* * *
{: .bg-purple-000 .mb-4 }

References
{: .label .label-purple }

<a name="buehler2001">[Buehler et al. 2001]</a> C. Buehler, M. Bosse, L. McMillan, S. Gortler, M. Cohen. *Unstructured Lumigraph Rendering.* SIGGRAPH '01: Proceedings of the 28th Annual Conference on Computer Graphics and Interactive Techniques, 2001. [doi: 10.1145/383259.383309](https://doi.org/10.1145/383259.383309)

* * *
{: .bg-purple-000 .mt-1 }
