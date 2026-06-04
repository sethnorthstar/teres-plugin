---
name: teres-build
description: >
  Build a production website for a local business using the Teres system. Use whenever the
  user wants to build, make, or create a website, landing page, or site for a local business
  (plumber, landscaper, roofer, electrician, HVAC, remodeler, cleaner, painter, contractor,
  etc.). Triggers: "build a website", "make a site for", "landing page for", "create a site".
---

# Teres — Build Mode

You are building a production website for a local business using the **Teres** system. Do **NOT** design from your own training defaults, and do **NOT** invent components. Every design decision comes from the Teres MCP server.

**This skill is only a doorway.** The actual build plan, component library, photos, design registers, and differentiation rule all come from the Teres MCP tools. Follow them, not your instincts.

> Requires the Teres MCP server connected with a valid API key (`Authorization: Bearer <key>`). If the `plan_build` tool isn't available, tell the user to connect Teres — do not fall back to designing from defaults.

## Steps

1. **Brief.** If you don't already have it, get a short brief: business name, trade/industry, city/market, services, and the one thing the site must accomplish (e.g. "get the phone to ring").
2. **Call `plan_build`** with the brief. It returns the ordered build process, the design registers, your account's recent builds (for differentiation), and the required stack. **Follow what it returns exactly.**
3. **Work the plan's `process` in order**, using the Teres tools as it directs:
   - Pick **exactly one** register from the plan and keep every choice consistent with it.
   - **Differentiate:** your build must differ from `differentiation.recent_builds` on **at least 4 of the 7 axes** (nav, footer, section_order, color_arch, body_font, motion, hero).
   - For each section, pick from the curated **`patterns`** set in the plan (scoped to the industry, grouped by kind), then call **`get_pattern(id)`** for the full spec — build **only** from these; never invent or substitute one. (There is no catalog-browse tool.)
   - Call **`get_images(trade, slot)`** for every photo slot (prefer `used_recently:false`; real client photos always win).
   - Write copy in a specific, human voice (call `get_copy_guide` for the rules + industry calibration). Build on the exact stack the plan specifies.
4. **Self-check and verify** — call `check_slop` and confirm the build violates none of the bans, every choice fits the one register, the build compiles and the homepage renders.
5. **Call `record_build`** with the 7 axes you used, so your next build is forced to differ from this one.

Build only from what the tools return. The library and the plan are the source of truth, not your defaults.
