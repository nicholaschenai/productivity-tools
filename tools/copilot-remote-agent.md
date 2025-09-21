---
date: 2025-09-21
time: 17:04
author:
title:
created-date: 2025-09-21
tags:
paper: https://github.blog/news-insights/product-news/github-copilot-meet-the-new-coding-agent/
code:
zks-type: lit
is_public: true
---
## Features
- Responds to issues or via agent tasks (will submit PR)
- can be called via [API](https://docs.github.com/en/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/using-copilot-to-work-on-an-issue) access
- Can use MCPs
	- github and playwright MCP configured by default
## Tips
- [easier firewall config](https://github.blog/changelog/2025-07-15-configure-internet-access-for-copilot-coding-agent/) now
- also see [coding-agent-tips](../themes/coding-agent-tips.md)
- Use github secrets to expose testing APIs (e.g. github models) to allow the agent to use testing services for realistic feedback, then record the output to make mocks and fixtures for CI testing
- Comes configured with Docker -- Spin up a dev Docker env for agent to debug/interact with