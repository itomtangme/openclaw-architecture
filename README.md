# 🏛️ OpenClaw Architecture

Hierarchical multi-agent architecture framework for [OpenClaw](https://openclaw.com) — a 6-layer org-chart structure with plug-and-play sub-systems, recursive delegation, and intelligent routing.

## What It Does

Turns OpenClaw into a structured multi-agent system where tasks flow through a hierarchy of specialized agents:

```
L0 Orchestrator (CEO)
├── L1-C Core Agents (sysadmin, full-power)
├── L1-D Domain Directors (pluggable departments)
│   ├── L2 Managers
│   │   ├── L3 Specialists
│   │   │   ├── L4 Operators
│   │   │   │   └── L5 Workers (ephemeral)
```

## Key Features

- **6-Layer Hierarchy** — L0 Orchestrator → L1 Director → L2 Manager → L3 Specialist → L4 Operator → L5 Worker
- **3 Mandatory Core Agents** — main (L0), sysadmin (L1-C), full-power (L1-C)
- **4-Tier Model System** — cost-efficient model allocation per layer
- **Task Affinity** — follow-up messages route back to the same child agent, preserving context
- **Result Caching** — shared cache prevents redundant delegation across branches
- **Graceful Degradation** — model outages trigger fallback chains, not hard failures
- **Health Monitoring** — heartbeat protocol with smart routing based on agent load
- **Plug-and-Play Departments** — add/remove domain-specific L1 directors anytime

## Installation

```bash
clawhub install openclaw-architecture
```

Or clone directly:

```bash
git clone https://github.com/itomtangme/openclaw-architecture.git ~/.openclaw/skills/openclaw-architecture
```

## Quick Start

1. Read `references/ARCHITECTURE.md` for the complete specification
2. Create shared directories in your main workspace:
   ```bash
   mkdir -p shared/cache/entries shared/artifacts templates
   ```
3. Copy templates from `assets/templates/` to your workspace
4. Bootstrap the 3 core agents (main, sysadmin, full-power)

See `SKILL.md` for detailed setup instructions.

## File Structure

```
├── SKILL.md                          # Skill entry point & setup guide
├── references/
│   └── ARCHITECTURE.md               # Complete v2.2 specification (source of truth)
└── assets/
    └── templates/
        ├── SOUL-template.md           # Template for new agent SOUL.md
        ├── MANIFEST-template.md       # Template for AGENT-MANIFEST.md
        ├── AGENTS-template.md         # Template for agent registry
        └── STATUS-template.md         # Template for STATUS.md dashboard
```

## Architecture at a Glance

| Aspect | Detail |
|--------|--------|
| Pre-installed agents | **3** (main, sysadmin, full-power) |
| Max hierarchy depth | **6 layers** (L0–L5) |
| Model strategy | **4-tier system** — children never exceed parent tier |
| Resilience | **Graceful degradation** — fallback chains, never hard-fail |
| Context continuity | **Task affinity** — follow-ups route to same child agent |
| Cache | **Shared cache** — prevents redundant delegation |
| Observability | **STATUS.md** — live dashboard, auto-updated |
| Ecosystem | **ClawHub** — one-command agent install |

## License

MIT

---

*Architecture v2.2*
