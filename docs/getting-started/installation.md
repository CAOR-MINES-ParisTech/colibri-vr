---
layout: default
title: Installation
permalink: /getting-started/installation
parent: Getting started
nav_order: 1
---

# Installation

* * *

## Required steps

1. Install the [Unity game engine](https://unity.com/).
2. Use the Unity package manager to add the package from COLIBRI VR's [Git page](https://github.com/caor-mines-paristech/colibri-vr-unity-package/). If you do not have Git, you can simply download the package from Git and manually add it into Unity using the package manager.

## Optional steps: linked external tools

Using the toolkit's graphical user interface, several external tools can be used from within Unity as part of COLIBRI VR's processing pipeline (see [this section](https://caor-mines-paristech.github.io/colibri-vr/core-components/processing#external-processing-helpers) of the Processing page for more details). These tools have to be installed separately. For simplicity, we recommend downloading the pre-built binaries.

- To perform sparse and dense 3D reconstruction from photographs:<br/>
Install [COLMAP](https://colmap.github.io/).

- To convert mesh file formats and perform mesh simplification:<br/>
Install [Blender](https://www.blender.org/).

- To apply mesh retopology methods:<br/>
Install [Instant Meshes](https://github.com/wjakob/instant-meshes).

* * * 
{: .bg-blue-300 }
* * * 

## FAQ
{: .d-inline-block }
Frequently asked questions
{: .label .label-blue }

### Can I run COLIBRI VR on any operating system?

COLIBRI VR should work on any operating system supported by the Unity game engine, and the linked external tools provide binaries for Windows, Mac OS X, and Linux. That being said, we have only tested the project on Windows 10, so feel free to provide feedback on this matter.

### Do I need a special setup to run COLIBRI VR?

A CUDA-enabled GPU is required if you wish to perform dense reconstruction via COLMAP, but is not necessary otherwise. 

Additionally, it is important to note that the processing/rendering pipeline is often performance-intensive in terms of GPU memory. Make sure to monitor memory during troubleshooting.

### Is the project affiliated with any or all of the linked external tools?

No, these tools are not affiliated in any way with COLIBRI VR. The word *linked* here simply means that the toolkit implements dedicated classes and interface elements for using these tools from within Unity, by way of underlying command-line calls.
