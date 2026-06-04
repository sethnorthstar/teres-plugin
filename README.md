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
claude mcp add --transport http --scope user --header "Authorization: Bearer <YOUR_KEY>" teres https://teres.sethhillestad707.workers.dev/mcp

# 2. install the two skills
mkdir -p ~/.claude/skills/teres-build ~/.claude/skills/teres-learn
curl -fsSL https://raw.githubusercontent.com/sethnorthstar/teres-plugin/main/skills/teres-build/SKILL.md -o ~/.claude/skills/teres-build/SKILL.md
curl -fsSL https://raw.githubusercontent.com/sethnorthstar/teres-plugin/main/skills/teres-learn/SKILL.md -o ~/.claude/skills/teres-learn/SKILL.md
```

### Windows (PowerShell — not CMD)
```powershell
# 1. connect the Teres server (key goes in the command)
claude mcp add --transport http --scope user --header "Authorization: Bearer <YOUR_KEY>" teres https://teres.sethhillestad707.workers.dev/mcp

# 2. install the two skills
New-Item -ItemType Directory -Force "$HOME\.claude\skills\teres-build" | Out-Null
New-Item -ItemType Directory -Force "$HOME\.claude\skills\teres-learn" | Out-Null
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/sethnorthstar/teres-plugin/main/skills/teres-build/SKILL.md" -OutFile "$HOME\.claude\skills\teres-build\SKILL.md"
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/sethnorthstar/teres-plugin/main/skills/teres-learn/SKILL.md" -OutFile "$HOME\.claude\skills\teres-learn\SKILL.md"
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
/plugin marketplace add sethnorthstar/teres-plugin
/plugin install teres@teres-plugin
```
…with `TERES_API_KEY` set as an environment variable. If `/plugin` reports it's unavailable, your CLI is too old or you're on an unsupported surface (Desktop app / web / JetBrains) — use the manual install above instead.

---

## Notes

- Trade/contractor industries are best-covered today (plumbing, roofing, concrete, electrical, HVAC, remodeling, handyman, painting, landscaping, cleaning).
- Learn mode (`teres-learn`) is early.
- The skills hold no design content — everything comes from the Teres server, which only works with a live, paid key.
