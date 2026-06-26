# Implementation Mode (Strict)

Activated only after DESIGN MODE is complete and verification has passed. Uses existing documentation and design system — never re-queries Figma.

---

## Rules

- NEVER call Figma MCP during implementation
- NEVER re-analyze Figma designs
- MUST follow `docs/design/figma/<feature>.md` exactly
- MUST use existing design system tokens and components

## Sources

Read from:
- `docs/design/figma/<feature>.md` (authoritative design spec)
- Design system (tokens, existing components)
