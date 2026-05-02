# Integration Guide – Caveman Compression Prompts

Overview: which file to use where.

| Tool | File | Scope |
|---|---|---|
| Google Gemini | `caveman-global-instruction.md` | Global |
| Claude Desktop | `caveman-global-instruction.md` | Global |
| Claude Code (VS Code) | `CLAUDE.md` in repo root | Repo / workspace |
| VS Code Copilot (any model) | `.github/copilot-instructions.md` | Repo-wide |
| Any chat (one-time) | `caveman-chat-prompt.md` | Single chat |

---

## 1. Google Gemini – Custom Instructions (Global)

**Goal:** Caveman Compression applies to all chats.

1. Open [gemini.google.com](https://gemini.google.com)
2. Click your profile picture top right → **"Manage Gems"** (or Settings → Custom Instructions, depending on interface version)
3. Alternative: **"Create a Gem"** → create new gem
4. Paste the content from `caveman-global-instruction.md` (section "Instruction") into the **system instruction** field
5. Save

> **Tip:** If Gemini has no custom instructions field (depending on region), create a **personal Gem** with the system prompt and use it as your default chat.

---

## 2. Claude Desktop – Custom Instructions (Global)

**Goal:** Caveman Compression applies to all Claude conversations.

1. Open Claude Desktop
2. Click **"Claude"** top left → **"Settings"** (or `Cmd/Ctrl + ,`)
3. Go to **"Custom Instructions"** or **"Personalization"**
4. Paste the full content from `caveman-global-instruction.md` (section "Instruction") into the text field
5. Save and close

> **Note:** Custom Instructions in Claude Desktop apply to all new conversations. Existing chats are not affected.

---

## 3. Claude Code (VS Code Extension) – CLAUDE.md

**Goal:** Caveman Compression activates automatically for any project that has a `CLAUDE.md`.

Claude Code automatically reads `CLAUDE.md` from the workspace root on startup.

### For this project only

Create `CLAUDE.md` in the project root with the caveman rules content.

### For all projects globally (user-level)

Claude Code also supports a global `~/.claude/CLAUDE.md`:

```bash
mkdir -p ~/.claude
```

Then add the caveman rules to `~/.claude/CLAUDE.md`. Applies to all projects.

---

## 4. VS Code Copilot – `.github/copilot-instructions.md` (repo-wide)

**Goal:** Copilot (regardless of backend model: GPT-4o, Claude Sonnet, Gemini, etc.) follows the rules in every chat within the workspace.

VS Code Copilot automatically reads `.github/copilot-instructions.md` from the workspace root.

### Steps

1. Create `.github/` folder in project root (if not present)
2. Create `.github/copilot-instructions.md` with the caveman rules content
3. Commit the file — Copilot recognizes it immediately in the next chat

> **Applies to all Copilot models** in this workspace: GPT-4o, Claude Sonnet, Gemini etc. — system prompt injected automatically.

### For all workspaces globally (User Instructions)

VS Code Copilot also supports **user-level instructions**:

1. `Cmd/Ctrl + Shift + P` → **"Open User Instructions"** (or "GitHub Copilot: Open User Instructions")
2. Alternative: Settings → Extensions → GitHub Copilot → **"Custom Instructions"**
3. Paste the caveman rules content

> These apply to all workspaces regardless of `.github/copilot-instructions.md`.

---

## Recommendation

| Scenario | Best option |
|---|---|
| Caveman everywhere always | Global Custom Instructions in each tool |
| Only for specific project | `CLAUDE.md` / `.github/copilot-instructions.md` in repo |
| One-time chat | Paste `caveman-chat-prompt.md` at the start |
| All VS Code workspaces | VS Code User Instructions (Copilot) + `~/.claude/CLAUDE.md` |

**MCP vs. Instructions:** An MCP server is not worth it for Caveman Compression. MCP is designed for tools that call external APIs or fetch data. Caveman is a pure text processing rule → instructions file is faster, simpler, no server needed.
