# Agent Manifest

## Identity
- **ID**: {{AGENT_ID}}
- **Name**: {{AGENT_NAME}}
- **Type**: {{AGENT_TYPE}} ({{LAYER_CODE}})
- **Parent**: {{PARENT_ID}}
- **Version**: 1.0.0

## Capabilities
- {{CAPABILITY_1}}
- {{CAPABILITY_2}}
- {{CAPABILITY_3}}

## Accepts (Input Contract)
- Natural language task descriptions related to {{DOMAIN}}
- Structured parameters: {{PARAMETER_DESCRIPTION}}

## Produces (Output Contract)
- {{OUTPUT_1}}
- {{OUTPUT_2}}

## Sub-Agents
| ID | Type | Persistence | Description |
|----|------|-------------|-------------|
| — | — | — | (none yet — add as needed) |

## Model Requirements
- Minimum Tier: {{MIN_TIER}}
- Recommended Tier: {{REC_TIER}}

## Dependencies
- {{DEPENDENCY_1}}

## Escalation Policy
- Escalates to: {{PARENT_ID}}
- Escalation triggers:
  - Task outside declared capabilities
  - Repeated failures (2+ retries)
  - Resource or budget exhaustion
  - Explicit user request to escalate
