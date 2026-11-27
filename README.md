# The 6-agent growth team

6 AI agents that run the whole marketing loop: research, competitors, SEO, content, growth ops, inbound and outbound.
One agent per job, and each one owns its job from start to finish.

All 6 run on the [ColdIQ MCP](https://coldiq.com). One ColdIQ account reaches Reddit, Exa, Parallel, Firecrawl, the Meta Ad Library, BuiltWith, DataForSEO, Serper, influencers.club, Instantly and Slack. No 11 subscriptions, no 11 API keys. Your own tools (Sume, beehiiv, Customer.io, Dub, Twenty, PostHog, Paper) plug in through their official MCPs.

Works in Grok Bot, Grok Build, Claude Code, Cursor, Codex, ChatGPT and Claude.

## The 6 agents

| # | Agent | What it does | Through the ColdIQ MCP | Your own MCPs |
|---|---|---|---|---|
| 1 | [Market Researcher](skills/01-market-researcher/SKILL.md) | Reads what your buyers say online and turns it into a weekly brief on what to talk about. | Reddit, Exa, Parallel | none |
| 2 | [Competitor Spy](skills/02-competitor-spy/SKILL.md) | Tracks rival pages, prices, tech stacks and the ads they keep paying for. | Company data, Firecrawl, Meta Ads, BuiltWith | none |
| 3 | [SEO Machine](skills/03-seo-machine/SKILL.md) | Finds the searches you don't rank for yet and drafts the pages to win them. | DataForSEO, Serper | Paper (optional) |
| 4 | [Content Studio](skills/04-content-studio/SKILL.md) | Turns one idea into ad videos and a newsletter, then finds the creators to push it. | influencers.club | Sume, beehiiv |
| 5 | [Growth Operator](skills/05-growth-operator/SKILL.md) | Prepares the nurture emails, drafts partner outreach, logs every lead in your CRM and reports what converts in Slack. | Enrichment, email finding, Slack | Customer.io, Dub, Twenty, PostHog |
| 6 | [Inbound x Outbound](skills/06-inbound-outbound/SKILL.md) | Turns every signup and site visitor into an enriched lead, loads the outbound follow-up and pings your team in Slack when someone replies. | Visitor ID, enrichment, email finding, Instantly, Slack | none |

Agents 1, 2 and 6 need nothing but the ColdIQ MCP.

## How they work together

```
01 Market Researcher ──> 03 SEO Machine ──> 04 Content Studio ──> 05 Growth Operator
         │                      ▲                   ▲                     ▲
         └──> 02 Competitor Spy ┴───────────────────┘                     │
                                          06 Inbound x Outbound ──────────┘
```

Each agent ends by naming the agent its output goes to, so you can run them one by one or as a weekly loop: Monday 01 and 02, then 03 and 04 on what they found, 06 every day, 05 on Friday for the report.

## Install in 2 steps

### 1. Connect the ColdIQ MCP

Server URL: `https://mcp.coldiq.com/mcp`

It signs in with your ColdIQ account (OAuth). There is no API key to paste and nothing secret in this repo. New accounts get up to 1,450 credits as they get started.

- **Grok Bot**: in a chat, ask: `Add this MCP server: https://mcp.coldiq.com/mcp` and sign in when asked.
- **Claude Code**: `claude mcp add --transport http coldiq https://mcp.coldiq.com/mcp` (or open Claude Code in this folder: the `.mcp.json` is already here).
- **Cursor**: Settings > MCP > Add server, URL `https://mcp.coldiq.com/mcp` (or copy `install/cursor-mcp.json` to `.cursor/mcp.json`).
- **Codex**: add the block of `install/codex-config.toml` to `~/.codex/config.toml`.
- **ChatGPT / Claude (web and mobile)**: Settings > Connectors > Add custom connector, URL `https://mcp.coldiq.com/mcp`.

For agents 5 and 6, connect Instantly and Slack once in the ColdIQ dashboard: the agents then reach them through the same MCP.

### 2. Load the agents

- **Grok Bot**: create one Bot per agent and paste its `SKILL.md` as the Bot instructions. Start with 01 and 06: they work with the ColdIQ MCP alone.
- **Grok Build**: `grok plugin install https://github.com/julescoldiq/marketing-6-agents`. The plugin bundles the 6 skills and the ColdIQ MCP. Then open `/mcps`, select `coldiq`, press `i` to sign in.
- **Claude Code**: `./install.sh claude` copies the 6 skills to `~/.claude/skills/`. Then: `/01-market-researcher we sell a CRM to 10 to 50 person agencies`.
- **Cursor**: `./install.sh cursor` writes them to `.cursor/rules/` of the current project.
- **Codex**: `./install.sh codex` writes one `AGENTS.md` with the 6 agents.
- **ChatGPT / Claude projects**: one project per agent, paste its `SKILL.md` as the project instructions.

## Your own MCPs (agents 3, 4 and 5)

All official, all optional: an agent without one of them returns a draft to paste instead.

| Tool | Used by | MCP |
|---|---|---|
| Paper | 03 SEO Machine | Paper desktop app ([paper.design](https://paper.design)) |
| Sume | 04 Content Studio | Your Sume account |
| beehiiv | 04 Content Studio | `https://mcp.beehiiv.com/mcp` (OAuth) |
| PostHog | 05 Growth Operator | `https://mcp.posthog.com/mcp` |
| Customer.io | 05 Growth Operator | `https://mcp.customer.io/mcp` (an admin enables it first) |
| Dub | 05 Growth Operator | `https://mcp.dub.sh/mcp/dub-partners` and `/mcp/dub-links` (Dub API key) |
| Twenty | 05 Growth Operator | Your Twenty workspace URL ([docs](https://docs.twenty.com/user-guide/ai/capabilities/mcp)) |

`install/all-mcps.json` holds the ColdIQ, PostHog, Customer.io and beehiiv servers in one block for Claude Code or Cursor.

## Always up to date

Each agent starts by asking the ColdIQ MCP how ColdIQ runs that job today (`search_knowledge` and `load_skill`), so the method follows ColdIQ's playbooks as they improve. The files here fix the scope, the steps, the output and the hand-off.

## Guardrails built into every agent

- A paid call that could pass 25 credits, or a pull over 10 rows, shows its estimate first and waits for your yes.
- No agent publishes, sends, activates or DMs. They prepare, you click. The only exception is the Slack report or alert in your own team channel, after your yes.
- No invented facts: every quote, price and number carries its source, and missing data is reported as missing.
- Before calling a provider endpoint for the first time, the agent reads its parameters. It never guesses.

## License

MIT. Built by [ColdIQ](https://coldiq.com).
