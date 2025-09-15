---
title: Induction Heads, 2022
draft: false
tags:
  - ai_safety
  - mech_interp
---

Link: https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html

Given a sentence:
> **Jack** and **Jill** went up the hill. **Jack** gave some water to ...

We want the model to predict the token "Jill".

We can generalise this sentence structure in the form (A)(B) ... (A) -> predict (B). When a two names A and B are seen in close proximity together, it makes sense that the model should predict B when A is mentioned followed by a conjunction indicating a relationship between two people. 

[Elhage et al ](https://transformer-circuits.pub/2021/framework/index.html) discovered the existence of induction heads, circuits that predict (B) when (A) precedes it to "complete the pattern".

More on the structure of induction heads:
- Induction heads in their toy model (2 layer attention-only) are a circuit of two attention heads. The first head tells you the answer to "what is the previous token?". The second head, which does most of the induction work, uses information from the first head to find tokens preceded by the present token (thus returning B).
	- This means that induction heads show up in minimum 2-layer transformers. 
- Elhage et al were able to show that induction heads implement a pattern copying behaviour and appear to be the primary source of in-context learning. 

The paper presents six lines of evidence as to why **induction heads many be the mechanistic source of general in-context learning in transformers of any size**. I think that this is a big (circumstantial) claim to made, and their arguments serve to supplement this idea. I am personally quite convinced by this, at least in smaller models (see the paper's section on direct ablation and co-occurence). 