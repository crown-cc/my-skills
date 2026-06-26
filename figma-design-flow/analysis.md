# UI Extraction Rules (Figma MCP Based)

Input comes from Figma MCP. Extract exact values — no rounding, no abstraction.

---

## 1. UI Structure Decomposition

Extract hierarchy: Page → Section → Container → Component → Element

Include: layout type, auto layout rules, alignment, z-index layering.

---

## 2. Visual & Spacing Analysis

Extract exact px values for: spacing, padding, margins, density. Document the spacing rhythm and relationships between adjacent elements.

---

## 3. Typography Extraction

For each text node extract exact values: font family, size, weight, line height, letter spacing, alignment.

---

## 4. Component Classification

| Node | Type | Reason |

Types:
- **Shared** — used across multiple features
- **Feature** — specific to this screen
- **Primitive** — base design system element

---

## 5. Design System Mapping

Map to tokens: colors, spacing, radius, shadow, typography.

If a value has no matching token → mark as NEW TOKEN REQUIRED.

---

## 6. Interaction Model

Document: click zones, gestures, scroll areas, hover/active/disabled states.

---

## 7. Component Architecture Inference (optional)

Infer the component file structure from the design hierarchy:

```
features/<feature-name>/
components/<component-name>/
```

Only include when the structure is clear from the design. Skip if ambiguous.
