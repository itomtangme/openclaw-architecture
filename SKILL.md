---
name: openclaw-architecture
description: >
  Hierarchical multi-agent architecture framework for OpenClaw. Defines a 6-layer
  org-chart structure (L0 Orchestrator → L1 Director → L2 Manager → L3 Specialist →
  L4 Operator → L5 Worker) with plug-and-play sub-systems, recursive delegation,
  graceful degradation, result caching, health monitoring, and an observability dashboard.
  Use when: (1) setting up a new OpenClaw instance with hierarchical agent management,
  (2) adding or removing domain-specific sub-systems (departments), (3) provisioning
  new agents at any layer, (4) checking or updating the agent org structure,
  (5) bootstrapping the architecture on a fresh install. NOT for: single-agent setups
  that don't need hierarchy, or modifying OpenClaw core code.
---

# OpenClaw Hierarchical Architecture v2.2

## Quick Start

Bootstrap the full architecture on a fresh or existing OpenClaw install:

1. Read `references/ARCHITECTURE.md` for the complete specification
2. Create required directories in the main workspace:
   ```
   mkdir -p shared/cache/entries shared/artifacts templates
   ```
3. Copy templates from `assets/templates/` to `<workspace>/templates/`
4. Write `ARCHITECTURE.md` into the main workspace (copy from `references/`)
5. Initialize `STATUS.md` in the main workspace (copy from `assets/templates/STATUS-template.md`)
6. Update `AGENTS.md` in the main workspace to the v2.2 registry format
7. Add `AGENT-MANIFEST.md` to each existing agent workspace

## Architecture Overview

### 6-Layer Hierarchy

| Layer | Role | Spawns Children? | Persistence |
|-------|------|-------------------|-------------|
| L0 — Orchestrator | CEO, routes & synthesizes | ✅ → L1 | Permanent |
| L1 — Director | Department head | ✅ → L2 | Permanent |
| L2 — Manager | Sub-domain coordinator | ✅ → L3 | Permanent / Session |
| L3 — Specialist | Focused expert | ✅ → L4 | Session / On-demand |
| L4 — Operator | Task executor | ✅ → L5 | On-demand |
| L5 — Worker | Atomic, ephemeral | ❌ | One-shot |

### 3 Mandatory Core Agents

Every installation requires exactly these three:

- **L0: Orchestrator (main)** — entry point, routing, synthesis
- **L1-C: System Admin (sysadmin)** — infrastructure, config, agent provisioning
- **L1-C: Full Power (full-power)** — emergency override, explicit invocation only

Everything else is pluggable.

### 4-Tier Model System

| Tier | Purpose | Typical Layer |
|------|---------|---------------|
| Tier-1 | Max intelligence | L0, L1 |
| Tier-2 | Strong capability | L1-D, L2 |
| Tier-3 | Fast & capable | L3, L4 |
| Tier-4 | Cheapest | L4, L5 |

Rule: children inherit or downgrade tier. Never upgrade beyond parent.

## Provisioning a New Agent

When adding a department (L1-D) or specialist (L2/L3):

1. Read `references/ARCHITECTURE.md` sections 5, 6, 15, 16
2. Create workspace: `/root/.openclaw/workspace-<agent-id>/`
3. Copy and customize templates from `<workspace>/templates/`:
   - `SOUL-template.md` → `SOUL.md`
   - `MANIFEST-template.md` → `AGENT-MANIFEST.md`
   - `AGENTS-template.md` → `AGENTS.md`
4. Write `USER.md`, `TOOLS.md`, `IDENTITY.md`
5. Add agent to `openclaw.json` via safe-config
6. Update main workspace `AGENTS.md` registry
7. Gateway restart
8. Dispatch test task to verify

## Communication Protocol

Delegation, results, and escalation follow structured message formats.
See `references/ARCHITECTURE.md` section 9 for full protocol specification.

Key rules:
- **No lateral shortcuts** — cross-branch communication goes through nearest common ancestor
- **Fail-up** — failed agents escalate to parent, never fail silently
- **Depth tracking** — every delegation includes depth counter; refuse at L5

## Health & Observability

- Each permanent agent (L0–L2) maintains `HEARTBEAT-STATUS.md`
- L0 aggregates into `STATUS.md` dashboard in main workspace
- Smart routing: check agent health before dispatching
- See `references/ARCHITECTURE.md` sections 10, 13

## Result Caching

- Location: `shared/cache/` in main workspace
- Check cache before dispatching; cache results after completion
- Only L0–L2 can write to cache
- TTL-based expiry with manual invalidation
- See `references/ARCHITECTURE.md` section 12

## Graceful Degradation

- Model provider outage → automatic tier downgrade via fallback chain
- Agent failure → parent handles directly + escalation
- Auto-recovery on heartbeat when providers return
- See `references/ARCHITECTURE.md` section 14

## File Reference

- `references/ARCHITECTURE.md` — complete v2.2 specification (the source of truth)
- `assets/templates/SOUL-template.md` — template for new agent SOUL.md
- `assets/templates/MANIFEST-template.md` — template for AGENT-MANIFEST.md
- `assets/templates/AGENTS-template.md` — template for agent registry
- `assets/templates/STATUS-template.md` — template for STATUS.md dashboard
