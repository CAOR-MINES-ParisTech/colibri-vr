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

<p align="center">
   <iframe width="720" height="405" src="https://www.youtube.com/embed/HtJarul_32c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe><br>
   Watch the project video: <a href="https://youtu.be/HtJarul_32c">on YouTube</a>
</p>

## About

COLIBRI VR is the Core Open Lab on Image-Based Rendering Innovation for Virtual Reality. It is an open resource with a graphical user interface that aims to enable researchers to easily use and develop image-based rendering techniques for virtual reality. It is currently being developed as a package for the Unity game engine.

## Citation

The toolkit was developed by [Grégoire Dupont de Dinechin](http://greg3dinechin.com) during his PhD at [MINES ParisTech, PSL University](http://www.mines-paristech.eu/) under the supervision of [Alexis Paljic](https://www.researchgate.net/profile/Alexis_Paljic). If you use COLIBRI VR, please cite the original paper that introduces the toolkit, presented at the [Workshop on Everyday Virtual Reality (WEVR)](https://wevr.adalsimeone.me/program2020) of the [IEEE VR 2020](http://ieeevr.org/2020/) conference:

```
@inproceedings{DinechinPaljic2020Real,
        title = {From Real to Virtual: An Image-Based Rendering Toolkit to Help Bring the World Around Us Into Virtual Reality},
        doi = {10.1109/VRW50115.2020.00076},
        booktitle = {2020 {IEEE} Conference on Virtual Reality and {3D} User Interfaces Abstracts and Workshops ({VRW})},
        author = {Dinechin, Gr{\'e}goire Dupont de and Paljic, Alexis},
        month = mar,
        year = {2020}
}
```

This project was also presented during the conference's main event by way of a poster, video submission, and research demonstration. The complete list of publications related to COLIBRI VR can be found [here](http://greg3dinechin.com/publications).

## Contributors

<!---
<ul class="list-style-none">
{% for contributor in site.github.contributors %}
  <li class="d-inline-block mr-1">
     <a href="{{ contributor.html_url }}"><img src="{{ contributor.avatar_url }}" width="32" height="32" alt="{{ contributor.login }}"/></a>
  </li>
{% endfor %}
</ul>
-->

<script src="//code.jquery.com/jquery-3.2.1.min.js"></script>
<div id="contributors_json"></div>
<script>
    $().ready(function(){
        $.getJSON("https://api.github.com/repos/CAOR-MINES-ParisTech/colibri-vr-unity-package/contributors", function(data) {
              var items = [];
              $.each( data, function( key, val ) {
                items.push("<li class=\"d-inline-block mr-1\"><a href=\"" + val["html_url"] + "\"><img src=\"" + val["avatar_url"] + "\" width=\"32\" height=\"32\" alt=\"" + val["login"] + "\"/></a></li>");
              });
              $( "<ul/>", {
                "class": "list-style-none",
                html: items.join("")
              }).appendTo("#contributors_json");
      });
    });
</script>

## License

The project is released under an [MIT license](https://github.com/caor-mines-paristech/colibri-vr-unity-package/blob/master/LICENSE.md).

## Documentation overview

Here are the different elements you can find on this documentation website:

- The [Getting started](https://caor-mines-paristech.github.io/colibri-vr/getting-started) pages help you get started with the toolkit, showing how to install it and describing the graphical user interface.
- The [Structural elements](https://caor-mines-paristech.github.io/colibri-vr/structural-elements) pages describe the concepts on which the project relies, and how they are implemented into practical structures and models.
- The [Core components](https://caor-mines-paristech.github.io/colibri-vr/core-components) pages contain detailed information on the components implemented in the project, and can thus help better use the related graphical user interfaces.
- The [Shader implementations](https://caor-mines-paristech.github.io/colibri-vr/shader-implementations) pages describe the vertex/fragment and compute shader implementations of several processing and rendering methods.
- The [Datasets](https://caor-mines-paristech.github.io/colibri-vr/datasets) page provides a list of online image datasets on which the project can be tested.
- The [Forum](https://caor-mines-paristech.github.io/colibri-vr/faq) page provides information on the related web forum.
- The [FAQ](https://caor-mines-paristech.github.io/colibri-vr/faq) page answers frequently asked questions.

