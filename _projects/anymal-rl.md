---
layout: page
title: "RL Fine-Tuning for Quadruped Locomotion (ANYmal)"
description: "Student Project at ETH Zürich\n(RSL Lab, Prof. Marco Hutter)"
img: /assets/anymal-rl/training_concept.jpg   # add a suitable ANYmal image
importance: 1
category: research
tags: [reinforcement learning, locomotion, ANYmal, robotics, ETH Zürich, RSL]
---

## Summary
In this ongoing project at RSL, we ([Clemens](https://www.linkedin.com/in/clemensschwarke/), [Junzhe](https://www.linkedin.com/in/junzhe-he-05aa8022a/), and I) are investigating whether **continued RL fine-tuning** can produce a **universal locomotion policy** for quadruped robots. The goal is to scale a distilled baseline policy to a growing collection of simulated and real-world terrains, and evaluate if and when generalization capabilities begin to plateau. In addition, we are exploring the use of **procedural terrain generation** to create environments that specifically target the weaknesses of the policy.

---

## Background
Previous work at RSL [1] has shown that multi-expert distillation combined with RL fine-tuning can synthesize diverse locomotion skills into a single controller, which was successfully deployed on the ANYmal D robot. The policy was able to traverse rough terrain with strong robustness, as seen in this YouTube video.

<div class="row justify-content-sm-center mb-4">
  <div class="col-sm-10 mt-3 mt-md-0">
    <div class="embed-responsive embed-responsive-16by9">
      <iframe class="embed-responsive-item"
        src="https://www.youtube.com/embed/QDU_FicBPDo"
        title="Parkour in the Wild"
        frameborder="0"
        allowfullscreen>
      </iframe>
    </div>
  </div>
</div>

The way the policy was trained is illustrated below:  
1. **Expert Training:** Nine terrain-specific expert policies were first trained independently using RL, each specialized to a single locomotion skill.  
2. **Distillation:** These experts were then combined into a single network using supervised learning and the DAgger algorithm. At this stage, the distilled policy switched from elevation maps to depth images as input.  
3. **Fine-Tuning:** Finally, the distilled policy was further improved through reinforcement learning on both the original terrains and an extended set of 3D-scanned real-world rubble environments. This enabled robust transfer from simulation to the real robot.

{% include figure.liquid path="/assets/anymal-rl/training_concept.jpg" title="ANYmal locomotion policy from Rudin et al. (2025)" class="img-fluid rounded z-depth-1" %}

Reference:  
[1] Rudin, N., He, J., Aurand, J., & Hutter, M. (2025). *Parkour in the Wild: Learning a General and Extensible Agile Locomotion Policy Using Multi-expert Distillation and RL Fine-tuning.* arXiv:2505.11164.  

---

## Objectives and Outlook

Building on this foundation, **our project explores the scalability of this approach**: how much can continued fine-tuning expand the generalization capacity of the policy? We are incrementally introducing new terrains (for now in simulation) and systematically analyzing when and where generalization begins to plateau. Beyond scaling, we also investigate **procedural terrain generation** as a way to expose policy weaknesses and accelerate robustness, moving toward the long-term goal of a truly generalist locomotion controller.  

- **Scalability:** incrementally fine-tune the policy on a larger and more diverse terrain set.  
- **Plateau Analysis:** systematically evaluate performance to determine where generalization saturates.  
- **Weakness-Directed Training:** explore procedural terrain generation for targeted robustness improvements.  

We hope to gain insights into the requirements for creating more generalist robotic controllers and achieving successful deployment on the ANYmal D robot across increasingly challenging environments. 

