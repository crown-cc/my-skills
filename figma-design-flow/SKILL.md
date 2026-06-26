---
name: figma-design-flow
description: Use when a Figma link is provided, UI analysis or style verification against Figma designs is requested, or design-to-documentation conversion is needed. Extracts structured design docs and implementation blueprints from Figma via MCP.
---

# Figma Design Flow (v2 — MCP Driven)

## Overview

Converts Figma designs into structured design documentation, implementation blueprints, and style verification reports. Figma (via MCP) is the single source of truth. The skill produces documentation only — no implementation unless explicitly requested.

All state, caching, and snapshot management is delegated to the Figma MCP. Do NOT persist state locally.

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
3. **Output**: [output.md](output.md) — exact 10-section document specification
4. **Verify**: [style-check.md](style-check.md) — compare docs against MCP snapshot, auto-fix loop
5. **Implement**: [implementation.md](implementation.md) — only if user explicitly requests; applies after verification is complete

## Modes

### DESIGN MODE (default)

Figma → Analysis → Documentation → Style Check → Auto-fix loop

Produces `docs/design/figma/<feature>.md`. No code is written.

### IMPLEMENT MODE (manual only)

Activated only when the user explicitly requests "implement." Follows [implementation.md](implementation.md) strictly — no MCP calls, no re-analysis, use existing docs and design system only.
