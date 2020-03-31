---
layout: default
title: Processing
permalink: /core-components/processing
parent: Core components
nav_order: 3
---

# Processing

* * *

## Overview

The `Processing` component is used to transform the input set of photographs into a scene representation, potentially containing both color and geometric data, stored as an asset bundle. The output of this process is a set of assets that can easily be loaded at render time. 

<p align="center">
      <img src="https://github.com/caor-mines-paristech/colibri-vr/raw/master/docs/illustrations/TerrainsProcessing2.png" alt="" width="1280" height="720"><br><i>Graphical user interface of the Processing component.</i>
</p>

## Source data

The component's graphical user interface starts with a section enabling the user to choose the input data directory. This section also provides information on what the selected directory contains, which can be useful to quickly check that the correct directory has been selected, and that it contains all of the required data.

## External processing helpers

COLIBRI VR can make use of several external tools during processing (see [this section](https://caor-mines-paristech.github.io/colibri-vr/getting-started/installation#optional-steps-linked-external-tools) of the Installation page for more details), notably to perform 3D reconstruction and mesh simplification. We specifically selected external resources that openly provide downloadable executable files, to ensure accessibility to all types of users.

- `COLMAP 3.6`: [COLMAP](http://colmap.github.io/) offers a full 3D reconstruction pipeline, able to estimate camera parameters and 3D meshes from the input set of images. We leverage its command-line interface to provide two functionalities within Unity:
  - `Recover sparse camera setup from images`: This button launches COLMAP's sparse reconstruction pipeline, and stores the camera parameters in a text file. The process also undistorts the input images based on the estimated parameters.
  - `Reconstruct 3D mesh (.PLY) from sparse camera setup.`: This button launches COLMAP's dense reconstruction pipeline, resulting in the creation of a `.PLY` mesh file. It can be launched only after the first process (sparse reconstruction) has finished.
  
- `Blender 2.8`: [Blender](https://www.blender.org/) is an open, general-purpose tool for creating and modifying 3D meshes. We use several of its features:
  - `Convert .PLY mesh to .OBJ file`: This button converts the `.PLY` mesh created in a previous step into a `.OBJ` mesh natively readable by Unity.
  - `Check .OBJ mesh information`: This button displays the number of triangle faces in the `.OBJ` mesh. It is only there for debug purposes.
  - `Simplify .OBJ mesh`: This button launches a simplification process based on Blender's [Decimate](https://docs.blender.org/manual/en/latest/modeling/modifiers/generate/decimate.html) modifier. It can be used to reduce the `.OBJ` mesh's face count.
  - `UV-map .OBJ file`: This button launches a UV-mapping process based on Blender's [Smart UV Project](https://docs.blender.org/manual/en/latest/modeling/meshes/editing/uv/unwrapping/mapping_types.html#smart-uv-project) method.
  
- `Instant Meshes`: [Instant Meshes](https://github.com/wjakob/instant-meshes) is an automatic retopology tool, useful for reworking a mesh so that its faces are spread out evenly and its normals face in coherent directions. We provide one button for this resource, `Perform automatic retopology`, which simply calls the software's main method.

## Data processing

- `Texture array from color data`: This color processing method groups the source photographs together, creating a Unity [Texture Array](https://docs.unity3d.com/Manual/SL-TextureArrays.html) object. Creating a texture array is practical for rendering, as this asset is then interpreted by the GPU as a single object.

- `Per-view meshes from underlying focal surfaces`: This geometry processing method stores mesh assets representing the images' underlying focal surfaces. In practice, it only stores the geometrical primitives corresponding to the focal surfaces, i.e. at most stores one quad mesh and one sphere mesh.

- `Per-view meshes from depth maps by quadtree simplification and triangle removal`: This geometry processing method creates mesh assets from the set of per-view depth maps. For details on the implementation of the meshing process, see the [Per-view meshes QSTR](https://caor-mines-paristech.github.io/colibri-vr/shader-implementations/per-view-meshes-qstr) page.

- `Global mesh from existing file`: This geometry processing method exports the `.OBJ` mesh created previously as a Unity asset.

The `Process source data` button applies the selected processing methods to transform the source data into the desired scene representation. The processed assets' names will be added to the "processing_information.txt" file.

The `Bundle processed data` button compresses the processed data into a Unity [Asset Bundle](https://docs.unity3d.com/Manual/AssetBundlesIntro.html) object, for easy loading at render time. Once this method is done executing, a special line is added to the "processing_information.txt" file to indicate the creation of an asset bundle for this dataset.

* * *

* * *
{: .bg-blue-000 .mb-4 }

Frequently asked questions
{: .label .label-blue }

### Why are the buttons for processing and bundling greyed out?

The first process can only be launched from within play mode.

The second process can only be launched from outside play mode. It requires the first step to have been performed, i.e. for the files to exist in the "processed_data" folder.

* * *
{: .bg-blue-000 .mt-1 }
