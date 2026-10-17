# Domain docs

This repo uses a single-context layout:

- `GLOSSARY.md` at the repo root defines domain terms.
- `docs/adr/` holds architecture decision records.

## Before exploring

Read the glossary and ADRs relevant to the area being explored.
If these files do not exist, proceed silently. Domain-modeling
creates them lazily when terms or decisions are resolved.

## Use the glossary's vocabulary

Use defined terms in issue titles, proposals, hypotheses, and tests.
If a concept is missing, reconsider the wording or note the gap
for domain-modeling.

## Surface ADR conflicts

If a proposal contradicts an existing ADR, identify the ADR and
explain why the decision should be reconsidered.
