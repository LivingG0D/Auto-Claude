# PROJECT KNOWLEDGE BASE: FRONTEND

**Context:** Electron & React Desktop UI

## OVERVIEW
The frontend is an Electron-based desktop application built with React, Tailwind CSS, and shadcn/ui, providing a graphical interface for orchestrating autonomous agents.

## STRUCTURE
```
apps/frontend/src/
├── main/             # Electron main process (PTY, Python Env, IPC Setup)
├── preload/          # ContextBridge API definitions
├── renderer/         # React application (Features, Stores, Hooks)
│   ├── components/   # UI components (shadcn/ui based)
│   ├── stores/       # Zustand state management
│   └── hooks/        # Custom React hooks (useIpc, useVirtualizedTree)
├── shared/           # Types and constants shared across processes
└── e2e/              # Playwright-based Electron testing
```

## WHERE TO LOOK
| Task | Location | Notes |
|------|----------|-------|
| **IPC Handlers** | `src/main/ipc-setup.ts` | Entry point for all main process listeners |
| **Terminal Logic** | `src/main/terminal/` | PTY management and terminal lifecycle |
| **Frontend API** | `src/preload/api/` | TypeScript definitions for the `window.api` bridge |
| **Global State** | `src/renderer/stores/` | Zustand stores (Project, Task, Terminal) |
| **Localization** | `src/renderer/` | `i18next` integration for multi-language support |
| **E2E Flows** | `e2e/flows.e2e.ts` | Critical user path testing |

## CONVENTIONS
- **Electron IPC**: All main-process calls MUST go through `src/preload/api/`. NEVER use `ipcRenderer` directly in components; use `useIpc()` or store abstractions.
- **State Management**: Use **Zustand** for global state. Keep stores small and feature-focused.
- **Styling**: Tailwind CSS + shadcn/ui. Custom animations via `motion` (framer-motion).
- **Native Modules**: Native dependencies like `@lydell/node-pty` require `npm run rebuild` on environment changes.
- **Python Integration**: The UI bundles its own Python runtime. See `src/main/python-env-manager.ts`.

## ANTI-PATTERNS
- **Prop Drilling**: Over-using props instead of Zustand stores for shared application state.
- **Main Thread Bloat**: Performing heavy FS or parsing operations in the main process thread (use worker patterns or async non-blocking logic).
- **Direct Node Access**: Enabling `nodeIntegration` or bypassing `contextBridge` security.
- **Unmocked Tests**: Running renderer tests without proper IPC/Electron mocks.
