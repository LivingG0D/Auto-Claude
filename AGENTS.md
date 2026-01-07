# PROJECT KNOWLEDGE BASE

**Generated:** 2026-01-08
**Context:** Auto-Claude Autonomous Coding Framework

## OVERVIEW
Auto Claude is a multi-agent autonomous coding framework that builds software through coordinated AI agent sessions. It uses the `claude-agent-sdk` to orchestrate agents in isolated git worktrees, with a 3-layer security model (sandbox, fs restrictions, allowlist).

## STRUCTURE
```
X:\Auto-Claude/
├── apps/
│   ├── backend/           # Python core (agents, specs, security, CLI)
│   └── frontend/          # Electron/React desktop application
├── scripts/               # Build & release utilities
└── tests/                 # Integration test suite
```

## WHERE TO LOOK
| Task | Location | Notes |
|------|----------|-------|
| **Agent Logic** | `apps/backend/agents/` | Planner, Coder, QA implementations |
| **SDK Config** | `apps/backend/core/client.py` | `create_client()` factory & security hooks |
| **Memory** | `apps/backend/integrations/graphiti/` | Graphiti knowledge graph implementation |
| **UI Components** | `apps/frontend/src/renderer/` | React components (shadcn/ui based) |
| **Spec Pipeline** | `apps/backend/spec_runner.py` | Spec creation workflow logic |
| **E2E Testing** | `apps/frontend/e2e/` | Electron MCP based testing |

## CONVENTIONS
- **SDK Usage**: strict adherence to `claude-agent-sdk`. NEVER use `anthropic` library directly.
- **Paths**: Absolute paths preferred in tooling.
- **Frontend**: `react-i18next` MANDATORY for all user-facing text.
- **Versioning**: Use `scripts/bump-version.js` (patch/minor/major).
- **PRs**: Target `develop` branch (upstream), not `main`.

## ANTI-PATTERNS (THIS PROJECT)
- **Direct API Calls**: Bypassing `core/client.py` factory.
- **Hardcoded Strings**: UI text without translation keys.
- **Main Branch Pushes**: Direct pushes to `main` (must use PRs to `develop`).
- **Global Install**: Installing python deps globally (use `.venv`).

## COMMANDS
```bash
# Backend Setup
cd apps/backend && uv venv && uv pip install -r requirements.txt

# Frontend Setup
cd apps/frontend && npm install

# Run Spec (CLI)
python apps/backend/run.py --spec 001

# Run App (Dev)
cd apps/frontend && npm run dev
```

## NOTES
- **Security**: The system caches security profiles in `.auto-claude-security.json`. If commands are blocked, check `apps/backend/core/security.py`.
- **Worktrees**: All active development happens in `.worktrees/`. The main working directory should stay clean.
