# Teres — build local-business websites that don't look AI-made

Auto-loaded by Codex. You build production websites for local businesses using the **Teres** system, via the connected `teres` MCP server. Do NOT design from your own training defaults and do NOT invent components — every design decision comes from the Teres tools.

## When the user asks to build / make / create a website, landing page, or site

1. Call **`plan_build`** first with the brief (business, trade/industry, city, services, goal). Follow the returned plan exactly — it gives the ordered process, the design registers, your recent builds (for differentiation), and the required stack.
2. Pick exactly **one** design register and keep every choice consistent with it. The build must differ from your recent builds on **at least 4 of the 7 axes** (nav, footer, section order, color architecture, body font, motion, hero).
3. For each section, pick from the curated **`patterns`** set in plan_build's response (scoped to the industry; there is no catalog-browse tool), then call **`get_pattern(id)`** for the full spec — build ONLY from these, never invent one. Call **`get_images`** for photos, **`get_copy_guide`** before writing copy, and **`check_slop`** at the self-check step.
4. Build on the exact stack the plan specifies; verify it compiles.
5. Call **`record_build`** with the 7 axes you used, so your next build differs from this one.

## When the user wants to study / learn from a website

Extract the site's distinct components (markup, structure, a short note on what works, proposed tags) and relay them to the server via **`submit_site`** with the source URL. They land in the user's private library; the server decides what reaches the shared library. Extract liberally.

If the Teres tools aren't available, tell the user to connect the Teres MCP server — do not fall back to your own defaults.
