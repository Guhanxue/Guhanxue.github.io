---
layout: page
title: Techniques for Medical Imaging Analysis
description: Efficient, adaptable deep learning tools for robust image analysis.
img: assets/img/publication_preview/finetune_strategy_v9.png
importance: 2
category: work
related_publications: true
---

This line of work focuses on pushing the robustness and efficiency of clinical image analysis through:

- **Fine-tuning foundation models** with low-rank adaptation (LoRA), adapters, and self-supervised learning ([Finetune-SAM](https://github.com/mazurowski-lab/finetune-SAM)).
- **Annotation-efficient learning** [Accelerating Volumetric Medical Image Annotation via Short-Long Memory SAM 2](https://arxiv.org/abs/2505.01854).
- **Domain shifts evaluation and OOD detection** [Fréchet Radiomic Distance (FRD): A Versatile Metric for Comparing Medical Imaging Datasets](https://arxiv.org/abs/2412.01496).
- **Test-time adaptation** for robustness to distribution shift ([InTEnt](https://openaccess.thecvf.com/content/CVPR2024W/DEF-AI-MIA/html/Dong_Medical_Image_Segmentation_with_InTEnt_Integrated_Entropy_Weighting_for_Single_CVPRW_2024_paper.html)).
- **Diffusion and generative models** for synthesis and augmentation ([Contour-diff](https://scholar.google.com/citations?view_op=view_citation&hl=en&user=aGjCpQUAAAAJ&citation_for_view=aGjCpQUAAAAJ:hqOjcs7Dif8C)).
- **2D to 3D reconstruction** for reconstruct high-resolution 3D object from 2D images, like 2D Xrays ([Fracture reconstruction](https://scholar.google.com/citations?view_op=view_citation&hl=en&user=aGjCpQUAAAAJ&cstart=20&pagesize=80&sortby=pubdate&citation_for_view=aGjCpQUAAAAJ:LkGwnXOMwfcC)), 2D MRIs ([SuperMask](https://proceedings.mlr.press/v227/gu24b.html)).
- **Registration algorithms** for breast registration, like [GuidedMorph](https://arxiv.org/abs/2505.13414).

These techniques enhance both performance and usability in clinical environments.

{% raw %}

<div class="row">
    <div class="col-sm mt-3">
        {% include figure.liquid path="assets/img/publication_preview/TTA.png" title="Test-time adaptation" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3">
        {% include figure.liquid path="assets/img/publication_preview/contour-diff.png" title="Diffusion synthesis" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="caption">
    Left: On-the-fly model adaptation. Right: Synthetic anatomy using generative models.
</div>
{% endraw %}
