# FAQ: choosing an open source Perplexity Computer alternative

These are the questions teams ask before they switch from a closed cloud agent to open source Kortix. Each answer stands on its own.

## Is Perplexity Computer open source?

No. Perplexity Computer is a closed, cloud-only digital worker available to Perplexity Pro and Max subscribers, and there is no self-hosted edition or published source ([Perplexity Computer product page](https://www.perplexity.ai/products/computer)). Kortix is the open-source alternative: you can read, fork and modify the code and run it on your own hardware.

## Can I self-host Kortix for free?

Yes. Kortix self-hosts at no software cost on a laptop, a VPS, a VPC or an on-prem host, and you pay only for the compute you run and the model API you choose. Managed Kortix Cloud starts at $40 per seat per month plus usage if you would rather not run the stack, with current plans at [kortix.com/pricing](https://kortix.com/pricing). The three setup commands are in [self-hosting.md](self-hosting.md).

## Which models can Kortix run?

Kortix is model-agnostic. You can run Claude, OpenAI or Gemini models, or any OpenAI-compatible endpoint of your own, and choose the model per agent, per session or per message. You bring your own API keys, so nothing routes through a vendor-selected model. That is the main structural difference from Perplexity Computer, which picks the models for you.

## How does Kortix differ from OpenHands, Open WebUI, AnythingLLM and Dify?

All four are open source and self-hostable, and each does one part of the job. OpenHands is a coding-agent control center, Open WebUI is chat and retrieval over documents, AnythingLLM is local-first document chat, and Dify is a visual workflow and RAG builder. Kortix puts the whole company in one git repo, agents, skills, memory and connectors, with per-tool permissions and a change request a human reviews before work lands. The sourced table is in [vs-perplexity-computer.md](vs-perplexity-computer.md).

## Where do my data and my credentials live with Kortix?

Everything Kortix runs on stays in infrastructure you choose. Agent, skill and memory files live in your git repo, and connector credentials are brokered server-side and never enter a session's machine, so a sandbox never holds a raw secret. Secrets are encrypted at rest with a key per project. You can run it on a laptop, a VPS, your VPC or on-prem, or use Kortix Cloud.

## How do I start?

Install the CLI, scaffold this repo, and start the stack:

```bash
curl -fsSL https://kortix.com/install | bash
kortix init
kortix self-host start
```

The source is on [Kortix on GitHub](https://github.com/kortix-ai/suna), the product docs are at [kortix.com/docs](https://kortix.com/docs), and the entry point is [kortix.com](https://kortix.com). Self-host open-source Kortix whenever you are ready.
