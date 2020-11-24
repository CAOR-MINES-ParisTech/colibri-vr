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

This blending method can be used to render per-view proxies (depth-based meshes and focal surface meshes) in a way that displays captured view-dependent effects such as specular highlights. The method is inspired by the work presented by <a href="#overbeck2018">[Overbeck et al. 2018]</a>. It renders each per-view proxy one after the other, thereby consecutively adding to the rendered image's color. Each added color value is then scaled by a blending weight, computed based on considerations similar to those used to compute the weights of unstructured lumigraph rendering. The total weight of an output pixel is stored in the texture's alpha channel, so that the output color values can be normalized after all per-view proxies have been drawn.

<p align="center">
      <img src="https://github.com/caor-mines-paristech/colibri-vr/raw/master/docs/illustrations/DiskBasedBlending.png" alt="" width="1491" height="388"><br><i>Disk-based blending applied to render a dataset from the Stanford Light Field Archive.</i>
</p>

## Blending procedure

Each input image is projected into the scene based on underlying geometry, with different weights assigned to different areas of each image to ensure that the parts most relevant for the current viewpoint are given more weight. Specifically, an angle factor is used such that weights are distributed on each image in the form of disks centered around the point of the image most relevant given the user's current head position, with weight values gradually falling off near the edges of the disk. All of the displayed color information is then combined based on these weights.

Disk-based blending is particularly interesting in that its design makes it both fast enough for VR and capable of scaling relatively well to large numbers of images. Indeed, each image is weighted independently from the others, with no need for computationally expensive steps such as ULR's loop over all images to select only the most relevant. This method can thus be an interesting alternative when having to render view-dependent highlights in a scene captured from a large number of viewpoints, that generally performs similarly to ULR in terms of visual quality.

## Depth testing challenges

When per-view depth information is available, the algorithm is thus designed to blend overlapping per-view meshes. However, finding the right form of depth testing is a challenge, as three potentially conflicting goals come into play. As a first goal, we want closer surfaces to occlude those behind them. This is true even within a single mesh: because per-view meshes are potentially non-convex, self-occlusions have to be handled. However, as a second goal, we do not want stretched triangle artifacts from one mesh to occlude relevant visual information from another. Moreover, as a third goal, we do not want one per-view mesh to occlude another representing the same object, as both may contribute relevant color information during blending. Such occlusions are likely to happen, because per-view meshes representing the same object are expected to closely overlap in 3D space. Therefore, while depth testing cannot be disabled completely (due to the first goal), the standard z-test is inadequate (for the second and third goals).

To solve this, in <a href="#overbeck2018">[Overbeck et al. 2018]</a>, the authors thus propose keeping the depth test within each mesh (i.e. handling intra-image occlusions, which achieves part of the first goal) but removing it when comparing meshes (i.e. ignoring inter-image occlusions, which achieves the second and third goals). Implementation-wise, this is done by keeping the z-test overall, but rendering each per-view mesh consecutively to a different depth range, so as to ensure that later meshes are always drawn on top of previous ones and thus that no surface is discarded.

In COLIBRI VR, this is implemented by relying on Unity's command buffers, that give control over the order of the rendering operations. In this way, the proxies' depth values can be scaled to ensure that those rendered later always appear on top of those rendered first. These values are then unscaled when finally writing to the depth buffer, so as not to incorrectly write over virtual objects that have been drawn before nor prevent future objects from being drawn correctly.

## Soft depth test with stretched triangle detection

One of the drawbacks of the original disk-based blending strategy is that it may result in colors from unrelated objects being blended together, because inter-image depth testing is removed completely. Instead, the method implemented in COLIBRI VR uses a soft depth test - i.e. that discards data only if it is beyond a given distance of the already written depth, which is less harsh than the standard z-test - to detect inter-image occlusions. This helps better achieve the first goal, while not causing a challenge to the third one (as standard depth testing would have). To prevent this soft depth test from causing occlusions by stretched triangles (i.e. to achieve the second goal), the implementation relies on a heuristic for detecting disocclusion edges, which is used to remove the stretched surfaces completely.

The soft depth test is implemented in Unity using a ping-pong buffer system to read and write depth in the rendering shader. Additionally, to detect whether a given triangle is likely to result in a stretching artifact due to being at a sharp depth edge, the method applies the orthogonality and triangle size tests presented in <a href="#pajarola2004">[Pajarola et al. 2004]</a>. The orthogonality test checks whether the angle difference between the triangle's normal and the direction from the source camera to the triangle's center is below a given threshold. The triangle size test checks whether the triangle's size, modulated by the distance of its center to the source camera, is below a given threshold. If both tests are passed, the triangle is not considered problematic; otherwise, it is classified as part of a disocclusion boundary, and can thus be removed (during processing or rendering) as necessary.

## Rendering light fields on image planes

Beyond depth-based meshes, this method can also easily be adapted to render light fields on image planes, when no estimated geometry is available. Each image is thus projected as a quad in 3D space, at a given focal distance that separates it from the corresponding camera center. Images are then blended wherever they overlap, using the disk-based blending weights described above. This representation is essentially interesting when considering sets of images densely packed together, e.g. datasets captured using light field camera systems with small baselines. Indeed, in this case, the lack of geometry can be compensated by the dense sampling of visual information, combined adequately using the view-dependent blending weights. As before, these weights also ensure that specular effects are rendered as the viewer moves around. Additionally, if the images are taken by perspective cameras facing in the same direction, the focal distance parameter can be increased or decreased to put different parts of the scene into focus, as the images are blended together at different depths. Finally, drawing the scene in this way is particularly interesting for performance reasons: indeed, quads are fast to render due to their small number of vertices, and, because the different images use the same 3D proxy, GPU instancing can be applied to render the entire set in a single draw call.


* * * 

* * *
{: .bg-purple-000 .mb-4 }

References
{: .label .label-purple }

<a name="overbeck2018">[Overbeck et al. 2018]</a> R. S. Overbeck, D. Erickson, D. Evangelakos, M. Pharr, and P. Debevec. *A System for Acquiring, Processing, and Rendering Panoramic Light Field Stills for Virtual Reality.* ACM Transactions on Graphics, 2018, [doi: 10.1145/3272127.3275031](https://doi.org/10.1145/3272127.3275031).

<a name="pajarola2004">[Pajarola et al. 2004]</a> R. Pajarola, M. Sainz, and Y. Meng. *DMesh: Fast Depth-Image Meshing and Warping.* International Journal of Image and Graphics, 04(04):653–681, Oct. 2004. [doi: 10.1142/s0219467804001580](https://doi.org/10.1142/s0219467804001580)

* * *
{: .bg-purple-000 .mt-1 }
