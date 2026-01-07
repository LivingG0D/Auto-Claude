# AGENTS KNOWLEDGE BASE

**Location:** `apps/backend/agents/`
**Context:** Multi-agent autonomous coding system.

## OVERVIEW
The `agents` module handles the execution of AI agents that plan and implement software features. It uses a modular architecture where specialized agents (Planner, Coder) coordinate through a shared implementation plan, leveraging a dual-layer memory system for cross-session learning.

## STRUCTURE
```
agents/
├── tools_pkg/          # Custom MCP tools for agents (Memory, QA, Subtask, Progress)
├── base.py              # Shared constants (auto-continue delay, pause files)
├── session.py           # Core execution loop & post-session processing
├── coder.py             # Main autonomous agent loop (Coding phase)
├── planner.py           # Implementation planning & follow-up planning
├── memory_manager.py    # Dual-layer memory (Graphiti + File-based)
└── utils.py             # Git operations & implementation plan management
```

## AGENT LIFECYCLE
1. **Planning Phase**: `Planner` analyzes the spec and creates `implementation_plan.json` with sequential subtasks.
2. **Coding Phase**: `Coder` executes subtasks one-by-one in isolated sessions.
3. **Post-Session**: `session.post_session_processing` automatically:
   - Validates subtask completion status.
   - Records git commits as "good commits" for recovery.
   - Extracts insights/patterns and saves them to memory.
   - Updates Linear/Status managers.
4. **Recovery**: `RecoveryManager` tracks failed attempts and provides hints to agents in subsequent sessions to avoid repeating mistakes.

## TOOL DEFINITIONS
Agents have access to specialized tools defined in `tools_pkg/`:
- **Subtask**: Manage subtask status (complete, in_progress, failed).
- **Progress**: Track build completion and phase status.
- **Memory**: Store and retrieve semantic context (insights, patterns, gotchas).
- **QA**: Run validation suites and record results.

## MEMORY INTEGRATION
The system uses a **Dual-Layer Memory** strategy managed by `memory_manager.py`:
- **Primary (Graphiti)**: Semantic knowledge graph for cross-session context, pattern discovery, and learning.
- **Fallback (File-based)**: Local JSON storage in `spec_dir/memory/` for reliability when Graphiti is disabled.
- **Learning Loop**: Insights extracted after sessions are injected into the prompt of future sessions as "Known Gotchas" or "Learned Patterns".

## CONVENTIONS
- **Isolation**: Agents must work in the provided worktree/project directory.
- **Async-First**: All agent sessions and memory operations are `async`.
- **Status Updates**: Use `StatusManager` to keep the UI (`ccstatusline`) in sync with agent progress.
- **Facade Imports**: Import from `agents` (package root) for public API, or directly from modules for internal logic.

## ANTI-PATTERNS
- **Manual Plan Editing**: Directly editing `implementation_plan.json` while an agent is running (can cause race conditions).
- **Tool Bypassing**: Relying on agent compliance for memory updates instead of using `post_session_processing`.
- **Direct Anthropic Usage**: Bypassing `claude-agent-sdk` and the `core/client.py` factory.
