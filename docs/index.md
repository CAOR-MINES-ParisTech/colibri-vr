---
layout: default
title: Home
permalink: /
nav_order: 1
---

# $TEMP-PROJECT$
{: .fs-9 }

## $TEMP-PROJECT-SUBHEADER$
{: .fs-6 .fw-300 }

Latest project version: 0.0 <br>
Latest release date: not yet released <br>
For Unity versions: 2019.2.15f1 or higher
{: .text-grey-dk-000 .fs-5 .fw-300 }

[$TEMP-PROJECT$ on GitHub](https://github.com/DinechinGreg/temp-project/){: .btn .btn-blue }
[$TEMP-PROJECT$ on the Unity Asset Store](https://assetstore.unity.com/){: .btn .btn-green }

* * *

<p align="center">
   <a href="https://www.youtube.com/watch?feature=player_embedded&v=aqz-KE-bpKQ" target="_blank"><img src="https://img.youtube.com/vi/aqz-KE-bpKQ/0.jpg" alt="Project video" width="640" height="480" border="10" /></a><br><i>Watch the project video: <a href="https://youtu.be/aqz-KE-bpKQ">on YouTube</a></i>
</p>

## About

$TEMP-PROJECT$ is the $TEMP-PROJECT-ACRONYM-EXPLAINER$. It is an open resource with a graphical user interface that aims to enable researchers to easily use and develop image-based rendering techniques for virtual reality. It is currently being developed as a package for the Unity game engine.

## Citation

The toolkit was developed by [Grégoire Dupont de Dinechin](http://greg3dinechin.com) during his PhD at [MINES ParisTech, PSL University](http://www.mines-paristech.eu/) under the supervision of [Alexis Paljic](https://www.researchgate.net/profile/Alexis_Paljic). If you use $TEMP-PROJECT$, please cite the following paper:

```
@inproceedings{deDinechinPaljic2020TEMP,
 author = {Gr{\'e}goire Dupont de Dinechin and Alexis Paljic},
 title = {$TEMP-PROJECT$}
} 
```

## Contributors

<ul class="list-style-none">
{% for contributor in site.github.contributors %}
  <li class="d-inline-block mr-1">
     <a href="{{ contributor.html_url }}"><img src="{{ contributor.avatar_url }}" width="32" height="32" alt="{{ contributor.login }}"/></a>
  </li>
{% endfor %}
</ul>

## License

The project is released under an [MIT license](https://github.com/DinechinGreg/temp-project/blob/master/LICENSE).

## Documentation overview

Here are the different elements you can find on this documentation website:

- The [Getting started](https://dinechingreg.github.io/temp-project/getting-started) pages help you get started with the toolkit, showing how to install it and describing the graphical user interface.
- The [Structural elements](https://dinechingreg.github.io/temp-project/structural-elements) pages describe the concepts on which the project relies, and how they are implemented into practical structures and models.
- The [Core components](https://dinechingreg.github.io/temp-project/core-components) pages contain detailed information on the components implemented in the project, and can thus help better use the related graphical user interfaces.
- The [Shader implementations](https://dinechingreg.github.io/temp-project/shader-implementations) pages describe the vertex/fragment and compute shader implementations of several processing and rendering methods.
- The [Datasets](https://dinechingreg.github.io/temp-project/datasets) page provides a list of online image datasets on which the project can be tested.
- The [FAQ](https://dinechingreg.github.io/temp-project/faq) page answers frequently asked questions.

## News
{: .d-inline-block }
New
{: .label .label-green }

Still working on the documentation. The package is almost done, should be uploaded to the asset store soon!
