# Clawdbot System Prompts

[Clawdbot](https://github.com/clawdbot/clawdbot) is an open-source AI agent platform that runs on messaging channels (WhatsApp, Discord, Telegram, Slack, etc.) and provides agentic capabilities through a modular prompt architecture.

## Architecture Overview

Unlike monolithic system prompts, Clawdbot uses a **modular file-based approach** where different aspects of the agent's behavior are defined in separate files:

| File | Purpose |
|------|---------|
| `SOUL.md` | Personality, tone, voice characteristics |
| `AGENTS.md` | Operational rules, approval flows, task patterns |
| `IDENTITY.md` | Identity boundaries, privacy rules, context awareness |
| `USER.md` | User-specific configuration (not included - template only) |
| `TOOLS.md` | Environment configuration, service status |
| `HEARTBEAT.md` | Scheduled check routines |

This separation enables:
- **Composability**: Swap personality without changing rules
- **Maintainability**: Update one aspect without touching others
- **Clarity**: Each file has a single responsibility
- **Version control**: Track changes to specific behaviors

## Key Design Patterns

### 1. Persona Separation (SOUL.md)
The personality lives in its own file, inspired by literary characters (in this case, the Heart of Gold's shipboard computer from Hitchhiker's Guide). This keeps tone consistent while allowing operational rules to evolve independently.

### 2. Approval Hierarchies (AGENTS.md)
Explicit categorization of actions:
- **Do without asking**: Read operations, drafts, research
- **Get approval before**: External sends, commitments, publishing
- **Never do**: Absolute boundaries

### 3. Context-Aware Privacy (IDENTITY.md)
Different rules for different conversation contexts:
- Owner's self-chat: Full access
- Group chats: Limited disclosure
- DMs with others: Respond only to specific questions

### 4. Heartbeat Pattern (HEARTBEAT.md)
Scheduled proactive checks with clear decision trees and escalation rules.

## Files

- [SOUL.md](SOUL.md) - Personality and voice
- [AGENTS.md](AGENTS.md) - Operational rules
- [IDENTITY.md](IDENTITY.md) - Identity and privacy boundaries

## Usage

These files are placed in the agent's workspace directory and automatically loaded as context. The agent reads them on session start and follows their guidance.

```
workspace/
├── SOUL.md
├── AGENTS.md
├── IDENTITY.md
├── USER.md (user-specific, not tracked)
├── TOOLS.md
├── HEARTBEAT.md
└── memory/
    └── YYYY-MM-DD.md (daily logs)
```

## License

MIT - Same as Clawdbot
