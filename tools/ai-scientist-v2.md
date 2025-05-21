---
date: 2025-04-14
time: 23:20
author: 
title: "The AI Scientist-v2: Workshop-Level Automated Scientific Discovery via Agentic Tree Search"
created-date: 2025-05-04
tags: 
paper: https://arxiv.org/abs/2504.08066
code: https://github.com/SakanaAI/AI-Scientist-v2
zks-type: lit
---
==draft==

The system iteratively formulates hypotheses, designs and executes experiments, analyzes data, visualizes results, and writes scientific manuscripts.

## Description of result
- submit 3 AI-generated papers to the ICBINB Workshop at ICLR 2025, 1 accept (avg reviewer score 6.33, top ~45% of submissions)
	- authors chose to withdraw upon acceptance
	- reviewers were informed that they might receive an AI generated paper.
	- first time an end-to-end generated paper is accepted for workshop
		- caveat: some steps still require human filtering
	- caveat: this workshop is for negative results (good idea, but results are worse than expected)

---
## How it compares to previous work
![](assets/Pasted%20image%2020250504233159.png)

* **Elimination of reliance on human-authored code templates**: V1 relied heavily on human-crafted templates for each new topic area, requiring manual effort. V2 removes this dependency, significantly increasing autonomy and allowing out-of-the-box deployment across multiple machine learning domains.

---
## Main strategies used to obtain results
![](assets/Pasted%20image%2020250504233213.png)
### Node types
- task type
	- hyperparam
	- ablation
	- replication
	- aggregation
- properties
	- best
	- non-buggy
	- buggy
![](assets/Pasted%20image%2020250504233238.png)


*   **Agentic Tree Search and Experiment Management**: A novel progressive agentic tree-search methodology, managed by a dedicated experiment manager agent, guides the experimentation process across four main stages: Preliminary Investigation, Hyperparameter Tuning, Research Agenda Execution, and Ablation Studies. An LLM evaluates nodes to select the best-performing ones to seed subsequent stages.
*   **Parallel Experiment Execution**: Multiple selected nodes from the tree are executed concurrently in parallel, significantly accelerating the exploration process.
*   **Vision-Language Model (VLM) Integration**: VLMs are incorporated at two phases: during the tree-based experimentation to provide immediate feedback on generated figures, and during the manuscript writing reflection stage to evaluate figures, captions, and text for clarity, coherence, and alignment. VLM feedback is used to identify buggy nodes during experimentation.
*   **Autonomous Code Generation**: The system generates and refines experiment code via the agentic tree search, eliminating the need for human-authored code templates used in v1.
*   **Streamlined Manuscript Writing**: V2 replaces the incremental writing approach of v1 with a simpler single-pass generation followed by a separate reflection stage, powered by reasoning models. The system is prompted to adhere to submission guidelines, such as page limits.
*   **Data Handling**: The system is prompted to leverage Hugging Face Hub for dataset loading whenever possible. Experimental outputs are saved into structured files for analysis and visualization.

The overall process for generating a single paper typically takes several hours, up to a set limit of 15 hours.

---

## Other
- challenges
	- still hallucinates

- Apparently reasoning models make a diff? (learnt about this from live ppt)