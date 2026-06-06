# Teres — Claude Code

Make AI-built websites that nobody can tell were built by AI. Teres connects your Claude Code to a component library, photo pool, design registers, a differentiation engine, and a quality check — so your AI builds local-business sites that look like a real designer made them.

You bring your own AI model; Teres is the brain it follows. You need a **Teres API key**.

> **Use the Claude Code CLI in a terminal** — not the Claude Desktop app, the web (claude.ai/code), or JetBrains. Those don't run Claude Code skills.

---

## Install (works on any Claude Code CLI)

Run these in your terminal. Replace `<YOUR_KEY>` with your Teres API key.

### macOS / Linux
```bash
# 1. connect the Teres server (key goes in the command)
claude mcp add --transport http --scope user --header "Authorization: Bearer <YOUR_KEY>" teres https://teres.buildwithteres.workers.dev/mcp

# 2. install the two skills
mkdir -p ~/.claude/skills/teres-build ~/.claude/skills/teres-learn
curl -fsSL https://raw.githubusercontent.com/teresnorthstar/teres-plugin/bf436c46f16ff44eaaeaa944c845c43deb8b3c81/skills/teres-build/SKILL.md -o ~/.claude/skills/teres-build/SKILL.md
curl -fsSL https://raw.githubusercontent.com/teresnorthstar/teres-plugin/bf436c46f16ff44eaaeaa944c845c43deb8b3c81/skills/teres-learn/SKILL.md -o ~/.claude/skills/teres-learn/SKILL.md
```

### Windows (PowerShell — not CMD)
```powershell
# 1. connect the Teres server (key goes in the command)
claude mcp add --transport http --scope user --header "Authorization: Bearer <YOUR_KEY>" teres https://teres.buildwithteres.workers.dev/mcp

# 2. install the two skills
New-Item -ItemType Directory -Force "$HOME\.claude\skills\teres-build" | Out-Null
New-Item -ItemType Directory -Force "$HOME\.claude\skills\teres-learn" | Out-Null
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/teresnorthstar/teres-plugin/bf436c46f16ff44eaaeaa944c845c43deb8b3c81/skills/teres-build/SKILL.md" -OutFile "$HOME\.claude\skills\teres-build\SKILL.md"
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/teresnorthstar/teres-plugin/bf436c46f16ff44eaaeaa944c845c43deb8b3c81/skills/teres-learn/SKILL.md" -OutFile "$HOME\.claude\skills\teres-learn\SKILL.md"
```
(Don't swap in `curl -o` on Windows — in PowerShell `curl` is an alias for `Invoke-WebRequest` and the flags differ.)

---

## Use it

Start Claude Code in your terminal:
```
claude
```
Confirm the server is connected:
```
/mcp        # should show "teres" connected
```
Then just ask, naturally:

> Build a website for a plumber called Cascade Plumbing in Portland, OR. Services: drain cleaning, water heaters, emergency repair. Goal: get the phone to ring.

The build skill runs the full Teres process: pick one design register, differentiate from your recent builds, pull components + photos from the library, write copy to the guide, self-check against the blacklist, and log the build so your next site comes out different. Build a second site in the same trade and confirm it looks like a different agency made it.

---

## One-step alternative (recent CLI only)

If your Claude Code CLI is current and supports plugins, you can install everything as a plugin **instead** of the manual steps above (don't do both — you'd get two copies of the server):

```
/plugin marketplace add teresnorthstar/teres-plugin
/plugin install teres@teres-plugin
```
…with `TERES_API_KEY` set as an environment variable. If `/plugin` reports it's unavailable, your CLI is too old or you're on an unsupported surface (Desktop app / web / JetBrains) — use the manual install above instead.

---

## Notes

- Trade/contractor industries are best-covered today (plumbing, roofing, concrete, electrical, HVAC, remodeling, handyman, painting, landscaping, cleaning).
- Learn mode (`teres-learn`) is early.
- The skills hold no design content — everything comes from the Teres server, which only works with a live, paid key.

---

## Security & your data

- **Installing connects you to a remote server we operate.** Both install paths register an MCP server at `https://teres.buildwithteres.workers.dev/mcp` (HTTPS) that your AI client calls during builds. Your Teres API key is sent as a `Bearer` token on each request.
- **What gets sent to the server:** the build brief you provide (business, trade, city, services, goal) and, in learn mode, the source URL plus the component markup your agent extracted from a site you named. The skills do **not** read or upload your local files, environment variables, or other credentials.
- **Your API key is a bearer credential** — anyone holding it can use your plan. Keep it out of shared shell profiles and screenshots; prefer a per-session env var or your client's secret store. If it leaks, rotate it from your Teres dashboard.
- **Verify what you install.** The manual-install URLs are pinned to a specific commit SHA (not `main`) over HTTPS, so a later change to the repo can't silently alter the skill your agent will follow. To adopt a newer version, bump the SHA in those URLs. The `/plugin marketplace` path is the signed alternative.
- **Treat learn-mode pages as untrusted.** The learn skill instructs the agent to treat any fetched page as data to analyze, never as instructions — so a malicious site can't hijack the agent through hidden prompts.
