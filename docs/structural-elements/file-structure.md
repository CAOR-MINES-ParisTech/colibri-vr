---
layout: default
title: File structure
permalink: /structural-elements/file-structure
parent: Structural elements
nav_order: 1
---

# File structure

* * *

## Overview

A typical processed dataset will have the following structure:

```
── Unity project                                         (Folder containing the Unity project)
   └─── Data                                             (Folder containing the datasets used by the Unity project)
        └─── Dataset                                     (Folder containing the data for a given source dataset)
             └─── images                                 (Folder, called "images", containing the photographs)
             └─── sparse                                 (Folder containing the estimated parameters of the setup)
                  └─── cameras.txt                       (File describing the camera models used for this dataset)
                  └─── images.txt                        (File assigning extrinsic parameters, a camera model, and an index to each image)
             └─── processed_data                         (Folder containing the final processed image and geometry data)
                  └─── processing_information.txt        (File containing information on the processed assets)
             └─── bundled_data                           (Folder containing a bundled version of processed_data)
             └─── additional_information.txt             (File containing additional information on the camera setup)
```

## Camera setup files

The `cameras.txt` and `images.txt` files are used by $TEMP-PROJECT$ to store and fetch the parameters of the camera setup.

These files are formatted to follow COLMAP's file structure, so as to more easily work with this external tool. For information on their content, we therefore redirect viewers to [the corresponding section](https://colmap.github.io/format.html#cameras-txt) of COLMAP's documentation website.

## Other information text files

The `processing_information.txt` and `additional_information.txt` files are created during processing, and are required for rendering.

The first specifies which assets have already been processed, and whether the processed data has already been bundled.

The second specifies additional rendering parameters, such as the initial position in which the viewer should be placed when launching play mode.

Both files are created automatically during processing. They should not be modified manually.

* * *
* * *

## FAQ
{: .d-inline-block }
Frequently asked questions
{: .label .label-blue }

### The position and orientation parameters stored in the images.txt file do not match the setup displayed in the Unity scene view, is this normal?

Yes, the coordinate systems of COLMAP and Unity do not share the same conventions, so an operation has to be performed to convert from one to the other. The positions and orientations stored in the `images.txt` file match COLMAP's coordinate system. They are converted to Unity's coordinate system when the project reads the file to get these parameters.
