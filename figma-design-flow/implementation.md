# Implementation Mode (Strict)

Activated only after DESIGN MODE is complete and verification has passed. Uses existing documentation and design system — never re-queries Figma.

---

## 1. Pre-Implementation Confirmation

Before starting implementation, request user confirmation using openQuestion:

- **Proceed** — begin implementation using the generated documentation
- **Modify** — user requests changes to the documentation first (update docs, then re-confirm)
- **Cancel** — end implementation mode

This is the only confirmation point in the workflow. All auto-fix and refinement loops during design mode happen automatically without user interruption.

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
