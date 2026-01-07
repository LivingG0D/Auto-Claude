# PROJECT KNOWLEDGE BASE

**Generated:** 2026-01-08
**Context:** Auto-Claude Integrations

## OVERVIEW
Connectors for external services and tools. The primary integration is Graphiti (Memory), with optional support for Linear (Tracking) and GitHub.

## STRUCTURE
```
apps/backend/integrations/
├── graphiti/          # Knowledge Graph Memory
├── linear/            # Issue Tracking Sync
└── github/            # PR/Issue Automation
```

## WHERE TO LOOK
| Task | Location | Notes |
|------|----------|-------|
| **Memory Queries** | `graphiti/queries_pkg/` | Semantic search & graph traversal |
| **Issue Sync** | `linear/client.py` | Bi-directional sync logic |
| **PR Automation** | `github/client.py` | GH API wrapper |

## CONVENTIONS
- **Abstraction**: All providers must follow a common interface.
- **Resilience**: Handle API rate limits and failures gracefully.
- **Async**: All network calls must be asynchronous.

## ANTI-PATTERNS
- **Vendor Lock-in**: Hardcoding provider-specific logic in core agents.
- **Blocking Calls**: Sync HTTP requests.
