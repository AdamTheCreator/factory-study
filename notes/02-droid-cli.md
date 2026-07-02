# 02 — Droid CLI Deep Dive

The CLI is what you'll live in and demo most. Build real muscle memory here — in an SE
interview, fumbling the tool is worse than fumbling a fact.

## Install & launch

```bash
curl -fsSL https://app.factory.ai/cli | sh   # install
droid                                          # interactive REPL in current dir
droid "refactor the auth module to use async"  # REPL seeded with a prompt
droid update                                   # upgrade the CLI
```

The UX deliberately resembles Claude Code (modes via Shift+Tab, slash commands, a REPL).
If you know Claude Code, you'll be productive in minutes — *say that in the interview, it
shows you understand the category.*

## The three modes (Shift+Tab cycles them)

1. **Default / manual** — Droid proposes; you approve each action. Safest, slowest.
2. **Auto** — Droid executes within the current autonomy level without asking each step.
3. **Plan / Spec** — Droid plans the work (as a spec) before touching code. (→ note 04)

## Autonomy levels — the safety dial (memorize this table)

Set with `--auto <level>` on the CLI, or cycle live with **Ctrl+L**.

| Level | Flag | What Droid may do without asking |
|-------|------|----------------------------------|
| **default** | *(none)* | Read-only: file reads, git diffs, inspection. |
| **low** | `--auto low` | Safe edits: create/format files, non-destructive commands. |
| **medium** | `--auto medium` | Typical dev: install deps, build, run tests, local commits. |
| **high** | `--auto high` | Broad ops: git push, deploy, orchestration. |
| **(unsafe)** | `--skip-permissions-unsafe` | Everything, no guardrails. **Sandbox/CI only.** |

**SE framing:** autonomy levels are how Factory makes "let an agent loose on our repo"
acceptable to a security team. Start low, escalate as trust builds. Never demo
`--skip-permissions-unsafe` on a customer's real machine.

## Key flags (the ones worth knowing)

| Flag | Purpose |
|------|---------|
| `-m, --model <id>` | Pick the model for the run. |
| `-r, --reasoning-effort <off\|low\|medium\|high>` | Trade speed vs. depth. |
| `--spec-model <id>` | Use a different (often stronger) model just for spec planning. |
| `--auto <low\|medium\|high>` | Set autonomy. |
| `--use-spec` | Start in spec/planning mode. |
| `--mission` | Multi-agent orchestration (Mission Mode). |
| `-w, --worktree [name]` | Isolate work in a git worktree (great for parallel/unsafe runs). |
| `--enabled-tools` / `--disabled-tools` | Force-allow or block specific tools. |
| `--append-system-prompt <text>` | Inject custom instructions. |
| `--cwd <path>` | Run against a different working directory. |

## Headless execution — `droid exec`

The Level-300 capability. Runs Droid non-interactively for CI/automation.

```bash
droid exec "run the test suite and fix any failures"
droid exec -f prompt.md                       # prompt from a file
droid exec --auto high "run tests, commit, push to main"   # full automation
droid exec -o json "summarize open TODOs"     # machine-readable output
```

Output formats: `text`, `json`, `stream-json`, `stream-jsonrpc`. Use JSON when wiring Droid
into a pipeline that consumes its results. (Full headless patterns → note 04.)

## Sessions (continuity matters)

```bash
droid --resume [sessionId]    # restore a previous session
droid --fork <sessionId>      # branch a session into a copy
droid search "query"          # search across local sessions/docs
```

In-REPL: `/new`, `/sessions`, `/fork`, `/rename`, `/favorite`.

## Slash commands (in the REPL)

**Workflow:** `/review` (code review), `/missions` (multi-agent), `/skills` (reusable skills),
`/bug [title]` (file a bug w/ session data).
**Config:** `/model`, `/settings`, `/mcp`, `/plugins`, `/language <locale>`.
**Info:** `/context` (token breakdown — *use this to teach customers about context*),
`/cost` (usage), `/status` (current config), `/help`.

## Keyboard shortcuts (demo smoothness)

- **Shift+Tab** — cycle modes · **Ctrl+L** — cycle autonomy · **Ctrl+N** — cycle models ·
  **Tab** — cycle reasoning effort.
- **Ctrl+O** — toggle detailed transcript · **Ctrl+C ×2** — cancel/exit.
- **`!`** — bash mode (run a shell command directly) · **`@`** — fuzzy file autocomplete ·
  **`?`** — help popup (empty input).
- Editing: **Ctrl+A** line start, **Ctrl+U** delete-to-start, **Ctrl+K** delete-to-end,
  **Ctrl+W** delete word, **Shift+Enter** newline.

## Extensibility from the CLI

```bash
droid plugin install <plugin>        # add a plugin
droid mcp add <name> <url>           # register an MCP server
```

(MCP + integrations are how you pull in GitHub/Jira/Sentry/Slack/Notion context — see note 03/05.)

## Hands-on rep (do this on the trial)

1. `droid` in a repo → `/context` to see what it loaded.
2. Ask: *"Explain this codebase's architecture and entry points."*
3. Fix a small bug at `--auto low`, review the diff, then redo at `--auto medium`.
4. Run the same task headless: `droid exec -o json "fix the failing test in X"`.
5. Practice the shortcut dance (Shift+Tab / Ctrl+L / Ctrl+N) until it's automatic.

## Self-check (Level 200)

- [ ] I can cycle modes/autonomy/models without looking.
- [ ] I can explain each autonomy level and *why* it exists to a security buyer.
- [ ] I ran `droid exec` headless and got JSON output.
- [ ] I can resume/fork a session and explain why that matters for long tasks.

Sources: [CLI reference](https://docs.factory.ai/reference/cli-reference) ·
[Droid CLI overview](https://factory.ai/product/cli) ·
[Droid Exec docs](https://docs.factory.ai/cli/droid-exec)
