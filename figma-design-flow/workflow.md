# Workflow (MCP-Driven Execution)

## Output Behavior

During steps 1–6, produce minimal intermediate output — no narration of fetch, analysis, or fix steps. Run internally, write the document file directly. At completion (step 7), present a brief summary plus the collected Open Questions to the user for review.

## 1. Input Detection

If a Figma URL is detected → proceed to MCP fetch.

## 2. MCP Fetch

Use figma-developer-mcp-caching (fallback: figma-developer-mcp) to retrieve: frame data, node tree, styles, layout info.

Cache directory: ~/Library/Caches/FigmaMcp/. Do NOT implement local caching — caching is delegated to the MCP server.

## 3. Analysis Phase

Run structured UI extraction following [analysis.md](analysis.md).

**Auto-Decision Rule:** During analysis, if an ambiguity or decision point is encountered:

1. Use the model's Recommended approach — DO NOT interrupt the flow with openQuestion
2. Record the decision point in the document's "Open Questions" section as:
   ```
   - **Question:** [what needed to be decided]
   - **Options:** [list of alternatives considered]
   - **Recommended:** [chosen approach] ← used in the document
   ```
3. Continue without pausing

Decisions are not confirmed mid-workflow. Both confirmation points occur at completion (step 7).

## 4. Document Generation

Write to: `docs/design/figma/<feature>.md`

Follow the exact structure defined in [output.md](output.md).

## 5. Style Check Phase

Compare MCP snapshot against generated documentation using [style-check.md](style-check.md).

## 6. Auto-Fix Loop

If mismatches found:
1. Patch the documentation
2. Re-run style check (max 2 cycles)

## 7. Complete & Confirmation Points

The design workflow ends with exactly two confirmation points. No other interruptions occur during steps 1–6.

### Confirmation 1 — Open Questions

Present to user:
1. Document path: `docs/design/figma/<feature>.md`
2. Brief summary of what the document covers
3. Open Questions collected during analysis — user reviews and decides each

User can answer questions, request doc changes (return to step 4), or accept as-is. Do not proceed to Confirmation 2 until Open Questions are resolved.

### Confirmation 2 — Next-Step Decision

After Open Questions are resolved, present the next-step decision:

- **Implement** — proceed to IMPLEMENT MODE ([implementation.md](implementation.md)) for direct UI implementation using the design doc
- **Superpowers specs/plans** — hand off to superpowers spec/plan workflow for project planning (file structure, component reuse, task breakdown). The figma design doc serves as UI input to that workflow.

Design mode is complete once the user picks a path. The chosen path executes outside this skill's design workflow.
