# Output Specification

Write to: `docs/design/figma/<feature>.md`

## Required Structure

Keep the section structure exactly as defined below. Do NOT add, remove, rename, or reorder sections.

### 1. Overview

Screen purpose, user goal, and high-level layout description.

### 2. Screen Layout Diagram

ASCII box-drawing diagram showing the visual arrangement of the screen. Use `┌─┐│└┘├┤┬┴┼` characters. Annotate key regions with size, style, and behavior notes using `←` callouts.

```
┌──────────────────────────────┐
│ Region Name                  │  ← annotation (size, style, behavior)
│  detail line                 │
├──────────────────────────────┤
│ Next Region                  │
│  ...                         │
└──────────────────────────────┘
```

### 3. UI Structure Tree

Hierarchical component tree showing parent-child relationships with file paths.

### 4. Layout Rules

Auto layout rules, alignment, z-index layering, scroll containers, sticky/fixed elements, overlays.

### 5. Spacing & Alignment Spec

Exact px values for spacing, padding, margins. Explain spacing relationships and layout rhythm, not just a list of values.

### 6. Typography Spec

Per text node: font family, size, weight, line height, letter spacing, alignment.

### 7. Component Mapping Table

| Node | Type | Reason |

Types: Shared, Feature, Primitive. Distinguish reusable from feature-specific components.

### 8. Interaction Model

Click zones, gestures, scroll areas, hover/active/disabled states.

### 9. Design System Mapping

Map to tokens: colors, spacing, radius, shadow, typography. Mark missing mappings as NEW TOKEN REQUIRED.

### 10. Implementation Plan

File structure, component tree, reuse strategy, identified gaps.

### 11. Open Questions

Record ambiguities, decision points, and inferred behaviors. Use this format:

```
### Design Decisions

- **Question:** [what ambiguity or decision was encountered]
  - **Options:** [alternative approaches that were considered]
  - **Recommended:** [chosen approach — this is what the document uses]
  - **Rationale:** [why this recommendation was chosen]

### Unresolved Ambiguities

- **Issue:** [actual ambiguity that needs clarification]
  - **Assumption:** [what was assumed in this document]
```

**Note:** All design decisions are made automatically during analysis phase. No confirmation is requested at this stage. Questions are recorded for traceability and potential discussion during implementation.

---

## Quality Standard

Each section must contain implementation-ready details, not high-level summaries. The document must be detailed enough that an engineer can implement the UI without reopening Figma.
