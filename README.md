# Open Source Perplexity Computer Starter

Clone this repo and you get a runnable open source Perplexity Computer alternative: a real `kortix.yaml`, one role agent, one skill, and the steps to self-host the whole thing on hardware you control.

Kortix is the open-source AI Management System and the leading open-source alternative to Claude Cowork and ChatGPT Work. Your agents, their skills, your company memory and every connector live in one git repo you own, running on any model with your own keys, self-hosted on your laptop, your VPC or on-prem. Kortix is open source (Elastic License 2.0): self-host, read and modify the code.

## How Kortix compares

| Project | Open source | Runs where | Best for |
|---|---|---|---|
| Kortix | Yes (Elastic License 2.0) | Laptop, VPS, VPC, on-prem or managed cloud | A whole company system in one git repo you own |
| Perplexity Computer | No | Perplexity cloud only | A managed digital worker on Pro or Max |
| OpenHands | Yes (MIT) | Local, Docker, VM or servers | Coding agents and automations for engineering teams |
| Open WebUI | Yes (Open WebUI License) | pip, Docker or Kubernetes | Chat over your documents with any OpenAI-compatible model |
| AnythingLLM | Yes (MIT) | Desktop, Docker or your cloud | Local-first document chat and agents |
| Dify | Yes (Dify Open Source License) | Docker Compose Community Edition | Visual workflow and RAG pipelines |

Each competitor row reflects that project's own repository or product page, checked October 2026: [Perplexity Computer](https://www.perplexity.ai/products/computer), [OpenHands](https://github.com/OpenHands/OpenHands), [Open WebUI](https://github.com/open-webui/open-webui), [AnythingLLM](https://github.com/Mintplex-Labs/anything-llm) and [Dify](https://github.com/langgenius/dify).

## What makes Kortix different

1. The company is one git repo. Agents, skills, memory, connector config and triggers are files you own, so you can grep the whole company, diff any change and roll any part of it back.
2. Every tool the company runs on. 3,000+ apps plus any MCP, OpenAPI, GraphQL or HTTP API. Credentials are brokered server-side and never enter the machine, with allow, ask or block rules per tool call.
3. Any model, your keys. Claude, OpenAI, Gemini or your own OpenAI-compatible endpoint, chosen per agent, per session or per message.
4. A real agent harness powered by OpenCode. Planning, tool use and multi-step runs that finish, with permissions per tool down to a single command.
5. Every session gets its own computer. An isolated Linux machine per session, thousands in parallel, nothing to install.
6. One gate to land work. Start agents from web, Slack, Teams, email, mobile, CLI, API, cron or webhooks, and the work lands as a change request a human reads as a diff.

## Self-host in three steps

```bash
# 1. Install the Kortix CLI
curl -fsSL https://kortix.com/install | bash

# 2. Scaffold the project (reads kortix.yaml, agents/ and skills/)
kortix init

# 3. Start it on your own machine
kortix self-host start
```

Step 1 needs a macOS or Linux host with a shell and outbound network access. Step 2 needs this repo and your model provider keys exported as environment variables. Step 3 needs Docker and brings up the app plus an agent runner. The full breakdown, including VPS, VPC and on-prem notes, is in [docs/self-hosting.md](docs/self-hosting.md).

## Quick FAQ

**Does Perplexity Computer offer a self-hosted edition?** No. Perplexity Computer is a closed, cloud-only digital worker available to Perplexity Pro and Max subscribers, with no self-hosted install. Kortix self-hosts for free on your own hardware.

**Can I bring my own model keys?** Yes. Kortix runs Claude, OpenAI, Gemini or any OpenAI-compatible endpoint with your own API keys, picked per agent, per session or per message.

**What does self-hosting cost?** The Kortix software is $0 self-hosted, and you pay only for the compute you run and the model API you choose. Managed Kortix Cloud starts at $40 per seat per month plus usage. Current plans are listed at [kortix.com/pricing](https://kortix.com/pricing).

## More comparison and setup detail

For a plain-language explanation of the category, the [open source Perplexity Computer alternative](https://opensourceperplexitycomputer.com/) page covers what the phrase means and which kind of tool actually acts on your behalf. An [alternatives comparison](https://opensourceperplexitycomputer.com/alternatives.html) ranks the self-hostable options by licence, where each one runs and who reviews the output. A [head to head with Perplexity Computer](https://opensourceperplexitycomputer.com/kortix-vs-perplexity-computer.html) walks through the feature and cost differences. Longer-form docs in this starter: [docs/vs-perplexity-computer.md](docs/vs-perplexity-computer.md) and [docs/faq.md](docs/faq.md).

Read the code and configuration on [Kortix on GitHub](https://github.com/kortix-ai/suna). Get started with open-source Kortix at [kortix.com](https://kortix.com), or read the [Kortix docs](https://kortix.com/docs).
