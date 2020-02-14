---
layout: default
title: Per-view meshes QSTR
permalink: /shader-implementations/per-view-meshes-qstr
parent: Shader implementations
nav_order: 1
---

# Per-view meshes from depth maps by quadtree simplification and triangle removal

* * *

## Overview

This geometry processing method can be used to convert depth maps into meshes, using quadtree-based simplification, and with the option to remove triangles at disocclusion boundaries.

<p align="center">
      <img src="https://github.com/DinechinGreg/temp-project/raw/master/docs/illustrations/BunnyQSTR.png" alt="" width="1500" height="500"><br><i>Per-view meshes from depth maps by quadtree simplification and triangle removal.</i>
</p>

### Quadtree-based simplification

The intuitive way of creating a 3D mesh from a depth map is to transform each pixel in the depth map into a group of four mesh triangles, with the triangles' vertices positioned in 3D space based on the corresponding distance values. This method is perfectly accurate, and can easily be implemented on the GPU as a set of parallel operations. However, it creates a prohibitive amount of vertices/triangles, and is generally sub-optimal: indeed, the depth map is likely to contain large regions that could be approximated, without losing much information, by a far smaller number of triangles.

In $TEMP-PROJECT$, we therefore implement a more optimal alternative, derived from the quadtree-based algorithm presented in <a href="#lee2014">[Lee et al. 2014]</a>. The general idea remains the same: square blocks of the depth map's pixels are transformed into groups of four 3D triangles, ultimately forming a mesh. However, instead of only triangulating blocks of the smallest size (i.e. the pixels themselves), the size of the triangulated region here depends on the depth map's content: larger blocks may be considered if this approximation results in little loss of information. Quadtree division is used to obtain a set of blocks that partition the image with different levels-of-detail (LODs): for instance, a 4x4 depth map will have three LODs (from fine to coarse: 4x4, 2x2, 1x1), defining 21 blocks (16 + 4 + 1) to consider for triangulation. To know whether a group of four triangles can reasonably be created from the given block of pixels, an error metric is computed for the block and is compared with a user-defined error threshold. Computations for each LOD can here again be implemented on the GPU as a set of parallel operations, since the blocks at each LOD partition the image into independent regions. To ensure that the mesh is airtight, i.e. that there are no cracks, the algorithm also includes a correction step by which created triangles can be subdivided so that their vertices match their neighbor's.

### Triangle removal at disocclusion boundaries

The triangle removal option is enabled using the orthogonality and triangle size tests presented in <a href="#pajarola2004">[Pajarola et al. 2004]</a>. This option aims to remove the "rubber sheet" effect that appears at disocclusion boundaries when creating a mesh from a depth map. The algorithm determines whether a triangle should be removed based on two tests. The orthogonality test checks whether the angle difference between the triangle's normal and the direction from the source camera to the triangle's center is below a given threshold. The triangle size test checks whether the triangle's size, modulated by the distance of its center to the source camera, is below a given threshold. If both tests are passed, the triangle is kept; otherwise, it is removed.

## Implementation details

This method is implemented as a compute shader. The different parameters used for the algorithms (e.g. error thresholds) can be defined by users using the graphical user interface.

### Equivalent power-of-two

We want blocks of the finest LOD to consist of single pixels in the depth map. To ensure this, the pixel grid on which to perform quadtree subdivision has to be square and power-of-two. We therefore compute the next power-of-two resolution that is equal to or greater than the depth map's dimensions, and define the quadtree blocks on a square pixel grid of this resolution. At compute time, blocks are then discarded from consideration if they contain pixels beyond the depth map's dimensions. This explains why the edges of the final mesh sometimes consist of small triangles corresponding to the finest LOD.

### Error metric

A block's error value represents the loss of information that would occur if one decided to triangulate this block instead of the finer-LOD child blocks that it contains. If one had triangulated the child blocks, new vertices would have been created at the center of the parent block's edges: the error is based on estimating the loss of information caused by not creating these vertices. For each of the block's edges, we thus compute the distance between the edge's center and the position of the discarded vertex. The block's computed error value is set as the maximum of these edge errors.

Additionally, a parent block's error value must be higher than that of its children. The error value of a block is therefore set as the maximum of the computed value and the error values of its children.

### Fine-to-coarse then coarse-to-fine

In a first step, the implemented method computes and stores the blocks' error values, by iterating on the quadtree LODs in a fine-to-coarse manner. Once these error values have been computed, a second step is launched, this time by iterating on the LODs in a coarse-to-fine manner. For each LOD, the error value is checked against a given threshold, based on which one of two things happens: either the error is low enough that triangles can be created for this LOD, in which case the algorithm does not need to consider the child blocks; or the error is still too high, in which case triangles cannot be created yet and the child blocks have to be considered. Every time a triangle is created, its neighbors are notified so that they can be subdivided adequately to ensure an airtight mesh. If the option is enabled, the triangle removal tests are also performed at this point.

### Parallel computation

For both steps of the process, each LOD iteration is computed in parallel on the GPU using the compute shader, ensuring a fast performance. Once the shader has finished computing the output collection of triangles and vertices, this collection is finally transferred to the CPU and used to create a mesh asset.

* * * 
* * * 

## References
{: .d-inline-block }
References
{: .label .label-purple }

<a name="lee2014">[Lee et al. 2014]</a> E.-S. Lee, J.-H. Lee, and B.-S. Shin. Bimodal Vertex Splitting: Acceleration of Quadtree Triangulation for Terrain Rendering. IEICE Transactions on Information and Systems, E97.D(6):1624–1633, 2014. [doi: 10.1587/transinf.e97.d.1624](https://doi.org/10.1587/transinf.e97.d.1624)

<a name="pajarola2004">[Pajarola et al. 2004]</a> R. Pajarola, M. Sainz, and Y. Meng. DMesh: Fast Depth-Image Meshing and Warping. International Journal of Image and Graphics, 04(04):653–681, Oct. 2004. [doi: 10.1142/s0219467804001580](https://doi.org/10.1142/s0219467804001580)
