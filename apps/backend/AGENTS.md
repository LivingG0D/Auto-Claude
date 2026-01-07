# PROJECT KNOWLEDGE BASE

**Generated:** 2026-01-08
**Context:** Auto-Claude Backend (Python)

## OVERVIEW
The backend is the brain of Auto Claude, hosting all agent logic, spec pipelines, and security controls. It runs as a CLI or a subprocess of the Electron app.

## STRUCTURE
```
apps/backend/
├── core/              # SDK Client, Security, Auth
├── agents/            # Agent implementations (Planner, Coder)
├── spec/              # Spec creation pipeline
├── integrations/      # External services (Graphiti, Linear)
├── merge/             # Auto-merge logic
└── runners/           # Task execution runners
```

## WHERE TO LOOK
| Task | Location | Notes |
|------|----------|-------|
| **Agent Logic** | `agents/` | Implementation of autonomous agents |
| **Spec Pipeline** | `spec/pipeline/` | Dynamic phases for spec creation |
| **Security** | `core/security.py` | Command allowlist and sandbox |
| **Memory** | `integrations/graphiti/` | Knowledge graph integration |

## CONVENTIONS
- **Dependency Management**: Use `uv` for fast package management.
- **Type Safety**: strict `mypy` compliance. Pydantic v2 for data models.
- **Async**: `asyncio` for all I/O bound operations.
- **Error Handling**: Use `core.exceptions` for typed errors.

## ANTI-PATTERNS
- **Sync I/O**: Blocking operations in agent loops.
- **Global State**: Mutable module-level state (use Dependency Injection).
- **Direct API**: Bypassing `ClaudeSDKClient`.
