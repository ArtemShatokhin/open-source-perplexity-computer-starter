# What it costs to run an open source Perplexity Computer alternative

An open source Perplexity Computer alternative costs two things you can price before you start: the machine it runs on and the model calls its agents make. The software itself is free to self-host. A Perplexity Computer bill has a different shape: the plan is the floor, and a credit meter sits over the agent work. For effort-heavy Computer tasks, the meter is the part that grows.

Kortix is the open-source AI Operating System. Agents, skills, company memory and connectors live as files in one git repository, and every session runs on its own computer. You can keep the whole system on hardware you control, or hand the running to Kortix Cloud. Perplexity Computer is a hosted agent: you describe an outcome, and its cloud plans and carries the work out across websites, files and connected apps. The longer definition is on the [what is a Perplexity Computer page](https://opensourceperplexitycomputer.com/what-is-a-perplexity-computer).

## The subscription is a floor under every Computer bill

Perplexity Computer has no price of its own. It ships inside Perplexity's subscription plans, so every Computer task starts from a plan. Perplexity's plans page lists Free at $0, Pro at $17 a month when billed annually, and Max at $167 a month billed annually ([Perplexity's plans page](https://www.perplexity.ai/pro), checked October 2026). Month to month costs more: the Max help article prices that plan at $200 a month ([Perplexity Max](https://www.perplexity.ai/help-center/en/articles/11680686-perplexity-max), checked October 2026).

Enterprise prices each seat separately, and every seat carries its own floor. Enterprise Pro is $40 a seat each month, or $400 a seat for a year. Enterprise Max is $325 a seat each month, or $3,250 a seat for a year, about $271 a month once the annual figure is spread across twelve ([Enterprise pricing and billing FAQ](https://www.perplexity.ai/help-center/en/articles/10352986-enterprise-pricing-and-billing-frequently-asked-questions), checked October 2026). Each Enterprise Pro seat also includes 500 credits a month, and each Enterprise Max seat 15,000, with an organization pool that admins fund on top. The monthly total therefore scales with headcount before anyone runs a task. The full plan-by-plan breakdown is on the [Perplexity Computer pricing page](https://opensourceperplexitycomputer.com/perplexity-computer-pricing).

## The credit meter is where the bill grows

Credits are the meter, and Perplexity spends them only on Computer tasks. Ask searches use none ([How credits work on Perplexity](https://www.perplexity.ai/help-center/en/articles/13838041-how-credits-work-on-perplexity), checked October 2026). One hundred credits equal $1. Perplexity's own examples price a quick fact at 15 to 70 credits, a multi-step research report at 350 to 950, a data dashboard at 2,400 to 9,800, and an app or multi-day build above 15,000. The effort setting decides how deep a task goes, and higher settings run pricier models ([Effort mode in Perplexity Computer](https://www.perplexity.ai/help-center/en/articles/20260917-effort-mode-in-perplexity-computer), checked October 2026). At that rate, one dashboard-sized run draws $24 to $98 in credits. Against a $17 monthly plan, the task is the bigger number.

Plans start you with very different balances. Max includes 10,000 credits a month. Consumer Pro includes none: its 4,000 credits are a one-time bonus that expires about 30 days after signup, and the recurring allowance on paid Pro plans is a weekly amount of Computer usage that Perplexity is still rolling out. Nothing carries over. Monthly credits lapse at the next billing date, and purchased credits expire after a year without Computer use. Auto-refill is off until you switch it on, and a Max account also carries a monthly spending cap on credit charges, $200 by default and settable up to $5,000 (same source, checked October 2026).

The Perplexity fan's argument runs: $17 a month beats any server bill. On light use, it can. It stops holding when agent work becomes the point. The meter sits outside the plan price and moves with how hard the agent works, so a team that leaves auto-refill on and runs recurring Computer tasks budgets from the meter. The plan price stops predicting the bill.

## What a self-hosted instance actually bills

On the open route, the two lines are the hardware and the model usage, and the software adds nothing to either. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free. This starter repo installs the stack on your own hardware with three commands:

```bash
# 1. Install the Kortix CLI
curl -fsSL https://kortix.com/install | bash

# 2. Scaffold the project (reads kortix.yaml, agents/ and skills/)
kortix init

# 3. Start it on your own machine
kortix self-host start
```

The installer needs a macOS or Linux host with a shell and outbound network access. `kortix init` reads the `kortix.yaml`, `agents/` and `skills/` already in the repo, and it wants your model keys exported as environment variables. `kortix self-host start` brings up the app and an agent runner with Docker. Each session then boots its own isolated Linux sandbox on its own branch ([self-hosting.md](docs/self-hosting.md)).

The machine line is whatever host you already own or rent. The model line lives in the repo:

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

Model keys are read from the host environment by name, so no secret sits in the tree. Any model provider with your own keys. Or the ChatGPT plan you already pay for. Or sign in with your OpenCode Console account for OpenCode Zen and Go. Whichever you pick, that provider's published price list is the model bill. You can read it before you start. No seat count multiplies the bill, and no meter prices each run.

If you would rather not run the stack, Kortix Cloud sells credits: Free is $0 with 200 credits per month and 1 project. Paid plans start at $50 a month for 5,000 credits, and members are free, sharing one credit pool. With your own keys on Kortix Cloud, credits pay for the agent computer and 5% of model usage past $1,000 a month, and the model usage itself bills to your provider ([Kortix pricing](https://kortix.com/pricing), checked October 2026).

## Perplexity's own hardware route

Perplexity sells one route off its cloud, and it carries a different name. Portable Computer runs the model and the agent on your own hardware: an NVIDIA DGX Spark, or a Windows or Linux PC with a supported NVIDIA RTX GPU ([What is Portable Computer?](https://www.perplexity.ai/help-center/en/articles/20260915-what-is-portable-computer), checked October 2026). Work the local model finishes spends no credits, which makes long or recurring local work cheap to run. The subscription, the hardware requirement and the closed code all stay, so the route trims the meter without changing who owns the stack.

## Which route costs less

Kortix is the recommendation when the work repeats, when several people need the system, or when the bill has to be readable before you start. Perplexity fits a single person who runs the occasional Computer task inside a plan they already pay for.

| Route | What you pay | Where it wins |
|---|---|---|
| Kortix, self-hosted | Hardware plus model calls, software free | Recurring agent work you own |
| Kortix Cloud | From $50 a month for 5,000 credits | A managed instance with no seats |
| Perplexity Free | $0, Computer capacity on paid plans | Testing a single task |
| Perplexity Pro | $17 a month annually, then credits | Occasional Computer work |
| Perplexity Max | $167 a month annually, 10,000 credits | Heavy single-person Computer use |
| Perplexity Enterprise | From $40 a seat a month | Managed seats for a team |

## Questions buyers ask

- **Is Perplexity Computer free?** Free is the name of Perplexity's $0 plan, and the Computer capacity it documents sits on the paid plans. Pro lists expanded Computer access, no monthly credits, a one-time 4,000-credit bonus and a weekly included allowance that is still rolling out. Max is the only consumer plan with a published monthly figure, 10,000 credits. Perplexity sells no self-hosted build of the cloud agent (checked October 2026).
- **What does it cost to self-host an open source Perplexity Computer alternative?** The software is free, and the bill is the hardware plus the model calls. A Linux host or cloud instance runs the stack, and your provider bills the model usage at its published prices. You pay the provider directly, with no plan in the middle. The steps are in [self-hosting.md](docs/self-hosting.md).
- **Do Perplexity Computer credits roll over?** No. Monthly credits lapse at the next billing date. Bonus credits are one-time per account and expire about 30 days after they arrive, so canceling and resubscribing does not bring them back. Purchased credits expire after a year without Computer use (Perplexity's credits help page, checked October 2026).
- **How much do model calls cost on a self-hosted instance?** Whatever your provider charges. Kortix runs any model provider with your own keys, per agent, per session or per message, and the calls bill at that provider's list prices. A self-hosted instance adds no markup of its own. On Kortix Cloud, credits cover the agent computer, and model usage through your own key bills to the provider.
