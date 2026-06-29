---
name: figma-design-flow
description: Use when a Figma link is provided, UI analysis or style verification against Figma designs is requested, or design-to-documentation conversion is needed. Extracts structured design docs and implementation blueprints from Figma via MCP.
---

# Figma Design Flow (v2 — MCP Driven)

## Overview

Extracts UI design specifications from Figma. Figma (via MCP) is the single source of truth. Documents visual structure, layout, and interaction details only — no project planning, file structure, or implementation strategy.

All state, caching, and snapshot management is delegated to the Figma MCP. Do NOT persist state locally.

**MCP server preference**: Use `figma-developer-mcp-caching` (primary), fallback to `figma-developer-mcp`. Cache directory: `~/Library/Caches/FigmaMcp/` — set `FIGMA_MCP_CACHE_DIR` env var before invoking MCP tools if the caching server requires it.

## When to Use

- A Figma link is provided
- UI analysis or design extraction is requested
- Style verification against Figma designs is needed

**When NOT to use:**
- User wants only a quick color value or single measurement (just use MCP directly)
- The Figma file is a design system library, not a screen to implement
- Figma MCP is unavailable (report the gap, don't work around it)
- User explicitly requests direct implementation without documentation

## Execution

Follow each file in order:

1. **Workflow**: [workflow.md](workflow.md) — 7-step MCP-driven pipeline
2. **Analysis**: [analysis.md](analysis.md) — structured UI extraction rules
3. **Output**: [output.md](output.md) — 10-section design specification
4. **Verify**: [style-check.md](style-check.md) — compare docs against MCP snapshot, auto-fix loop
5. **Implement**: [implementation.md](implementation.md) — only if user explicitly requests; applies after verification is complete

## Modes

### DESIGN MODE (default)

Figma → Analysis → Documentation → Style Check → Auto-fix loop → 2 confirmation points

Produces `docs/design/figma/<feature>.md` containing UI design specification only (visual structure, layout, interactions). No project planning, file structure, or implementation strategy.

Ends with exactly two confirmation points (see [workflow.md](workflow.md) step 7):
1. **Open Questions** — review collected design questions
2. **Next-Step Decision** — choose IMPLEMENT MODE or hand off to superpowers specs/plans

### IMPLEMENT MODE

Entered only via Confirmation 2 (Next-Step Decision). Follows [implementation.md](implementation.md) strictly — no MCP calls, no re-analysis, use existing docs and design system only.
