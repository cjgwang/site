---
title: Progress Measures for Grokking via Mechanistic Interpretability
draft: true
tags:
  - ai_safety
---
Cath wants to say: *I think this paper is maybe not worth reading completely, since it was optimised for ICLR. I find some parts a bit wordy and I focus more on the mathematical framework.*

Link: https://arxiv.org/pdf/2301.05217

Paper abstract: (...)We argue that progress measures can be found via mechanistic interpretability: reverseengineering learned behaviors into their individual components. As a case study, we investigate the recently-discovered phenomenon of “grokking” exhibited by small transformers trained on modular addition tasks. We fully reverse engineer the algorithm learned by these networks, which uses discrete Fourier transforms and trigonometric identities to convert addition to rotation about a circle. We confirm the algorithm by analyzing the activations and weights and by performing ablations in Fourier space. Based on this understanding, we define progress measures that allow us to study the dynamics of training and split training into three continuous phases: memorization, circuit formation, and cleanup. Our results show that grokking, rather than being a sudden shift, arises from the gradual amplification of structured mechanisms encoded in the weights, followed by the later removal of memorizing components.

### Introduction
- This paper tries to tackle the problem of abrupt emergence of reward hacking and other phase transitions due to scaling through finding hidden progress measures which are less abrupt. A measure that already exists is cross-entropy loss. 
- We can use mechanistic interpretability (reverse engineer the circuits of a network by identifying circuits within a model that implement a specific behaviour) to uncover hidden progress measures. 
- Nanda et al study the problem of grokking, where models transition from overfitting for a large number of training steps to generalisation abruptly.
	- Specifically, modular addition, where the model takes inputs a, b ∈ {0, . . . , P −1}  for some prime P and predicts their sum c mod P. 
	- Small transformers trained with weight decay consistently exhibit grokking. 
 ![[Screenshot 2025-07-10 at 16.42.07.png]]
Grokking

A one-layer transformer implementing a modular addition algorithm.
![[Screenshot 2025-07-10 at 16.31.29.png]]

- Through mech interp, Nanda et al find that the one-layer transformer maps the inputs onto a circle and performs modular addition on the circle. The embedding matrix maps a, b to sines and cosines at a sparse set of frequencies w. Then, the attention and MLP layers combing them and compute w(a+b), and the output matrices shift and combine these frequencies. 
- Thus, Nanda et al construct two progress measures for modular addition, which improve continuously even prior to grokking.
	- Restricted loss is where we ablate all non-key frequencies.
	- Excluded loss is where we ablate all key frequencies.
- Conclusion: training is split into 3 phases: memorisation of training data, circuit formation, and clean-up (weight decay removes memory). The transition to generalisation happens during cleanup, after the generalising mechanism is learned. 
#### Set up