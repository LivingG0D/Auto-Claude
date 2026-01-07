# PROJECT KNOWLEDGE BASE

**Generated:** 2026-01-08
**Context:** Auto-Claude Renderer (UI)

## OVERVIEW
The React application running inside the Electron window. It manages the visual state, user interactions, and real-time updates from the agents.

## STRUCTURE
```
apps/frontend/src/renderer/
├── components/        # Reusable UI components
├── pages/             # Route-level views
├── hooks/             # Custom React hooks
├── stores/            # State management (Zustand)
└── lib/               # Utilities (utils, api)
```

## WHERE TO LOOK
| Task | Location | Notes |
|------|----------|-------|
| **Global State** | `stores/` | App-wide data (tasks, settings) |
| **UI Library** | `components/ui/` | shadcn/ui primitives |
| **Agent Terminal** | `components/terminal/` | Xterm.js integration |

## CONVENTIONS
- **Components**: Functional components with TypeScript.
- **State**: Zustand for global, `useState` for local.
- **Styles**: Tailwind utility classes. `cn()` utility for merging.

## ANTI-PATTERNS
- **Class Components**: Use functional + hooks.
- **Inline Styles**: Use Tailwind.
- **Complex Effects**: Keep `useEffect` simple and focused.
