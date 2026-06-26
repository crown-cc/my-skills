# Workflow (MCP-Driven Execution)

## 1. Input Detection

If a Figma URL is detected → proceed to MCP fetch.

## 2. MCP Fetch

Use Figma MCP to retrieve: frame data, node tree, styles, layout info.

Cache is handled by MCP — do NOT implement local caching.

## 3. Analysis Phase

Run structured UI extraction following [analysis.md](analysis.md).

## 4. Document Generation

Write to: `docs/design/figma/<feature>.md`

Follow the exact structure defined in [output.md](output.md).

## 5. Style Check Phase

Compare MCP snapshot against generated documentation using [style-check.md](style-check.md).

## 6. Auto-Fix Loop

If mismatches found:
1. Patch the documentation
2. Re-run style check (max 2 cycles)

## 7. Wait for User Decision

Present options:
- **review** — user inspects the generated documentation
- **implement** — user explicitly requests implementation (triggers [implementation.md](implementation.md))
- **exit** — end the session
