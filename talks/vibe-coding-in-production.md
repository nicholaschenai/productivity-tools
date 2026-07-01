---
date: 2026-07-01
time: 19:02
author:
title:
created-date: 2026-07-01
tags:
source: https://www.youtube.com/watch?v=fHWFF_pnqDk
zks-type: lit
is_public: true
---
## summary
- vibe code definition: forget the code exists (dont need review code)
- why? METR's study of AI can double len of tasks every X months, in the future AI will output code that takes days, weeks, months to write, and we need to learn to vibe to move in lockstep
	- ppl in the 90's, with their RAM n CPU, wont be able to imagine what applications we have today now that compute has grown orders of magnitude
- its still possible to check something without full understanding
	- CTO can check domain expert by writing tests
	- PM can check SWE by using the product
	- SWEs dont need to know assembly
- ultimately, we only check at a layer of abstraction
- problem: tech debt, so still must understand **core architecture** (the extensible parts) but dont need to understand 'leaf nodes' (the extended parts)
	- core architecture: human must deeply understand and review code
	- leaf nodes: can vibe code
- How to succeed at vibe coding: be Claude's PM
	- spend 15-20min collecting guidance into a single prompt and let Claude execute
		- this isnt writing the prompt by hand! its a back n forth conversation w claude to explore codebase.
		- capture essence of 
			- what user wants, 
			- what files will be changed, 
			- what patterns in codebase to follow
- case study: 22k line merge into their RL codebase
	- still days of human coding n guidance
		- coming up with requirements
		- figuring out what system should be
	- mostly leaf nodes (they dont expect those parts to change/extend in the future)
	- extensible parts still with human supervision
	- carefully designed stress tests for stability
	- designed for human readable and easily verified input/output
	- verifiable checkpoints to check its correct even without understanding/reading the underlying
- minimalist end to end tests (that remain general rather than detailed)
	-  just three main scenarios: the happy path, one error case, and another error case
	- explicitly warns against Claude writing tests that are "too implementation specific," noting this is a common rabbit hole the AI can fall into
	- the tests are often the only part of the code he'll actually review
## instruction detail
"it depends a lot on what you care about".
- For things where he doesn't care about implementation: "I won't talk at all about the implementation details. I'll just say these are my requirements like this is what I want at the end"
- When he knows the codebase well: He goes "into much more depth of like, hey, these are the classes you should use to implement this logic. Look at this example of a similar feature"
- not explicitly stated but i assume the first point is for vibe code, the second point is for core architecture?
