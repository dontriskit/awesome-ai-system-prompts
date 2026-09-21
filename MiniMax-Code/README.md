# MiniMax Code

Terminal coding agent from MiniMax (`@minimax-ai/code` 0.4.12). Captured 2026-09-20.

**It ships three system prompts and picks one per surface** — three documents, not one with a
flag in it. `coding` swaps the whole `Deliverable Files` section for `Media Output`; `work` adds an
`Artifact Completion Contract` on top of that. All three declare the same 18 tools, byte-identical,
so they share one `tools.json`.

| `--prompt-mode` | file | chars |
|---|---|--:|
| `tui` (default) | [tui.md](./tui.md) | 14,674 |
| `coding` | [coding.md](./coding.md) | 16,054 |
| `work` | [work.md](./work.md) | 17,618 |

Not asked from the model: recorded off the wire by a local proxy while the CLI ran unmodified.
Each mode reproduces with one command:

```console
npm i -g orcareplay
git clone https://github.com/Continuum-AI-Corp/OrcaReplay && cd OrcaReplay
node capture/capture.mjs mcode --model deepseek/deepseek-v4-flash-free --prompt-mode tui --allow-failed
```

Bring-your-own-key shape: a BYOK run forces `disableMemory`, dropping a 3,381-character `# Memory`
section that a signed-in run carries. Scrubbed of home directory, username, git identity and uuids.

Source: [OrcaPromptVault](https://github.com/Continuum-AI-Corp/OrcaPromptVault/tree/main/MiniMax-Code)
