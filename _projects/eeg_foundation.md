---
layout: page
title: "Foundation Model for EEG"
description: "Bachelor’s Thesis at ETH Zürich (DISCO Lab, Prof. Roger Wattenhofer)"
img: /assets/eeg-foundation/concept.jpg
importance: 2
category: research
---

## Overview
For my bachelor's thesis, we ([Ard](https://www.linkedin.com/in/ard-kastrati/) and I) explored the pre-training of a **foundation model for EEG data**, motivated by the success of such models in the language and vision domains. The central idea was to leverage large-scale EEG datasets such as the TUH EEG Corpus [1] for self-supervised pretraining, followed by fine-tuning for diverse downstream tasks:

- **Brain–Computer Interfaces (BCI):** e.g., classifying left vs. right hand motor imagery  
- **Clinical Applications:** e.g., detecting Alzheimer’s, Parkinson’s, depression

## Background

Our approach was inspired by the **Audio-MAE** framework from Meta AI [2], which demonstrated how masked autoencoders (MAEs) can be applied to spectrogram representations of audio. EEG shares key properties with audio, making this a natural fit (signals are continuous, possibly multi-channel, and rich in spectral information).

{% include figure.liquid path="/assets/eeg-foundation/audio-mae.jpg" title="Audio-MAE Architecture (Huang et al., 2023)" class="img-fluid rounded z-depth-1 d-block mx-auto" width="80%" %}
<div class="caption text-center">
  Key idea of Audio-MAE (Huang et al., 2023)
</div>

The Audio-MAE method converts raw waveforms into spectrograms, divides them into fixed-size patches, and applies heavy masking. Only the visible patches are passed through a transformer encoder, while a lightweight decoder reconstructs the missing ones. This process reduces computational cost while producing robust self-supervised representations.

## Results

Our thesis was guided by two primary objectives:

- **Framework efficiency:** to develop a flexible architecture for heterogeneous EEG inputs, and  
- **Compute efficiency:** to ensure feasible large-scale training on the group's multi-GPU cluster.

### Flexible Model

A key challenge was designing a model capable of handling the substantial variability in EEG recordings, including differences in duration and electrode configurations. Prior models [3,4,5,6] were typically limited to specific subsets of EEG data, so the main part of my research was to come up with a flexible architecture that could adapt to our large dataset.

An overview of the main techniques is shown here:

{% include figure.liquid path="/assets/eeg-foundation/flexible_architecture.jpg" title="Flexible Architecture for Heterogeneous EEG Inputs" class="img-fluid rounded z-depth-1 d-block mx-auto" width="80%" %}
<div class="caption text-center">
  Architectural Tricks to Accomodate Diverse Input Data
</div>

### Feasible Training

On the computational front, optimizing training efficiency was critical given the scale of data (>2 TB) and model complexity. We employed profiling using the PyTorch Profiler to analyze GPU utilization and occupancy across multiple hardware configurations. This enabled targeted code refinements for optimized CUDA performance. Additionally, we performed experiments on data loading strategies (local versus network storage), batch size scaling, and multi-GPU training to maximize throughput. Finally, we also employed comparative benchmarking across different GPU types that provided more general insights into the cluster's performance and was shared with the group.

## Outlook

The main remaining challenge was to carry out long-duration pretraining runs on large models and the full EEG corpus, which other students took on after me. I was awarded grade 6/6.

---

## References:
[1] I. Obeid and J. Picone, “The temple university hospital eeg data corpus,” [Frontiers in Neuroscience, vol. 10, 2016](https://www.frontiersin.org/journals/neuroscience/articles/10.3389/fnins.2016.00196).

[2] Huang, P.-Y., Xu, H., Li, J., Baevski, A., Auli, M., Galuba, W., Metze, F., & Feichtenhofer, C. (2023). *Masked Autoencoders that Listen.* [arXiv:2207.06405](https://arxiv.org/abs/2207.06405). 

[3] D. Kostas, S. Aroca-Ouellette, and F. Rudzicz, “Bendr: Using transformers
and a contrastive self-supervised learning task to learn from massive amounts
of eeg data,” [Frontiers in Human Neuroscience, vol. 15, 2021](https://www.frontiersin.org/articles/10.3389/fnhum.2021.653659).

[4] D. Wu, S. Li, J. Yang, and M. Sawan, “neuro2vec: Masked fourier spectrum
prediction for neurophysiological representation learning,” [2022](https://ar5iv.labs.arxiv.org/html/2204.12440).

[5] W. Cui, W. Jeong, P. Thölke, T. Medani, K. Jerbi, A. A. Joshi, and R. M.
Leahy, “Neuro-gpt: Towards a foundation model for eeg,” [2024](https://arxiv.org/abs/2311.03764).

[6] W.-B. Jiang, L.-M. Zhao, and B.-L. Lu, “Large brain model for learning
generic representations with tremendous eeg data in bci,” [2024](https://arxiv.org/abs/2405.18765).