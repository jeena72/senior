# Claude Code for Senior/Lead Python Engineers

[← Back to README](README.md)

A practical guide to AI-assisted development with Claude Code. Written for engineers who already know how to build software and want to know how to drive an agent well — not a marketing overview. Claims are based on the official docs at [code.claude.com/docs](https://code.claude.com/docs) (as of August 2026); links for re-checking are at the end.

## Table of contents

1. [What Claude Code is and how the agentic loop works](#1-what-claude-code-is-and-how-the-agentic-loop-works)
2. [Talking to Claude effectively](#2-talking-to-claude-effectively)
3. [Planning: plan mode, decomposition, and reasoning depth](#3-planning-plan-mode-decomposition-and-reasoning-depth)
4. [CLAUDE.md best practices](#4-claudemd-best-practices)
5. [README vs CLAUDE.md](#5-readme-vs-claudemd)
6. [Permission modes and safety](#6-permission-modes-and-safety)
7. [Remote usage: web, cloud, GitHub, mobile](#7-remote-usage-web-cloud-github-mobile)
8. [Workflow features worth knowing](#8-workflow-features-worth-knowing)
9. [Anti-patterns](#9-anti-patterns)
10. [Interview-ready summary](#10-interview-ready-summary)

## 1. What Claude Code is and how the agentic loop works

Claude Code is an **agentic coding tool**: it reads your codebase, edits files, runs commands, and integrates with your dev tools. It is not autocomplete and not a chat window with a copy button.

**Surfaces** — all run the same engine, so your `CLAUDE.md`, settings, and MCP servers work everywhere:

| Surface | How to get it | Best for |
|---|---|---|
| Terminal CLI | `curl -fsSL https://claude.ai/install.sh \| bash` (macOS/Linux/WSL) | Full-featured default |
| VS Code / Cursor | "Claude Code" extension | Inline diffs, @-mentions, plan review |
| JetBrains (PyCharm) | Marketplace plugin (requires the CLI) | IDE diff viewing, selection context |
| Desktop app | macOS / Windows / Linux (beta) | Visual diffs, parallel sessions, scheduled tasks |
| Web | [claude.ai/code](https://claude.ai/code) | Long-running cloud tasks, repos you don't have locally |
| Mobile | Claude app for iOS/Android | Monitoring and steering cloud sessions |

**The agentic loop** has three phases that blend together: **gather context → take action → verify results**, repeating until the task is done. You are inside this loop — you can interrupt at any point.

Concretely, "fix the failing tests" becomes: run the suite → read errors → search for source files → read them → edit → re-run tests. Each tool result feeds the next decision.

**Why this matters:** you are not reviewing a single generated blob. You are supervising a loop. Everything in this guide is about (a) making the loop's inputs precise and (b) giving the loop a way to close itself without you.

## 2. Talking to Claude effectively

### Be specific: name the file, the scenario, the constraint

```text
❌ "add tests for foo.py"

✅ "write a test for foo.py covering the edge case where the user is
    logged out. avoid mocks."
```

**Why:** the vague version forces Claude to guess scope, test style, and which cases matter. Every guess is a coin flip you pay for in review time. The specific version removes three decisions.

### Point at existing patterns instead of describing them

```text
❌ "add a repository class for orders"

✅ "look at how existing repositories are implemented in src/repos/.
    UserRepository is a good example. follow that pattern for an
    OrderRepository. build from scratch without adding new libraries."
```

**Why:** Claude infers conventions far more reliably from one concrete example in your repo than from your prose description of the convention. This also prevents it from pulling in a dependency you don't want.

### Describe the symptom, the likely location, and what "fixed" means

```text
❌ "fix the login bug"

✅ "users report that login fails after session timeout. check the auth
    flow in src/auth/, especially token refresh. write a failing test
    that reproduces the issue, then fix it"
```

**Why:** "write a failing test first" converts a subjective judgment ("is it fixed?") into a binary signal the agent can read itself.

### Always give Claude something it can verify

> Claude stops when the work looks done. Without a check it can run, "looks done" is the only signal available, and you become the verification loop.

```text
✅ "implement validate_email(). test cases: user@example.com → True,
    'invalid' → False, user@.com → False. run pytest after implementing
    and iterate until it passes."
```

Escalating levels of enforcement:

- **In one prompt** — "run the tests and fix failures" (works today, zero setup).
- **Across a session** — `/goal` sets a condition; a separate evaluator re-checks after every turn.
- **As a deterministic gate** — a `Stop` hook runs your check as a script and blocks the turn from ending until it passes.
- **By a second opinion** — a verification subagent grades the diff in a fresh context, so the agent doing the work isn't the one grading it.

**Why:** without a check, every mistake waits for a human to notice. With one, the loop closes on its own and you can walk away.

### Provide rich context, cheaply

- `@src/api/handlers.py` — Claude reads the file before responding, instead of guessing where code lives.
- Paste screenshots/images directly (drag and drop).
- Pipe data: `cat error.log | claude -p "find the anomaly"`.
- Prefer CLI tools (`gh`, `aws`, `kubectl`) over describing external state — they are the most context-efficient way to reach external services.

### Interrupt and correct early

| Action | Effect |
|---|---|
| `Esc` | Stops Claude immediately; context is preserved so you can redirect |
| Type + `Enter` while it works | Sends a correction *without* stopping the running tool |
| `Esc Esc` or `/rewind` | Rewind menu: restore conversation, code, or both |
| `/clear` | Reset context between unrelated tasks |

**Rule of thumb from the docs:** if you have corrected Claude more than twice on the same issue, `/clear` and restart with a better prompt. A clean session with a good prompt almost always beats a long session full of failed approaches.

**Why:** failed attempts stay in the context window and actively bias the next attempt toward the same dead end.

### For big features, make Claude interview you

```text
I want to build [brief description]. Interview me in detail using the
AskUserQuestion tool.

Ask about technical implementation, UI/UX, edge cases, concerns, and
tradeoffs. Don't ask obvious questions, dig into the hard parts I might
not have considered.

Keep interviewing until we've covered everything, then write a complete
spec to SPEC.md.
```

Then **start a fresh session** to implement `SPEC.md`.

**Why:** the interview surfaces decisions you hadn't made yet, and the spec is a durable artifact. The fresh session gets clean context focused entirely on implementation, with none of the exploratory back-and-forth.

## 3. Planning: plan mode, decomposition, and reasoning depth

### Plan mode

Claude reads files and runs exploratory commands but **does not edit your source**. Edits stay blocked until you approve a plan.

```bash
claude --permission-mode plan      # start in plan mode
```

| Control | Effect |
|---|---|
| `Shift+Tab` | Cycle permission modes until the status bar shows `⏸ plan mode on` |
| `/plan` prefix | Apply plan mode to a single prompt |
| `Ctrl+G` | Open the proposed plan in your `$EDITOR` and edit it directly |

The recommended four-phase workflow:

```text
1. Explore  (plan mode)
   "read src/auth and understand how we handle sessions and login.
    also look at how we manage environment variables for secrets."

2. Plan     (plan mode)
   "I want to add Google OAuth. What files need to change?
    What's the session flow? Create a plan."

3. Implement (after approving; Shift+Tab out)
   "implement the OAuth flow from your plan. write tests for the
    callback handler, run the test suite and fix any failures."

4. Commit
   "commit with a descriptive message and open a PR"
```

**Approving a plan** offers: *Yes, and use auto mode* / *Yes, manually approve edits* / *No, keep planning*.

**When to skip planning:** the docs are explicit — "If you could describe the diff in one sentence, skip the plan." Plan mode adds overhead. Use it when the approach is uncertain, the change spans multiple files, or you're unfamiliar with the code.

**Why plan mode beats just asking for a plan:** in plan mode source edits are *mechanically* blocked, not merely discouraged. And you get to edit the plan (`Ctrl+G`) before a single line changes — cheaper than reviewing a wrong 800-line diff.

Make it the project default for risky repos:

```json
// .claude/settings.json
{ "permissions": { "defaultMode": "plan" } }
```

### Reasoning depth — what's actually current

⚠️ **Training-data trap.** The old "think / think hard / think harder / ultrathink" ladder is **no longer a ladder**. Current docs: include `ultrathink` anywhere in your prompt to request deeper reasoning on that turn; other phrases such as "think", "think hard", and "think more" are passed through as ordinary prompt text and are not recognized as keywords.

The real control is the **effort level**:

| Level | When |
|---|---|
| `low` | Short, scoped, latency-sensitive, not intelligence-sensitive |
| `medium` | Cost-sensitive work that can trade off some intelligence |
| `high` | Default on nearly every model; balances tokens and intelligence |
| `xhigh` | Deeper reasoning at higher token spend |
| `max` | Demanding tasks; diminishing returns, prone to overthinking |
| `ultracode` | Claude Code setting: plans a dynamic workflow per task at `xhigh` |

```bash
claude --effort xhigh          # for one session
/effort                        # interactive slider mid-session
/effort auto                   # back to the model default
/model                         # switch model; effort slider is here too
```

Effort can also be set per skill/subagent via `effort:` frontmatter, in `settings.json` as `effortLevel`, or via `CLAUDE_CODE_EFFORT_LEVEL` (which outranks everything else).

**Why this matters in an interview:** knowing that `ultrathink` is the only surviving keyword, and that effort levels are the primary control, is a clean signal you're working from current docs rather than 2024 blog posts.

## 4. CLAUDE.md best practices

`CLAUDE.md` is loaded into the context window at the **start of every session**. That is its power and its cost.

### Where files live (load order, broadest → most specific)

| Scope | Location | Shared with |
|---|---|---|
| Managed policy | `/Library/Application Support/ClaudeCode/CLAUDE.md` (macOS), `/etc/claude-code/CLAUDE.md` (Linux/WSL), `C:\Program Files\ClaudeCode\CLAUDE.md` | Whole org; cannot be excluded |
| User | `~/.claude/CLAUDE.md` | Just you, all projects |
| Project | `./CLAUDE.md` or `./.claude/CLAUDE.md` | Team, via git |
| Local | `./CLAUDE.local.md` | Just you; add to `.gitignore` |

Files are **concatenated, not overridden** — root-down, so instructions nearest your working directory are read last. Subdirectory `CLAUDE.md` files load **on demand** when Claude reads files in those directories.

Bootstrap with `/init` (analyzes the codebase, generates a starter; suggests improvements rather than overwriting if one exists). Verify with `/context` → **Memory files**. Browse/edit with `/memory`.

### What belongs in it — and what doesn't

| ✅ Include | ❌ Exclude |
|---|---|
| Bash commands Claude can't guess | Anything Claude can figure out by reading code |
| Code style rules that differ from defaults | Standard language conventions Claude already knows |
| Testing instructions and preferred test runners | Detailed API docs (link instead) |
| Repo etiquette (branch naming, PR conventions) | Information that changes frequently |
| Architectural decisions specific to your project | Long explanations or tutorials |
| Environment quirks (required env vars) | File-by-file descriptions of the codebase |
| Common gotchas and non-obvious behaviors | Self-evident advice like "write clean code" |

**Size target: under 200 lines.** The test for every line: *"Would removing this cause Claude to make mistakes?"* If not, cut it.

> Bloated CLAUDE.md files cause Claude to ignore your actual instructions!

**Why:** CLAUDE.md is delivered as context, not enforced configuration. Attention is finite — a 600-line file means important rules compete with filler and lose. If Claude keeps violating one rule despite it being written down, the file is probably too long, not the rule too weak. Add `IMPORTANT` to *one* line only; emphasize many and none stand out.

### A realistic Python `CLAUDE.md` (uv + ruff + pytest)

```markdown
# Commands

- Install/sync deps: `uv sync --all-extras`
- Run anything: `uv run <cmd>` (never bare `python` or `pip`)
- Tests: `uv run pytest -q`
- Single test: `uv run pytest tests/test_orders.py::test_refund -q`
- Lint + fix: `uv run ruff check --fix .`
- Format: `uv run ruff format .`
- Types: `uv run mypy src/`
- Migrations: `uv run alembic upgrade head`

# Workflow

- After a series of code changes, run: ruff check, mypy, then pytest.
- Prefer running the single relevant test over the full suite.
- IMPORTANT: never edit files under `src/api/_generated/` — they are
  regenerated by `uv run python -m tools.gen_openapi`.

# Conventions

- Python 3.12. Full type annotations on all public functions.
- Pydantic v2 models for all I/O boundaries; dataclasses internally.
- Async everywhere in `src/api/`; sync-only code lives in `src/jobs/`.
- Custom exceptions subclass `app.errors.AppError`; never raise bare
  `Exception`.
- Tests use real Postgres via testcontainers. Do not add `unittest.mock`
  for database access.

# Architecture pointers

- HTTP handlers: `src/api/routers/` (thin — no business logic)
- Business logic: `src/services/`
- Persistence: `src/repos/` (SQLAlchemy 2.0 style, no legacy Query API)

# Gotchas

- `pytest` needs `DATABASE_URL` set; `.env.test` is loaded by conftest.
- Celery tasks must be imported in `src/jobs/__init__.py` or they are
  silently unregistered.
- `uv.lock` is committed. Never run `pip install`.
```

**Why this file works:** every line is either a command Claude cannot guess, a convention that differs from Python defaults, or a gotcha that would cost a wasted turn. There is no "this is a FastAPI project" prose — Claude derives that in one `Read`.

### Keep it small as it grows

- **`.claude/rules/`** — split topics into files. Add `paths:` frontmatter so a rule loads only when Claude touches matching files:

  ```markdown
  ---
  paths:
    - "src/api/**/*.py"
  ---
  # API rules
  - Every endpoint validates input with a Pydantic model.
  - Use the standard error envelope from `app.errors.to_response`.
  ```

  **Why:** a 40-line API rulebook costs zero context when you're editing Celery jobs.

- **Skills** for procedures. If an entry is a multi-step playbook rather than a fact, it belongs in `.claude/skills/`, which loads on demand.
- **Imports** — `@path/to/file.md` (max depth 4). Note: imports still load at launch, so they organize but do **not** save context.
- **`@AGENTS.md`** — if your repo already has one, create `CLAUDE.md` containing `@AGENTS.md` plus Claude-specific additions.
- **`/doctor`** proposes trims for a checked-in CLAUDE.md, cutting what Claude can derive from the codebase.
- **Auto memory** (on by default) is separate: Claude writes its own notes to `~/.claude/projects/<project>/memory/`. Browse it with `/memory`; disable with `autoMemoryEnabled: false`.

### When CLAUDE.md isn't enough

> Both are loaded at the start of every conversation. Claude treats them as context, not enforced configuration. To block an action regardless of what Claude decides, use a PreToolUse hook instead.

**Why:** "never edit `.env`" in CLAUDE.md is a request. A `PreToolUse` hook that exits 2 is a guarantee. Know which one your rule needs.

## 5. README vs CLAUDE.md

| | README.md | CLAUDE.md |
|---|---|---|
| Audience | Humans, incl. outsiders evaluating the project | An agent starting a fresh session in your repo |
| Optimized for | Onboarding narrative, motivation, screenshots, badges | Token efficiency and instruction adherence |
| Contains | What the project is, why it exists, install & quickstart, contribution guide, license | Exact commands, conventions that differ from defaults, gotchas, "always/never" rules |
| Cost of extra content | Near zero | Real — it is re-sent with every request |
| Failure mode when bloated | Nobody reads past the fold | Claude ignores your actual rules |

**Practical split:** README explains *why the OrderService exists*; CLAUDE.md says *`uv run pytest -q`, thin routers, never touch `_generated/`*.

**Do not just symlink README to CLAUDE.md.** A good README is prose and marketing; a good CLAUDE.md is a terse imperative checklist. Duplicating install instructions is fine — but the README's project tour, architecture essay, and badge wall are pure context tax.

You *can* import selectively: `See @README.md for project overview.` Only do this if the README is short — imported files load fully at launch.

## 6. Permission modes and safety

A permission mode sets what Claude may do **without asking you first**. `Shift+Tab` cycles modes in the CLI; the status bar shows the active one.

| Mode (config value) | Runs without asking | Use for |
|---|---|---|
| `default` (labeled **Manual**) | Reads only | Sensitive work, unfamiliar code, reviewing every action |
| `acceptEdits` | Reads, file edits, common fs commands (`mkdir`, `touch`, `mv`, `cp`, `rm`, `sed`) inside the working dir | Iterating on code you'll review via `git diff` |
| `plan` | Reads, plus classifier-approved commands when auto mode is available | Exploring before changing anything |
| `auto` | Everything, with background safety checks by a classifier model | Long tasks, reducing prompt fatigue |
| `dontAsk` | Only pre-approved tools | Locked-down CI and scripts |
| `bypassPermissions` | Everything | Isolated containers and VMs **only** |

```bash
claude --permission-mode default      # a.k.a. manual
claude --permission-mode acceptEdits
claude --permission-mode plan
claude --permission-mode auto
claude -p "run the test suite" --permission-mode dontAsk \
       --allowedTools "Bash(uv run pytest)" "Read"
claude -p "<prompt>" --dangerously-skip-permissions   # container only
```

### Auto mode — the current default, and what it actually does

On **Pro, Max, and Team plans**, `auto` is the built-in starting mode for interactive terminal and VS Code sessions (v2.1.228+). It is **not** "yes to everything": a separate classifier model reviews actions and blocks scope escalation, unknown infrastructure, and hostile-content-driven actions.

Blocked by default include: `curl | bash`, force push, production deploys and migrations, `git reset --hard` / `git clean -fd`, amending already-pushed commits, `terraform destroy`, IAM grants, printing live credentials, pushing secrets to public repos, and opening PRs against repositories you didn't name.

> Auto mode reduces permission prompts but does not guarantee safety. Use it for tasks where you trust the general direction, not as a replacement for review on sensitive operations.

### `bypassPermissions` / `--dangerously-skip-permissions`

Only appropriate inside a container, VM, or the sandbox runtime — and on Linux/macOS, as a **non-root user**. Deny rules still apply; allow rules become meaningless.

**Why the flag name is a warning, not a hurdle:** in this mode nothing stands between a hallucinated `rm -rf` and your filesystem except checkpoints, which only cover Claude's file-editing tools — **not** changes made via Bash. Checkpoints are not a git replacement.

### The better lever: rules + sandbox, not looser modes

```json
// .claude/settings.json
{
  "permissions": {
    "allow": [
      "Bash(uv run pytest*)",
      "Bash(uv run ruff*)",
      "Bash(git status)",
      "Bash(git diff*)"
    ],
    "deny": ["Read(./.env)", "Read(./secrets/**)"]
  }
}
```

Plus `/sandbox` for OS-level filesystem/network isolation (macOS, Linux, WSL2).

**Why:** pre-approving the twenty commands you actually trust removes 90% of prompts while keeping a hard stop on everything else. Escalating to `bypassPermissions` because you're tired of clicking removes the stop too. Deny rules apply in **every** mode, including `bypassPermissions`.

Interview-worthy nuance: `"defaultMode": "auto"` does **not** take effect from `.claude/settings.json` or `.claude/settings.local.json` — put it in `~/.claude/settings.json`.

## 7. Remote usage: web, cloud, GitHub, mobile

### Claude Code on the web

[claude.ai/code](https://claude.ai/code) — research preview for Pro, Max, and Team; Enterprise with premium or Chat + Claude Code seats. Sessions run in **isolated, Anthropic-managed VMs** (or your org's self-hosted environment), persist when you close the browser, and can be monitored from the mobile app.

Each session runs in a **cloud environment**: a saved config controlling network access, environment variables, and setup scripts.

**GitHub access** — two options: authorize the Claude GitHub App during onboarding, or run `/web-setup` in your terminal to sync your local `gh` token. A cloud session can reach any repo the connected GitHub account can see.

### Moving work between surfaces

```bash
# Terminal → cloud (clones your GitHub remote at your current branch)
claude --cloud "Fix the authentication bug in src/auth/login.py"

# Fan out — each is an independent cloud session
claude --cloud "Fix the flaky test in tests/test_auth.py"
claude --cloud "Update the API documentation"

# Monitor from the CLI
/tasks

# Cloud → terminal (fetches the branch, loads full history)
claude --teleport                 # interactive picker
claude --teleport <session-id>
/teleport   (or /tp)              # from inside an existing session

# Queue a follow-up into a running cloud session from any machine
claude -p "also add a regression test" --cloud <session-id>
```

**The high-value pattern — plan locally, execute remotely:**

```bash
claude --permission-mode plan     # collaborate on the approach
# save the plan to docs/migration-plan.md, commit, push
claude --cloud "Execute the migration plan in docs/migration-plan.md"
```

**Why:** planning is the phase where your judgment is worth the most and latency is cheap. Execution is the phase where latency is expensive and supervision adds little. Splitting them also produces a reviewable artifact.

Constraints worth knowing: `--teleport` requires a claude.ai subscription (not an API key) and a clean git working tree, and you must run it from a checkout of the same repository. Handoff from the CLI is one-way — you can pull cloud → terminal, not push terminal → cloud (the Desktop app has a *Continue in* menu that can).

### Remote Control (different thing — don't confuse them)

`/remote-control` (or `/rc`), or `claude --remote-control`, exposes a **local** session for driving from claude.ai or the mobile app. Execution and filesystem access stay on your machine; your MCP servers and project config stay available.

**Why it's not the same as `--cloud`:** cloud sessions run Anthropic-side on a clone of your remote. Remote Control runs on *your* machine with *your* uncommitted work. Use Remote Control when the work depends on local state.

### GitHub integration

- **Auto-fix PRs** — Claude subscribes to PR events and pushes fixes for CI failures and review comments. Enable with `/autofix-pr` from the PR's branch, or from the web session's CI status bar. Requires the Claude GitHub App. ⚠️ Claude may reply to review threads under your GitHub account — audit any `issue_comment`-triggered automation (Atlantis, deploy bots) before enabling.
- **Code Review** (research preview, Team/Enterprise) — multi-agent inline PR review, tuned by a repo-root `REVIEW.md`. Findings are tagged 🔴 Important / 🟡 Nit / 🟣 Pre-existing and never block merge.
- **GitHub Actions / GitLab CI/CD** — run Claude in your own CI.
- **Locally, free of all that:** `/code-review` reviews your branch's diff in a background subagent. `--fix` applies findings, `--comment` posts them as inline PR comments.

### Mobile

The Claude app for iOS/Android monitors and steers cloud sessions and Remote Control sessions. Realistic use: kick off a migration before lunch, approve a question from your phone, review the diff at your desk.

## 8. Workflow features worth knowing

### Slash commands

Built-ins you'll actually use: `/init`, `/context`, `/compact`, `/clear`, `/rewind`, `/plan`, `/model`, `/effort`, `/permissions`, `/memory`, `/hooks`, `/mcp`, `/doctor`, `/code-review`, `/security-review`, `/tasks`, `/btw`, `/resume`, `/branch`. `/help` lists everything in your build.

**Why `/btw` deserves a mention:** it answers a side question *without* the answer entering conversation history — check a detail without paying context for it.

### Skills (custom commands are now skills)

Custom commands have been merged into skills: a file at `.claude/commands/deploy.md` and a skill at `.claude/skills/deploy/SKILL.md` both create `/deploy` and work the same way. Existing `.claude/commands/` files keep working.

```markdown
<!-- .claude/skills/fix-issue/SKILL.md -->
---
name: fix-issue
description: Fix a GitHub issue end to end
disable-model-invocation: true
---
Analyze and fix the GitHub issue: $ARGUMENTS.

1. `gh issue view` to get details
2. Search the codebase for relevant files
3. Implement the fix
4. Write and run tests (`uv run pytest -q`)
5. `uv run ruff check --fix .` and `uv run mypy src/`
6. Commit, push, open a PR
```

Run it with `/fix-issue 1234`. Skills live in `.claude/skills/` (project) or `~/.claude/skills/` (personal).

**Why skills beat CLAUDE.md for procedures:** the body loads **only when used**, so a 300-line playbook costs ~one description line per session instead of 300. `disable-model-invocation: true` keeps side-effecting workflows manual and their descriptions out of context entirely.

### Hooks

Deterministic shell commands (or HTTP requests, MCP calls, prompts, subagents) fired at lifecycle events: `SessionStart`, `UserPromptSubmit`, `PreToolUse`, `PostToolUse`, `PostToolUseFailure`, `Notification`, `SubagentStop`, `Stop`, `PreCompact`, `SessionEnd`, and more.

```json
// .claude/settings.json — auto-format every Python file Claude edits
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | grep '\\.py$' | xargs -r uv run ruff format"
          }
        ]
      }
    ]
  }
}
```

**Why a hook, not a CLAUDE.md line:** "always run ruff after editing" is advisory — Claude follows it most of the time. The hook fires 100% of the time, costs zero context, and works even if CLAUDE.md is long. `PreToolUse` hooks that exit 2 **block** the action and feed the reason back to Claude. Browse configured hooks with `/hooks`. You can also just ask: *"write a hook that runs ruff after every file edit."*

### MCP servers

Model Context Protocol connects Claude to external systems — Jira, Sentry, Postgres, Figma, Notion.

```bash
claude mcp add --transport http notion https://mcp.notion.com/mcp
claude mcp add --env PGURL=... --transport stdio pg -- npx -y @some/pg-mcp
claude mcp add --transport http --scope project jira https://mcp.example.com/mcp
claude mcp list      # health status per server
/mcp                 # connection status in-session
```

Scopes: local (default) → project (`.mcp.json`, committable) → user. Tool search is on by default, so only tool **names** load at session start; full schemas are deferred.

**Why:** connect a server when you notice yourself copy-pasting from a browser tab. But treat third-party MCP servers as code you're granting tool access to — prefer a CLI (`gh`, `psql`) when one exists, since it costs no persistent context and no trust decision.

### Subagents

Isolated workers with their own context window that return only a summary.

```markdown
<!-- .claude/agents/security-reviewer.md -->
---
name: security-reviewer
description: Reviews Python code for security vulnerabilities
tools: Read, Grep, Glob, Bash
model: opus
---
You are a senior security engineer. Review for injection (SQL, command),
auth/authz flaws, secrets in code, and unsafe deserialization.
Provide specific line references and suggested fixes.
```

```text
Use subagents to investigate how our auth system handles token refresh,
and whether we have existing OAuth utilities I should reuse.
```

**Why:** codebase research is the single biggest context consumer. A subagent reads forty files in *its* window and hands you back six lines. Built-ins `Explore` and `Plan` do this automatically. Add `isolation: worktree` to a subagent's frontmatter so its edits can't collide with parallel work.

### Git worktrees for parallel sessions

```bash
claude --worktree feature-auth      # or -w; creates .claude/worktrees/feature-auth
claude -w "#1234"                   # branch from a PR (quote the #)
```

Claude Code **enforces** the isolation: edits, command working directories, and git redirects that target the main checkout are blocked. Add `.claude/worktrees/` to `.gitignore`, and a `.worktreeinclude` file to copy gitignored `.env` files into each new worktree.

**Why worktrees over branches:** two sessions on one checkout will clobber each other's uncommitted work. Worktrees give each session real filesystem isolation while sharing `.git`, so `git commit` still works. Manual equivalent: `git worktree add ../proj-feature -b feature`.

The **Writer/Reviewer** pattern this enables:

| Session A (Writer) | Session B (Reviewer) |
|---|---|
| `Implement a rate limiter for our API endpoints` | |
| | `Review @src/middleware/rate_limit.py. Look for edge cases, race conditions, and consistency with our existing middleware.` |
| `Here's the review feedback: [B's output]. Address these issues.` | |

**Why it works:** a fresh context is not biased toward code it just wrote.

### Context management

The context window holds conversation, every file read, every command output, CLAUDE.md, auto memory, skill descriptions, and system instructions. **Performance degrades as it fills** — this is the constraint behind nearly every practice in this guide.

| Tool | Effect |
|---|---|
| `/context` | See exactly what's using space (`/context all` for per-MCP-tool tokens) |
| `/clear` | Full reset between unrelated tasks |
| `/compact` | Summarize to free space; auto-fires near the limit |
| `/compact focus on the API changes` | Steer what survives |
| `Esc Esc` → *Summarize from/up to here* | Compact only part of the conversation |
| Subagents | Keep exploration out of your window entirely |
| `/btw` | Ask without the answer entering history |

Project-root `CLAUDE.md` **survives compaction** — Claude re-reads it from disk afterward. Conversation-only instructions do not.

```markdown
# Compact Instructions
When compacting, always preserve the full list of modified files and any
test commands that were run.
```

**Why `/clear` beats `/compact` between tasks:** compaction keeps a lossy summary of work you no longer need. Clearing costs you nothing when the next task is unrelated, and CLAUDE.md reloads automatically.

## 9. Anti-patterns

**1. The kitchen sink session.** One task, then an unrelated question, then back. Context is now full of noise.
→ **Fix:** `/clear` between unrelated tasks.

**2. Correcting over and over.** Three corrections in, context is polluted with failed approaches that bias every retry.
→ **Fix:** after two failed corrections, `/clear` and write a better initial prompt incorporating what you learned.

**3. The over-specified CLAUDE.md.** 400 lines, and Claude ignores half of it.
→ **Fix:** ruthlessly prune. If Claude already does it right without the instruction, delete it. If it must happen every time, convert it to a hook.

**4. The trust-then-verify gap.** Plausible implementation, unhandled edge cases, merged.
→ **Fix:** always provide verification — tests, a script, a screenshot. **If you can't verify it, don't ship it.** Have Claude show *evidence* (the command it ran and its output), not an assertion of success.

**5. The infinite exploration.** "Investigate the auth system" with no scope; Claude reads 200 files.
→ **Fix:** scope the investigation, or delegate it to a subagent so it doesn't consume your main context.

**6. Dumping a huge vague task.** "Refactor the payments module."
→ **Fix:** plan mode → reviewed plan → implement in steps, each with its own verification. Big vague tasks fail *late*, after the expensive part.

**7. Not reviewing diffs.** `acceptEdits` or `auto` is a convenience mode, not an approval.
→ **Fix:** read `git diff` before committing. Run `/code-review` on the branch. Checkpoints only track Claude's file-editing tools — not Bash changes — so they are not your safety net.

**8. Over-chasing reviewer findings.** A reviewer asked to find gaps will find some, even in sound work — leading to defensive code and tests for impossible cases.
→ **Fix:** tell the reviewer to flag only gaps affecting correctness or stated requirements; treat the rest as optional.

**9. Escalating permissions to stop the prompts.** Reaching for `--dangerously-skip-permissions` out of fatigue.
→ **Fix:** pre-approve trusted commands in `permissions.allow`, turn on `/sandbox`, and use `auto` mode. Reserve bypass for containers.

## 10. Interview-ready summary

The senior-level framing, in one paragraph:

> Claude Code is an agentic harness around a model — a loop of gather context, act, verify. Because the loop's only stopping signal is "looks done," the engineer's job is to (1) make inputs precise enough that the first attempt is close, (2) give the loop a machine-readable success criterion so it self-corrects without you, and (3) manage the context window, which is the binding resource and degrades everything as it fills. Everything else — CLAUDE.md hygiene under 200 lines, plan mode for multi-file work, skills for on-demand procedures, hooks for guarantees, subagents and worktrees for isolation, `/clear` over `/compact` between tasks — is a specific application of those three.

**Further reading (official):**

- Best practices — https://code.claude.com/docs/en/best-practices
- How Claude Code works — https://code.claude.com/docs/en/how-claude-code-works
- CLAUDE.md / memory — https://code.claude.com/docs/en/memory
- Permission modes — https://code.claude.com/docs/en/permission-modes
- Skills — https://code.claude.com/docs/en/skills
- Hooks — https://code.claude.com/docs/en/hooks-guide
- MCP — https://code.claude.com/docs/en/mcp
- Subagents — https://code.claude.com/docs/en/sub-agents
- Worktrees — https://code.claude.com/docs/en/worktrees
- Claude Code on the web — https://code.claude.com/docs/en/claude-code-on-the-web
- Model config & effort — https://code.claude.com/docs/en/model-config

*Note: Claude Code evolves quickly — version-gated details (default modes, plan availability, model lineups) drift; re-check the linked docs before relying on them.*
