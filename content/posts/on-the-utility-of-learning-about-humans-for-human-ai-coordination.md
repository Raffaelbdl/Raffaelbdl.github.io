---
title: "On the Utility of Learning About Humans for Human Ai Coordination"
date: 2022-10-06T19:40:16+09:00
draft: false
tags: 
- human-ai-coordination
- reinforcement-learning
- beginner-friendly   
---
Paper : http://arxiv.org/abs/1910.05789

The coordination / cooperation between humans and AI can be useful in many applications like robotics or video games. But this task proves to be difficult.

Indeed, when a reinforcement learning agent meets a human it is usually in an adversarial context (chess for instance). Therefore if the human performs poorly, it makes it easier for the agent. Conversely in a cooperation framework, the agent must take into account that the human underperforms.

| ![img1](/resources/paper-explained/overcooked1.png) |
| :-: |
| Figure 1 from the paper, it shows how human underperformance affects the agent both in adversarial and in cooperative gamee |

To address this issue, the authors have decided to introduce two Behavior Cloning (BC) models : one for training and the other one for testing. The goal is to encapsulate a fraction of the human behavior in a policy.

In parallel, they have chosen several reinforcement learning algorithms, in particular those known for their robustness. That is because they suspect that agents trained only by self-play are not confronted to enough game states and therefore do not adapt to a noisy human behavior. The chosen algorithms are PPO (trained in self-play or with the BC agent), PBT (Population Based Training), and classic planification algorithms.

The used environment is a simplification of the Overcooked game. The action space is restrained in order to force cooperation.

| ![img2](/resources/paper-explained/overcooked2.png) |
| :-: |
| Figure 3 from the paper, it shows different layouts of the game, especially some are circular and require a good synchronisation between the two playerse |

The results show that agents trained without a glimpse at human behavior (self-play agents for instance) systematically underperform.

| ![img3](/resources/paper-explained/overcooked3.png) |
| :-: |
| Figure 4 from the paper, the crossed bars correspond to trainings where the original position of the agents are reversed. This is significative in asymmetrical layouts. |

There are a few more points addressed in this paper.

First the agents trained with a BC partner can adapt faster to human actions. They can realised more tasks in a given layout compared to self-play agents that appear to be hyper-specialized. Moreover, agents trained with a BC partner do not tend to impose a behavior to the agent, as the rotation direction in a circular layout.
This make sense since the agent may have to learn how to compensate for the human failures, and therefore can not expect the human to perform however it wants they to.

They also observe that finetuning self-play agents by progressively putting them with more BC partners can help obtain higher results.

They argue that humans possess an ability to adapt to the agent behavior, which the former does not take into account. The authors suggests that training directly on the current human behavior could help.

Ultimately, this kind of study raises the issue of a standardized benchmark. In this paper, the authors asked 40 real human to play with agents. However, it makes the results are not reproductible. Indeed, it is almost impossible to make all the same people join again to test a new algorithm, and they could also have become better in the meantime. The question of a relevant standardized benchmark is thus still open.

| ![img4](/resources/paper-explained/overcooked4.png) |
| :-: |
| Figure 6 from the paper, it shows the performance of the agents when partnered with humans. |