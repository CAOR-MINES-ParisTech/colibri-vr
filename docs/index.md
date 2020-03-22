---
layout: default
title: Home
permalink: /
nav_order: 1
---

# COLIBRI VR
{: .fs-9 }

## An Open-Source Toolkit to Render Real-World Scenes in Virtual Reality
{: .fs-6 .fw-300 }

Latest project version: 1.0 <br>
Latest release date: on Github since March 2020 <br>
For Unity versions: 2019.2.15f1 or higher
{: .text-grey-dk-000 .fs-5 .fw-300 }

[COLIBRI VR on GitHub](https://github.com/caor-mines-paristech/colibri-vr-unity-package/){: .btn .btn-blue }
[COLIBRI VR on the Unity Asset Store](https://assetstore.unity.com/){: .btn .btn-green }

## News
{: .d-inline-block }
New
{: .label .label-green }

- We'll be presenting this project live today (March 22) during the WEVR workshop of the IEEE VR 2020 conference! The Twitch stream is available to everyone: [https://www.twitch.tv/ieeevr2020_wevr](https://www.twitch.tv/ieeevr2020_wevr). We'll be presenting from 4:15PM to 4:30PM Atlanta time (UTC-4).

- You can now join our COLIBRI VR [web forum](https://groups.google.com/forum/#!forum/colibri-vr) to ask questions about COLIBRI VR, report bugs, or request features! More generally this will be a good place to discuss subjects related to image-based virtual reality and image-based rendering.

## Important note
{: .d-inline-block }
Important
{: .label .label-red }

COLIBRI VR is not yet available on the Unity Asset Store, and tutorial videos still have to be uploaded. Expected time of arrival for these features: end of March 2020. We recommend waiting for these steps to be completed before using the project: nonetheless, for those wanting to try out the current version, we have already made the source code acessible [via GitHub](https://github.com/caor-mines-paristech/colibri-vr-unity-package/), from which it can be loaded as a Unity package.

* * *

<p align="center">
   <a href="https://www.youtube.com/watch?feature=player_embedded&v=HtJarul_32c" target="_blank"><img src="https://github.com/caor-mines-paristech/colibri-vr/raw/master/docs/illustrations/thumbnail.png" alt="" width="600" height="600" /></a><br><i>Watch the project video: <a href="https://youtu.be/HtJarul_32c">on YouTube</a></i>
</p>

## About

COLIBRI VR is the Core Open Lab on Image-Based Rendering Innovation for Virtual Reality. It is an open resource with a graphical user interface that aims to enable researchers to easily use and develop image-based rendering techniques for virtual reality. It is currently being developed as a package for the Unity game engine.

## Citation

The toolkit was developed by [Grégoire Dupont de Dinechin](http://greg3dinechin.com) during his PhD at [MINES ParisTech, PSL University](http://www.mines-paristech.eu/) under the supervision of [Alexis Paljic](https://www.researchgate.net/profile/Alexis_Paljic). If you use COLIBRI VR, please cite the following [WEVR 2020](https://wevr.adalsimeone.me/program2020) paper:

```
@inproceedings{deDinechinPaljic2020From,
        title = {From Real to Virtual: An Image-Based Rendering Toolkit to Help Bring the World Around Us Into Virtual Reality},
        booktitle = {6th Workshop on Everyday Virtual Reality ({WEVR})},
        publisher = { {IEEE} },
        author = {Gr{\'e}goire Dupont de Dinechin and Alexis Paljic},
        month = mar,
        year = {2020}
} 
```

This project was also presented at the [IEEE VR 2020](http://ieeevr.org/2020/) conference by way of a poster, video submission, and research demonstration. The complete list of related publications can be found [here](http://greg3dinechin.com/publications).

## Contributors

<ul class="list-style-none">
{% for contributor in site.github.contributors %}
  <li class="d-inline-block mr-1">
     <a href="{{ contributor.html_url }}"><img src="{{ contributor.avatar_url }}" width="32" height="32" alt="{{ contributor.login }}"/></a>
  </li>
{% endfor %}
</ul>

## License

The project is released under an [MIT license](https://github.com/caor-mines-paristech/colibri-vr-unity-package/blob/master/LICENSE.md).

## Documentation overview

Here are the different elements you can find on this documentation website:

- The [Getting started](https://caor-mines-paristech.github.io/colibri-vr/getting-started) pages help you get started with the toolkit, showing how to install it and describing the graphical user interface.
- The [Structural elements](https://caor-mines-paristech.github.io/colibri-vr/structural-elements) pages describe the concepts on which the project relies, and how they are implemented into practical structures and models.
- The [Core components](https://caor-mines-paristech.github.io/colibri-vr/core-components) pages contain detailed information on the components implemented in the project, and can thus help better use the related graphical user interfaces.
- The [Shader implementations](https://caor-mines-paristech.github.io/colibri-vr/shader-implementations) pages describe the vertex/fragment and compute shader implementations of several processing and rendering methods.
- The [Datasets](https://caor-mines-paristech.github.io/colibri-vr/datasets) page provides a list of online image datasets on which the project can be tested.
- The [FAQ](https://caor-mines-paristech.github.io/colibri-vr/faq) page answers frequently asked questions.

