
- https://github.com/assafelovic/gpt-researcher

## features
ref https://docs.gptr.dev/docs/gpt-researcher/context/tailored-research
- has option for [source urls](https://github.com/assafelovic/gpt-researcher/blob/master/gpt_researcher/master/agent.py) so it only goes to specific site u specify
- customization for prompts n research report types

- has multiple [scraper classes](https://github.com/assafelovic/gpt-researcher/blob/master/gpt_researcher/scraper/scraper.py) for the scenarios below, decided via if else blocks (see [this](https://github.com/assafelovic/gpt-researcher/blob/master/gpt_researcher/scraper/scraper.py))
	- pdf, 
	- arxiv (if url is arxiv.org then it uses this API to get metadata and main article)
	- beautifulsoup or selenium or web base loader
		- web base loader (main one for html), uses langchain's scraper as main n beautifulsoup for imgs n other misc data

### new
- research on local documents (so its just chat with ur document store) or hybrid with web search
- [filtering by domain](https://docs.gptr.dev/docs/gpt-researcher/context/filtering-by-domain) which uses google's domain filter syntax
- agent based research
- azure support

## other

- ==the `ContextCompressor` class seems generically useful, learn about it when got time==

