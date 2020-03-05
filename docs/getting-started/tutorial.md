---
layout: default
title: Tutorial
permalink: /getting-started/tutorial
parent: Getting started
nav_order: 2
---

# Tutorial

* * *

## Objectives

The goal of this tutorial is to help you use COLIBRI VR to render view-dependent rendering effects in VR in Unity from a sample set of photographs.

## Prerequisites

Before reading the rest of this tutorial, please ensure that you have already performed the following steps:

1. You have installed COLIBRI VR and imported it into a new Unity project. For help on this step, follow the instructions on the [Installation](https://caor-mines-paristech.github.io/colibri-vr/getting-started/installation/) page, including the instructions to install the external tools COLMAP and Blender.

2. You have set up your input photographs in a folder as defined by the file structure shown below (see the [File structure](https://caor-mines-paristech.github.io/colibri-vr/structural-elements/file-structure) page for more details). These photographs can have been captured by yourself, downloaded from an online image dataset (see the [Datasets](https://caor-mines-paristech.github.io/colibri-vr/datasets) page), or captured from a synthetic scene using the toolkit's dedicated tool (see the [Acquisition](https://caor-mines-paristech.github.io/colibri-vr/core-components/acquisition) page).
```
── Unity project              (Folder containing the Unity project)
      └─── Data                  (Folder containing the datasets used by the Unity project)
           └─── Dataset          (Folder containing the data for a given source dataset)
                └─── images      (Folder, to be called "images", containing the photographs)
```

## Step-by-step

Here is an overview of the steps examined in this tutorial:
- *Steps A-B:* Using the [Processing](https://caor-mines-paristech.github.io/colibri-vr/core-components/processing) component to transform the source photographs into a 3D scene representation.
- *Steps Y-Z:* Using the [Rendering](https://caor-mines-paristech.github.io/colibri-vr/core-components/rendering) component to render the representation in VR with view-dependent highlights.

**TODO: This section is not yet complete. Tutorial videos should be coming soon.**
