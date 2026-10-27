---
name: glacier-planner
description: Compare Canadian retirement ages, spending, and CPP/QPP or OAS start ages with Glacier Planner, or read permitted saved-plan check-ins. Confirmed basic inputs need no Glacier account; saved plans use OAuth.
---

# Glacier Planner

Use the calculation engine for numbers and explain the returned evidence. Projections and education, not personalized investment advice.

## Choose the job

- **Retire at 63 or 65:** read https://planner.glacierfinancial.ca/guides/retire-at-63-or-65-canada/index.md. The made-up input template is at the same path with `index.md` replaced by `template.json`.
- **CPP at 65 or 70:** read https://planner.glacierfinancial.ca/guides/cpp-at-65-or-70-canada/index.md and its `template.json`. This made-up example changes only CPP start age; retirement and OAS stay at 65.
- **Compare two spending amounts:** read https://planner.glacierfinancial.ca/guides/retirement-spending-canada/index.md and its `template.json`.
- **What changed in my saved plan:** read https://planner.glacierfinancial.ca/guides/what-changed-in-my-retirement-plan/index.md. This needs the person's permitted saved plan; it has no public input template.

The guide examples are made up. Ask whether the person wants a demonstration or their own numbers. Never present the sample or an example as their plan.

## First calculation: no Glacier account

1. Read the live schema and scope at https://planner.glacierfinancial.ca/api/calculate. Ask for missing facts. The basic scope excludes property, debts, corporations, children, LIRA/LIF and extra planned contributions; other exclusions are in the contract. Do not invent financial inputs.
2. Review the inputs, return/inflation assumptions, benefit estimates and any compared CPP/QPP or OAS start ages with the person. Templates have `assumptionsAccepted:false`. Set it to `true` only after their explicit confirmation; installing this skill is not confirmation.
3. POST exactly `{"input": <confirmed input>}` to that URL, or use `calculate_retirement` with an `input` object on https://planner.glacierfinancial.ca/calculate/mcp. No Glacier account, API key or payment method is required for an available first calculation. Respect service errors and request limits; do not evade them or substitute an example result.
4. Explain spending coverage, first shortfall year, after-tax estate or gap, assumptions and engine/rates provenance. Give the person the returned `glacier-calculator-v1` input artifact to keep. It is not a saved-plan ID, ownership token or credential. Public calculations do not save financial inputs/results at Glacier; the caller and AI host can retain them. See https://planner.glacierfinancial.ca/privacy.

Stopping work earlier can reduce actual CPP/QPP. Review statement assumptions; do not silently change the statement amount. Returns are assumptions, not predictions.

For one explicit benefit-age what-if, `alternative.cppStartAges` and `alternative.oasStartAges` each take one integer per person. Keep other fields unchanged to isolate that comparison. The supplied CPP/QPP amount at 65 and OAS residence years stay fixed; changed work history or residence is not inferred. Read the live contract for the accepted ages in the person's province. This compares entered choices; it does not choose an optimal age.

For a finished read-only demonstration, use https://planner.glacierfinancial.ca/sample. Its separate MCP endpoint, https://planner.glacierfinancial.ca/sample/mcp, only reads synthetic saved results; it cannot calculate the person's inputs.

## Return to a saved plan

Reuse the person's approved connection to https://planner.glacierfinancial.ca/mcp. If none exists, let them sign in and approve OAuth in their own browser. Never request their password or tokens.

Use `find_households` to obtain the correct real `workspaceId` and `scenarioId`, then:

```json
{"tool":"plan_check_in","arguments":{"workspaceId":"<workspaceId>","scenarioId":"<scenarioId>"}}
```

This reads permitted existing saved evidence without calculating, editing, unlocking results or using a calculation allowance. An existing `runId` can pin the displayed result. Explain source dates, revisions and rule changes. Earlier locked results may yield inputs-only evidence. `no_saved_result` means a new projection is separate work; follow existing authorization and ask only where it is missing. Never invent past outcomes or describe projections as actual investment performance.

For edits and advanced saved-plan work, read https://planner.glacierfinancial.ca/docs/agents/tools.md. Preserve the original when trying a what-if. Access, pricing and ordinary resource limits are defined at https://planner.glacierfinancial.ca/pricing. Do not enable payment, connect an account or create a subscription without the person's authorization. Host support and approval requirements vary; protocol support does not guarantee a hosted assistant will accept the connection.
