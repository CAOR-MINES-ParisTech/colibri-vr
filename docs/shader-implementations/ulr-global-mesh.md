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

This blending method can be used to render a global mesh in a way that displays captured view-dependent effects such as specular highlights. It is a good baseline for view-dependent image-based rendering, as it efficiently demonstrates the potential of such methods for photorealistically replicating visual highlights and reflections, and has frequently been used by recent works as a reference point for comparison.

## Vertex and fragment

This method is implemented as a vertex/fragment shader, following the operations described by <a href="#buehler2001">[Buehler et al. 2001]</a>. In the vertex stage, weights are computed for each of the source cameras (one for each input image), quantifying the relevance of each camera's contribution to the color of the given vertex. This is called the camera blending field. It is used in the fragment stage, where the output color is computed as the weighted contribution of the *n* images most relevant for the given fragment, where *n* is a parameter that can be chosen in the graphical user interface.

## Relevance metric and computing the blending field

Relevance is here defined based on the considerations outlined in the original publication on ULR: more weight is given to cameras in which the vertex is seen from an angle similar to that of the current viewpoint, and that are closer to the given vertex (to select higher-resolution information), while discarding those in which the vertex is occluded by another object.

More specifically, the rendering process starts with a view selection step, during which several validity checks are performed to exclude irrelevant source cameras. For instance, at the start of every frame, any source camera facing in the direction opposite to the viewer's current orientation is excluded from the blending field, because such a camera could not have captured any surface visible in the rendered view. Additionally, when selecting the cameras most relevant to provide color in a given 3D point, the algorithm also excludes those with a pose and field of view such that the point would have fallen outside of the corresponding image. In the same way, if there is too large a dissimilarity between the point's 3D position and the recorded depth value in a given source image, then it is likely that in this image the point was occluded by another object: therefore, the corresponding source camera cannot provide relevant color information in this point. Using these validity checks, incorrect color information is thus prevented from being included during blending.

Before computing the blending weight of a given camera for a given vertex, several checks are performed. A preliminary step is to project the 3D position of the vertex into the image to obtain a 2D UV position. The first check verifies that this UV position is within the image's bounds. The second check verifies that the depth in this UV position (i.e. value of the pixel in the corresponding depth map) corresponds to the expected depth given the 3D position of the vertex: a large dissimilarity means that the vertex is probably occluded in the image by another object. The third check verifies that the 3D normal of the vertex is consistent with the orientation of the source camera, which helps more correctly detect occlusions on thin surfaces where the depth difference is small. If any of these checks fail, the blending weight is set to its lowest value, because the given image is not relevant for contributing color to the given vertex.

Then, if the checks are validated, the blending field is computed using a weight function similar to the one described in <a href="#buehler2001">[Buehler et al. 2001]</a>. The weight of a given camera in a given 3D point is thus computed as the weighted sum of an angle term and a distance term. The angle factor is set to vary with the opposite of the absolute angle difference between two rays, (1) the ray from the render camera to the 3D point and (2) the ray from the render camera to the source camera. This notably ensures that the weight is set to its maximum value if the angle difference is equal to zero: indeed, a zero-value angle difference means that the ray from the viewer to the 3D point goes through the source camera, thereby justifying a maximum weight for this camera. Conversely, if the angle difference is high, then another source image is likely to provide more relevant information: the weight is set to a low value. Then, we compute the distance factor, set to vary with the inverse of the distance separating the 3D point and the source camera's position. This is used to give more weight to images that were captured by cameras closer to the point, that are more likely to have seen the point with higher resolution. By finally combining the angle and distance factors, we thus obtain an output weight designed for rendering view-dependent effects while also prioritizing high-resolution information.

## Interpolating between vertex and fragment

Two versions of the method are implemented in COLIBRI VR. The first computes the blending field in the fragment stage, which is likely to yield better results, but is also much more computationally expensive. The second computes the blending field in the vertex stage instead to enhance performance, in which case the blending weights of each camera have to be interpolated between the vertex and the fragment stage, in order to obtain blending weights in each fragment.

For this second version, the simplest way to perform the interpolation is to pass the values computed in the vertex stage using the built-in interpolators. However, this approach cannot work if there is a large number of source cameras, because there is only a restricted number of built-in interpolators. Alternatively, because only *n* source cameras are used in the final blend, COLIBRI VR only passes the *n* most important blending weights. To do this correctly, the blending weights have to be sorted, and the weighting order has to be the same in every vertex in the triangle to make sure that the interpolation is performed for the blending weights of the same source. Therefore, the implementation includes an intermediate geometry stage, in order to perform these operations. The blending field is thus effectively transferred between the vertex and fragment stages.

## Computing the blending field over several frames

Because VR requires high framerates for comfortable viewing, the graphical user interface for this method also enables spreading the computation of the blending field over several frames.  Therefore, instead of computing blending weights for each of the mesh's vertices at every frame, the method adaptively diminishes the number of vertices it has to process per frame if the framerate falls below a given threshold, using a sliding window to iterate over the entire set over the next few frames. Using this method, it thus takes at most *m* frames to update the appearance of the entire mesh, where *m* can be specified by the user in the GUI (it should remain relatively small for the difference to hardly be noticeable).

Note that the vertex/fragment shader is still called even in areas for which the blending weight is not updated, to ensure that the mesh is still displayed. In vertices where the blending weights have not been updated, the color is thus given by the previous blending field, stored in a buffer. Therefore, each render camera is assigned a buffer in which to store the blending field for each vertex of the rendered mesh, along with a script to update this buffer with newly-computed blending weights.

* * * 

* * *
{: .bg-purple-000 .mb-4 }

References
{: .label .label-purple }

<a name="buehler2001">[Buehler et al. 2001]</a> C. Buehler, M. Bosse, L. McMillan, S. Gortler, M. Cohen. *Unstructured Lumigraph Rendering.* SIGGRAPH '01: Proceedings of the 28th Annual Conference on Computer Graphics and Interactive Techniques, 2001. [doi: 10.1145/383259.383309](https://doi.org/10.1145/383259.383309)

* * *
{: .bg-purple-000 .mt-1 }
