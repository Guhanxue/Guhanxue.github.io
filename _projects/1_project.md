---
layout: page
title: Foundation Models for Medical Imaging
description: Building and fine-tuning vision foundation models for clinical imaging tasks.
img: assets/img/publication_preview/MRI-core.png
importance: 1
category: work
related_publications: true
---

We develop and benchmark foundation models tailored for medical imaging tasks. Our work spans:

- **General-purpose segmentation models** like [SegmentAnyBone](https://github.com/mazurowski-lab/SegmentAnyBone) and [SegmentAnyMuscle](https://github.com/mazurowski-lab/SegmentAnyMuscle), adapted from SAM.
- **MRI-specific encoders**, such as [MRI-CORE](https://github.com/mazurowski-lab/mri_foundation), self-supervised trained on 116,806 volumes.
- **Zero-shot and cross-modality generalization**, evaluating foundation models in zero-shot segmentation and registration tasks.

Our models aim to reduce annotation cost and improve generalizability in real-world clinical settings.

<div class="row">
    <div class="col-sm mt-3">
        {% include figure.liquid path="assets/img/publication_preview/WholeBody_dataset.png" title="SegmentAnyBone Overview" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3">
        {% include figure.liquid path="assets/img/publication_preview/MRI-core.png" title="MRI-CORE, self-supervised MRI foundation model" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="caption">
    Left: Bone segmentation in knee MRI. Right: Multi-sequence MRI model using MRI-CORE.
</div>
