# PROJECT KNOWLEDGE BASE

**Generated:** 2026-01-08
**Context:** Auto-Claude Core Infrastructure

## OVERVIEW
The Core module handles the fundamental infrastructure: SDK client instantiation, authentication, security sandboxing, and configuration management.

## STRUCTURE
```
apps/backend/core/
├── client.py          # Claude SDK Client Factory
├── security.py        # Command Allowlist & Sandbox
├── auth.py            # OAuth Token Management
└── config.py          # Environment Configuration
```

## WHERE TO LOOK
| Task | Location | Notes |
|------|----------|-------|
| **Client Setup** | `client.py` | `create_client()` is the only valid entry point |
| **Command Whitelist** | `security.py` | `COMMAND_ALLOWLIST` definition |
| **Auth Logic** | `auth.py` | Token storage and refresh |

## CONVENTIONS
- **Security First**: Default deny for all commands. Explicit allowlist only.
- **Singleton Pattern**: Client should be created once per session context.
- **Environment**: All secrets via `.env`, loaded in `config.py`.

## ANTI-PATTERNS
- **Hardcoded Secrets**: Never commit tokens/keys.
- **Bypassing Security**: Executing commands without validation.
- **Custom Clients**: Instantiating `Anthropic()` directly.
