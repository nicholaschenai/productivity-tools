---
date: 2025-05-21
time: 19:02
author: Roberta Raileanu
title: "Automating Scientific Discovery: How Far Are We? (Roberta Raileanu, Meta)"
created-date: 2025-05-21
tags:
  - ai-scientist
source: https://iclr.cc/virtual/2025/workshop/23987#collapse37268
zks-type: lit
---
- AI makes algo discoveries in constrained domains
	- Funsearch for math https://www.nature.com/articles/s41586-023-06924-6
	- CUDA Kernels https://sakana.ai/ai-cuda-engineer/
	- Preference opt algos https://arxiv.org/abs/2406.08414
- MLGym, sci equivalent of OAI gym
	- https://github.com/facebookresearch/mlgym
	- https://arxiv.org/abs/2502.14499
	- problem setting: algo reasoning, RL, supervised learning, SSL
	- domains: DS, CV, NLP, RL, CS, Game theory
- agents seem to be able to reason about hyperparam n NN architectures
- Current limitations: can hill climb (incremental improvement), but not breakthru ideas
- AIDE: AI-Driven Exploration in the Space of Code https://arxiv.org/abs/2502.13138
	- good agentic scaffolds can significantly improve performance
	- humans still produce better research given enough time
- Can LLMs Generate Novel Research Ideas? A Large-Scale Human Study with 100+ NLP Researchers https://arxiv.org/abs/2409.04109
- Sparks of Science: Hypothesis Generation Using Structured Paper Data https://arxiv.org/abs/2504.12976
	- "HypoGen, the first dataset of approximately 5500 structured problem-hypothesis pairs extracted from top-tier computer science conferences" ... and extract the insights behind the papers
	- ft a model based on this
	- LLMs are still significantly worse than humans at hypothesis generation
- evaluation
	- RE bench https://arxiv.org/abs/2411.15114
	- MLE bench
	- CORE-Bench
	- SciReplicate-Bench
	- PaperBench
- Problems (for both humans and AI): 
	- hard to tell what is good research over long run -- ref "Why Greatness Cannot Be Planned: The Myth of the Objective"
	- what problems to solve?
	- when to give up on an idea?
	- how to evaluate AI-assisted human or Human-AI scientist team?
- Summary: How far are we from automating scientific discovery?
	- cannot gen truly innovative/feasible/useful ideas
	- dont know what probs to solve
	- dont know when to persist or give up
	- cannot solve complex open research probs
	- cannot make progress over extended periods of time
	- cannot autonomously make a breakthru discovery
