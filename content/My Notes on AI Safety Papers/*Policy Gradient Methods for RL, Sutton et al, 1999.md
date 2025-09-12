---
title: Policy Gradient Methods for RL, Sutton et al, 1999
draft: true
tags:
  - ai_safety
  - RL
---
Abstract: Function approximation is essential to reinforcement learning, but the standard approach of approximating a value function and determining a policy from it has so far proven theoretically intractable. In this paper we explore an alternative approach in which the policy is explicitly represented by its own function approximator, independent of the value function, and is updated according to the gradient of expected reward with respect to the policy parameters. Williams's REINFORCE method and actor-critic methods are examples of this approach. Our main new result is to show that the gradient can be written in a form suitable for estimation from experience aided by an approximate action-value or advantage function. Using this result, we prove for the first time that a version of policy iteration with arbitrary differentiable function approximation is convergent to a locally optimal policy.

Link: https://proceedings.neurips.cc/paper_files/paper/1999/file/464d828b85b0bed98e80ade0a5c43b0f-Paper.pdf

### Stochastic policy approaches
- Value-function approaches such as Q-Learning and SARSA are sometimes unable to converge
- Value-function approaches are deterministic, whereas the optimal policy is often stochastic. 
- Expected value approaches mean that arbitrarily small changes in the expected value of an action can cause it to be selected/deselected. 
Sutton et al introduce a stochastic policy using an independent function approximator with its own parameters.
Let the policy be decided by a NN whose input is state and outputs action selection probabilities. The NN then updates its weights, which are the policy parameters. 


Policy parameter update:
![[Screenshot 2025-07-17 at 15.50.49.png]]
Where theta is the vector of policy parameters, roe is performance (e.g. avg reward per step), and alpha is step size. 

Thus, small changes in policy parameters do not change your policy by much. 