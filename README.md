# Teres — Claude Code plugin

Make AI-built websites that nobody can tell were built by AI. This plugin connects your Claude Code to the **Teres** system — the build + learn skills and the hosted Teres MCP server (component library, photos, design registers, the differentiation engine, the blacklist + copy guide).

You bring your own AI model; Teres is the brain it follows. You need a **Teres API key**.

## Setup (~2 minutes)

**1. Set your Teres API key once.**

macOS/Linux:
```bash
echo 'export TERES_API_KEY="your-key-here"' >> ~/.zshrc && source ~/.zshrc
# (bash users: use ~/.bashrc)
```

Windows (PowerShell):
```powershell
setx TERES_API_KEY "your-key-here"
# then open a NEW terminal window so it takes effect
```

**2. Add the marketplace and install the plugin** (inside Claude Code):
```
/plugin marketplace add sethnorthstar/teres-plugin
/plugin install teres@teres-plugin
```

**3. Verify:**
```
/mcp        # should show the "teres" server connected
```
If `teres` shows as failed/unauthorized, `TERES_API_KEY` isn't set in the shell that launched Claude Code — set it (step 1) and restart Claude Code.

## Use it

Just ask, naturally:

> Build a website for a plumber called Cascade Plumbing in Portland, OR. Services: drain cleaning, water heaters, emergency repair. Goal: get the phone to ring.

The build skill runs the full Teres process: pick one design register, differentiate from your recent builds, pull components + photos from the library, write copy to the guide, self-check against the blacklist, and log the build so your next site comes out different. Build a second site in the same trade and confirm it looks like a different agency made it.

## Updates

Automatic — when we publish, your plugin updates. Force a refresh anytime with `/plugin marketplace update teres-plugin`.

## Notes

- Trade/contractor industries are the best-covered today (plumbing, roofing, concrete, electrical, HVAC, remodeling, handyman, painting, landscaping, cleaning).
- Learn mode (`/teres:teres-learn`) is early.
- The plugin holds no design content — everything comes from the Teres server, which only works with a live, paid key.
