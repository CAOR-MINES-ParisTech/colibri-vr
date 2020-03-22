---
layout: default
title: Evaluation methods
permalink: /structural-elements/evaluation-methods
parent: Structural elements
nav_order: 5
---

# Evaluation methods

* * *

## Overview

In order to evaluate the quality of a rendering solution, one typically compares, for each image in multiple datasets, the view rendered in the source camera's position with the original image (the source image itself being excluded for rendering). This comparison is typically quantified using per-pixel error metrics.

Work-in-progress
{: .label .label-yellow }
- COLIBRI VR does not yet enable obtaining a quantitative evaluation value for a given rendering solution, that would be obtained as an average value over multiple datasets (e.g. virtual rephotography, see <a href="#waechter2017">[Waechter et al. 2017]</a>). The project currently implements evaluation metrics for visualization purposes only.

## Cb+Cr

The `Cb+Cr` error metric is computed in each pixel as the sum of absolute differences, for the Cb and Cr channels in the YCbCr color space, of the source and rendered view's color values. For more information, see <a href="#waechter2017">[Waechter et al. 2017]</a>.

<p align="center">
      <img src="https://github.com/caor-mines-paristech/colibri-vr/raw/master/docs/illustrations/PyriteEval.png" alt="" width="480" height="360"><br><i>Evaluation is performed by comparing the original images and the corresponding rendered views. In this illustration, differences are computed using the Cb+Cr metric, and visualized with the plasma colormap.</i>
</p>

* * *
* * *

## References
{: .d-inline-block }
References
{: .label .label-purple }

<a name="waechter2017">[Waechter et al. 2017]</a> M. Waechter, M. Beljan, S. Fuhrmann, N. Moehrle, J. Kopf, and M. Goesele. *Virtual Rephotography: Novel View Prediction Error for 3D Reconstruction.* ACM Transactions on Graphics, 36(4):1, Jan. 2017. doi: [10.1145/3072959.2999533](https://doi.org/10.1145/3072959.2999533)
