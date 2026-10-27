# Glacier Planner for agents

Canadian retirement questions, with numbers from the calculation engine and evidence the person can keep.

## Build an app or agent

Start with the [HTTP and MCP quickstart](https://planner.glacierfinancial.ca/developers), then read the [live calculator contract](https://planner.glacierfinancial.ca/api/calculate). The public first calculation uses supplied, confirmed inputs without a Glacier account or API key. Saved household work uses a separate OAuth connection.

## Install the skill

```bash
npx skills add marcpineault/glacier-planner-agents
```

Review [SKILL.md](skills/glacier-planner/SKILL.md) before installing. Choose the supported agent and installation location in the CLI. Installation adds instructions; it does not connect an account, accept assumptions or enable payment. Skills support and remote MCP access depend on the actual host.

The install command follows the [official skills CLI documentation](https://skills.sh/docs/cli). Its optional anonymous install telemetry is described there; `DISABLE_TELEMETRY=1` opts out. This repository does not claim a leaderboard listing, installs, citations or recommendations.

## Useful jobs

| Question | Start here | Access |
| --- | --- | --- |
| Retire at 63 or 65? | [Worked guide and made-up inputs](https://planner.glacierfinancial.ca/guides/retire-at-63-or-65-canada) | Available basic calculator; no Glacier account |
| CPP at 65 or 70? | [Compare CPP start ages with retirement and OAS held at 65](https://planner.glacierfinancial.ca/guides/cpp-at-65-or-70-canada) | Made-up example; basic calculator without a Glacier account |
| Spend $5,000 more each year? | [Spending comparison](https://planner.glacierfinancial.ca/guides/retirement-spending-canada) | Available basic calculator; no Glacier account |
| Will our money last as a couple? | [Joint retirement projection](https://planner.glacierfinancial.ca/guides/retirement-calculator-for-couples-canada) | Available basic calculator for two people; no Glacier account |
| What changed in my plan? | [Saved-plan check-in](https://planner.glacierfinancial.ca/guides/what-changed-in-my-retirement-plan) | OAuth and permission to read the person's saved evidence |

Made-up templates require the person to review and explicitly confirm assumptions and any compared benefit start ages before calculation. A benefit-age comparison holds the supplied CPP/QPP amount at 65 and OAS residence years fixed; it does not infer extra work or residence years or choose an optimal start age. The basic calculator excludes property, debts and other cases listed in its live contract. A projection is not a promise or personalized investment advice.

## Connect the right service

| Service | URL | What it does |
| --- | --- | --- |
| Free first calculation MCP | `https://planner.glacierfinancial.ca/calculate/mcp` | `calculate_retirement`: supplied, confirmed basic inputs and one explicit what-if; no Glacier account, key or payment |
| Read-only sample MCP | `https://planner.glacierfinancial.ca/sample/mcp` | Synthetic stored results only; does not calculate personal inputs |
| Saved-plan MCP | `https://planner.glacierfinancial.ca/mcp` | Separate OAuth connection; account permissions and feature access apply |
| HTTP calculator contract | [GET /api/calculate](https://planner.glacierfinancial.ca/api/calculate) | Current schema, scope and made-up example; POST `{"input":...}` only after confirmation |

Glacier's public calculator does not save financial inputs/results. The person receives a portable input artifact; their AI host or chosen storage can retain it. Importing an exact baseline into an account preserves its free basic result. Other saved results, advanced tools and reports have their own access. See [current pricing](https://planner.glacierfinancial.ca/pricing), [privacy](https://planner.glacierfinancial.ca/privacy) and [terms](https://planner.glacierfinancial.ca/terms). Do not put personal inputs, artifacts, credentials or client data in this repository or its issues.

## Registry metadata

[`server.json`](server.json) describes **only the free calculator MCP**. It is not the sample or the OAuth saved-plan server. The [official MCP Registry](https://registry.modelcontextprotocol.io) hosts metadata, not this hosted service or its private implementation. Metadata publication does not establish acceptance or listing by any AI host.

Full maintained instructions: [agent guide](https://planner.glacierfinancial.ca/docs/agents), [public skill](https://planner.glacierfinancial.ca/docs/agents/skill.md), and [tool reference](https://planner.glacierfinancial.ca/docs/agents/tools.md).

## License

MIT applies to the documentation in this repository. The hosted service, private calculation engine, customer data and trademarks are not included or licensed here.
