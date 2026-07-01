---
is_public: true
---
# Coding agent tips
## Setup
- Setup system prompt (AGENTS.md, CLAUDE.md etc) for generic instructions
- Write slash commands / skills / documentation for any repetitive instructions ('Dont repeat yourself' principle) and/or instructions that are situation specific (generic ones should go into system prompt)
- setup github cli to allow agents to manage github (e.g. issues). Remember to scope permissions properly and protect important branches!
- UPDATE: most coding agents now come with native websearch so this might be redundant: If possible, always configure some websearch MCP
	- free:  brave 2,000 queries per month
	- paid: bing, perplexity [perplexity-ai](../tools/perplexity-ai.md)

## Interaction and context management
- Do thread branching (`/branch` in claude, `/fork` in codex) to explore multiple scenarios and recycle accumulated context
	- in claude, you can double esc to rewind as well
- Make use of subagents, most harnesses now come with default subagent types so you don't have to manually configure them. Can be as simple as prompting the main agent to use subagents.
	- subagents also help manage context, see later
### IMPORTANT: Manage context well!
Be aware of 'context rot' ( https://www.trychroma.com/research/context-rot ) / 'lost in the middle' ( https://arxiv.org/abs/2307.03172 ) effects -- when context gets too long, even if it is under the model's maximum context length, memory recall (recalling facts from its context) and reasoning can **degrade**. In light of this, many of the tips in following sections are written with context management in mind
- rule of thumb: approx 50% model's context window, or for those 1m context models approx 200-300k tokens
- tip: have a 'handoff' command to capture important points of the conversation when it gets too long

## Testing
- If working with live API services (eg databases), see if can get a testing API / create dev environment with API. Coding agents perform better when it can execute code and get feedback
- setup a devcontainer json to use devcontainers for reproducible environments and security
	- github codespaces will read this and configure accordingly -- useful for a quick VM to YOLO mode so don't have the frictions of approval
		- comes with github CLI

---
## Structured workflow
This is for projects that have some level of complexity in it; for simple projects just talk to the AI directly. In a large project, we need a structured workflow to keep the context focused and short.
### 1. Gather requirements
Have a command to discuss with AI to elicit what you want in **simple human language** into a doc (PRD). If you can't articulate what you want, the AI might make assumptions which goes against your intent. Once per project. Some ideas:
- What is the value proposition / goals?
- What are the explicit and implicit requirements?
- What is the user story, use cases, target users?
- How is success defined?

### 2. Architecture design
Have a command to discuss the architecture design with AI, referencing the PRD from previous and then writing the architecture design doc. Having this high level technical overview helps chunk the work items into slices small enough for AI to complete effectively. Once per project. Some ideas
- What is the high level architecture e.g. modules, data models and their interactions? What patterns do you want to follow?
- What are the features in your app?
- What is the tech stack?
- How is success defined?
- Plan out slices: units of work that produce something checkable
- Plan out build sequence and parallelization to take advantage of parallel coding agents

### 3. Testing/Validation strategy
Need a proper doc for testing and validation strategy to help AI check its outputs and iterate. Once per project
- From PRD / architecture design doc, infer workflows as a hint for what to test
- Linting, type checking, formatting
- Unit, integration, E2E tests
- Explicitly list commands for testing and validation for AI to follow

### 4. Plan and execute
This is done per slice/feature, i.e. multiple times per project. Only do this for slices of at least moderate complexity. For simple fixes, just talk to AI directly

#### Planning
Per slice (reference the architecture design doc), 

- First get the agent to familiarize with the codebase e.g. identify project structure, languages, frameworks, runtime versions, patterns, integration points, config files etc
	- Have a command for this. Using `tree` (linux) and git history helps
	- alternatively you can directly tell it what to do
- Then discuss with AI to write a plan doc. We separate planning from execution because planning alone incurs some context, especially from reading the codebase which might contain irrelevant details. We want the execution agent to have as focused context as possible (i.e. the feature plan doc), so that it still has enough context to code, test, and fix errors.
- AI needs to include these in the plan
	- Codebase files, documentation to read
	- New files to create
	- Step by step tasks and how to validate/test each step (see testing/validation strategy doc)
		- IMPORTANT: discuss with user the testing strategy. 
		- Efficiency tips, inspired by [vibe-coding-in-production](../talks/vibe-coding-in-production.md)
			- verification does not need to be tests, can be **easily checkable** artifacts like screenshots, logs, traces, output samples
			- Get AI to label tasks as 'core' (other code depends on this) and 'leaf' (no dependencies on this), and humans only read 'core' code
- Tip: require it to launch a subagent (which has a fresh context) to check the plan for completeness (main agent can test subagent with questions)
#### Execution
Once the plan is done, give instruction to a fresh agent to execute the plan, run tests to check its work and iterate till done
- can include reminders like to reference the testing/validation document for checking
- can include an 'implementation summary' instruction to tell you what was done, what was not (and what is the blocker preventing it e.g. some bug or incompatibility or missing credentials etc), where are the artifacts for human review and how to read them
