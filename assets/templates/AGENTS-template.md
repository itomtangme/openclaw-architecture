# AGENTS.md — {{AGENT_NAME}} Sub-Agent Registry

## Architecture
- Version: 2.2
- This Agent: {{AGENT_ID}} ({{LAYER_CODE}})
- Parent: {{PARENT_ID}}

## Sub-Agent Tree
| ID | Name | Type | Layer | Model Tier | Status |
|----|------|------|-------|------------|--------|
| — | — | — | — | — | (none yet) |

## Routing Rules
Route tasks to the appropriate sub-agent based on domain match.
If no sub-agent matches, handle directly or escalate to parent.

## Handoff Protocol
When delegating:
```
[TASK FROM: {{AGENT_ID}} (L{{LAYER_NUMBER}}) → <child-id> (L<n+1>)]
```

When receiving results:
```
[RESULT FROM: <child-id> (L<n+1>) → {{AGENT_ID}} (L{{LAYER_NUMBER}})]
```
