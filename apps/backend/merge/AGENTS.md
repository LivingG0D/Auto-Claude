# PROJECT KNOWLEDGE BASE

**Generated:** 2026-01-08
**Context:** Auto-Claude Auto-Merge

## OVERVIEW
Logic for intelligently merging feature branches (worktrees) back into the main codebase, resolving conflicts using AI when possible.

## STRUCTURE
```
apps/backend/merge/
├── auto_merger/       # Main merge orchestration
├── ai_resolver/       # LLM-based conflict resolution
└── file_evolution/    # History analysis for smarter merges
```

## WHERE TO LOOK
| Task | Location | Notes |
|------|----------|-------|
| **Merge Strategy** | `auto_merger/strategies/` | Recursive vs Squash vs Rebase |
| **Conflict Prompt** | `ai_resolver/prompts.py` | Guidance for AI resolution |
| **AST Analysis** | `semantic_analysis/` | Language-aware diffing |

## CONVENTIONS
- **Safety**: Always dry-run merges first.
- **Verification**: Run tests after merge before committing.
- **Fallback**: Bail to manual merge on high uncertainty.

## ANTI-PATTERNS
- **Blind Merges**: Merging without CI checks.
- **Destructive Ops**: Force pushing to shared branches.
