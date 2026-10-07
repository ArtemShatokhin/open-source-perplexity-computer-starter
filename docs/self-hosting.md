# Self-hosting open source Kortix

Kortix is the open source AI Management System, and it self-hosts on a laptop, a VPS, a VPC or an on-prem host with three commands and no managed service. Agents, skills, company memory and connector config live in one git repo you own, and every session boots its own isolated Linux machine.

This guide runs this starter repo, so it assumes you already cloned it. Each step lists what it needs before you run it.

## Step 1: install the Kortix CLI

```bash
curl -fsSL https://kortix.com/install | bash
```

What it needs:

- A macOS or Linux host with a POSIX shell.
- Outbound network access to download the CLI binary.
- Permission to write to a directory on your `PATH`.

The installer puts the `kortix` command on your path and needs no account, no sign-up and no hosted control plane. It is a single static binary, so a fresh VPS or a container image works as well as a developer laptop.

## Step 2: scaffold the project

```bash
kortix init
```

What it needs:

- This repo cloned locally, since `kortix init` reads the `kortix.yaml`, `agents/` and `skills/` already in it.
- Your model provider keys, exported as environment variables such as `ANTHROPIC_API_KEY` or `OPENAI_API_KEY` for the provider you choose.
- A model selection in `kortix.yaml`. The starter ships with a Claude model per agent and an OpenAI-compatible fallback, both referenced by environment variable name rather than a literal key.

Model keys stay as environment variables on the host. Connector credentials are brokered server-side and never enter a session's machine, so nothing in the repo holds a secret.

## Step 3: start the stack

```bash
kortix self-host start
```

What it needs:

- Docker installed and running, since the command brings up the Kortix app and an agent runner as one stack.
- The model provider keys from step 2 available to the stack.
- Free disk for the first session's sandbox image.

The command starts the app on your host. From there, each session starts a disposable Linux sandbox on its own branch with your repo and tools already installed, and uses your locally configured model.

## Verify it works

Start a session from the CLI and ask for a small job, then read what the agent proposes as a change request:

```bash
kortix sessions new --prompt "Summarize this repo's agents and skills, then open a change request"
kortix cr ls
```

A session that reaches `cr ls` as a change request is working. Merge is human-gated: the agent opens the change request and you review the diff.

## Deployment notes

- Laptop: the fastest path to a first session. Nothing beyond Docker and a model key.
- VPS or VPC: the same three commands on a remote host, so sessions survive your laptop closing. Restrict the app's port to your network.
- On-prem: run the same container stack inside your own network when the data cannot leave it.
- Managed cloud: if you would rather not run the stack, Kortix Cloud runs it for you from $40 per seat per month plus usage, with current plans at [kortix.com/pricing](https://kortix.com/pricing).

Kortix is open source (Elastic License 2.0): self-host, read and modify the code. The source and configuration are on [Kortix on GitHub](https://github.com/kortix-ai/suna), and the product docs start at [kortix.com/docs](https://kortix.com/docs).
