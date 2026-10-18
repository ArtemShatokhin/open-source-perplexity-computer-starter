# How to run your first session on an open source Perplexity Computer alternative

Three commands start your first session on an open source Perplexity Computer alternative, and the run ends as a change request you read and merge. Kortix is the open-source AI Operating System. Agents, skills, company memory and connectors are files in one git repository, and every session runs on its own computer. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free.

In this system a session is one agent run in its own sandbox and branch, and a change request is the reviewed merge that carries that work toward `main`. A Perplexity Computer run ends in a thread you read, and the trust step is yours to improvise afterward. Here the trust step is built in: the agent opens a diff, a person reads it, and only then does anything land. That gate is also what makes unattended work safe, because nothing merges itself. What the hosted product is, in plain words, is on the [what is a Perplexity Computer page](https://opensourceperplexitycomputer.com/what-is-a-perplexity-computer).

## What you need before you start

- A macOS or Linux host with a shell and outbound network access, for the installer.
- Docker, installed and running.
- This starter repo, cloned locally.
- A model provider key exported as an environment variable, such as `ANTHROPIC_API_KEY` or `OPENAI_API_KEY`.

The repo already carries what the session will use: one agent, one skill, and a manifest that ties them together. Host-by-host detail, VPS and on-prem included, is in [self-hosting.md](docs/self-hosting.md).

## The three commands

```bash
# 1. Install the Kortix CLI
curl -fsSL https://kortix.com/install | bash

# 2. Scaffold the project (reads kortix.yaml, agents/ and skills/)
kortix init

# 3. Start it on your own machine
kortix self-host start
```

The installer puts the `kortix` command on your path and asks for no account and no hosted control plane. `kortix init` reads this repo's manifest and agents, and it leaves secrets out of the tree: model keys stay as environment variables on the host, and connector credentials are brokered server-side. `kortix self-host start` starts the app on your host. From there, every session boots a disposable Linux sandbox on its own branch, with your repo and tools already installed.

The starter's `kortix.yaml` names the model the agent uses, by environment variable rather than a literal key:

```yaml
model:
  provider: anthropic
  name: claude-sonnet
  api_key_env: ANTHROPIC_API_KEY
  fallback:
    provider: openai
    name: gpt-5
    api_key_env: OPENAI_API_KEY
```

Any model provider with your own keys. Or the ChatGPT plan you already pay for. Or sign in with your OpenCode Console account for OpenCode Zen and Go. Switching models is a one-line edit in the manifest, and the next session picks it up.

## What the first session does

Start a session from the CLI and give it a small job, then list the change requests:

```bash
kortix sessions new --prompt "Summarize this repo's agents and skills, then open a change request"
kortix cr ls
```

1. The sandbox boots. It clones the repo and cuts a branch named for the session; the branch name is the `session_id` ([Kortix docs](https://kortix.com/docs)).
2. The agent loads its role. This repo ships one agent, `agents/research-lead.md`, whose description reads: "Owns a research question end to end: plans the search, gathers primary sources, cites every claim and opens a change request with the findings."
3. The agent plans before it searches. Its first working rule reads: "Restate the question in one sentence and write down what a sufficient answer must contain."
4. It gathers evidence with the sources kept attached. The `cite-sources` skill it carries says to "Cite the primary source, not a summary of it", and to record the date a source was checked when the fact can change.
5. It writes the findings as a markdown report, commits on the session branch, and opens a change request. The role file draws the boundary plainly: "You do not publish anything and you do not merge your own work; you open a change request."
6. You read the diff and decide. The repo's self-hosting doc gives the working signal: "A session that reaches `cr ls` as a change request is working."

## What lands where

One isolated sandbox per session. Each session has its own isolated machine and branch. The agent commits on that branch, pushes it, and opens a change request against the project's default branch ([Kortix docs](https://kortix.com/docs)). Session work reaches `main` through a change request. Merge is default-deny for agents. A person with the merge permission reviews the change request and merges it, and the docs name that permission `project.gitops.merge`.

The gate is what makes unattended work safe. A trigger starts a session with nobody asking, through a cron schedule or a signed webhook. This repo's manifest carries a commented example:

```yaml
# triggers:
#   - slug: daily-research-digest
#     type: cron
#     cron: "0 9 * * 1-5"
#     prompt: Summarize yesterday's sources and open a change request with the digest.
```

A trigger-started session gathers its sources, writes its digest, and stops at a change request waiting in the queue. No schedule can push to `main` on its own. This repo is the clone-and-run starting point, and the wider GitHub field is mapped on the [open source Perplexity Computer on GitHub page](https://opensourceperplexitycomputer.com/open-source-perplexity-computer-github).

## Troubleshooting the first run

| Symptom | What it means | Fix |
|---|---|---|
| `kortix` is not found after the install | The install directory is not on your `PATH` | Open a new shell, or add the directory to `PATH` |
| `kortix init` cannot find the config | The repo is not cloned in the current directory | Clone this repo and run the command inside it |
| `kortix self-host start` stops at once | Docker is not installed or not running | Install Docker, start it, run the command again |
| The stack warns about disk space | The first session's sandbox image needs free disk | Free disk space and run the command again |
| A model call fails mid-session | The provider key is not exported | Export `ANTHROPIC_API_KEY` or `OPENAI_API_KEY` for the provider in `kortix.yaml` |
| The app is unreachable on a VPS | The app's port is not open on that host | Restrict the app's port to your network, or open it |

## First-session questions

- **Does the agent run on my own machine?** The agent runs in its own sandbox. One isolated sandbox per session. Each session has its own isolated machine and branch. On a self-hosted install that sandbox runs on the host running Docker; on Kortix Cloud, Kortix runs it. Your laptop is where you start the session and read the diff.
- **Can the agent merge its own change request?** No, by default. Session work reaches `main` through a change request, and merge is default-deny for agents. The starter's research lead opens the change request and stops. An admin can grant the merge capability to an agent in its configuration, and a session can never merge a change request it opened itself.
- **Do I need to write code to add my own agent?** No. An agent is a markdown file in `agents/` plus a block in `kortix.yaml`. The research lead here sets its model, its skill and `permissions: default: ask` in front-matter, and the manifest's `agents.research-lead` block points at the file. Copy the pattern, change the name, and the next session can use the new agent.
- **Which models can a first session use?** Any model provider with your own keys. Or the ChatGPT plan you already pay for. Or sign in with your OpenCode Console account for OpenCode Zen and Go. The starter ships Claude as the per-agent model with an OpenAI-compatible fallback, both named by environment variable, so a model switch is a config edit.
