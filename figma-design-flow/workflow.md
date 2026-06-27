# Workflow (MCP-Driven Execution)

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

The only confirmation point is during implementation mode (see implementation.md). Design mode is fully automated.

## 4. Document Generation

Write to: `docs/design/figma/<feature>.md`

Follow the exact structure defined in [output.md](output.md).

## 5. Style Check Phase

Compare MCP snapshot against generated documentation using [style-check.md](style-check.md).

## 6. Auto-Fix Loop

If mismatches found:
1. Patch the documentation
2. Re-run style check (max 2 cycles)

## 7. Complete

The documentation phase is complete. The generated document is ready for review or implementation.

**Note:** This flow only produces documentation. No confirmation is requested at this stage.
