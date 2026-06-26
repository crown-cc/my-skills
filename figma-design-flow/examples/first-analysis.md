# Example Output: User Profile Screen

Generated from Figma MCP extraction. Shows the expected depth for "implementation-ready" documentation.

---

## 1. Overview

User profile screen displaying avatar, account details, and a settings section. Vertical scroll layout with sticky header. User can edit profile via a FAB in the bottom-right.

---

## 2. Screen Layout Diagram

```
┌──────────────────────────────────┐
│ ←  My Profile                    │  ← sticky header, z-10, 56px height
├──────────────────────────────────┤
│                                  │
│          ┌──────────┐            │  ← avatar 96×96 circle, centered
│          │  Avatar  │            │
│          └──────────┘            │
│        Change Photo              │  ← link, 14px accent, below avatar
│                                  │
├──────────────────────────────────┤
│ Account Details                  │  ← section header, 12px medium, gray
│                                  │
│ Name            Alex Johnson  ›  │  ← InfoRow, 48px height, tap to edit
│ Email           alex@e...com  ›  │
│ ──────────────────────────────── │  ← divider, 1px subtle
├──────────────────────────────────┤
│ Settings                         │  ← section header, 12px medium, gray
│                                  │
│ 🔔  Notifications       [ON]    │  ← SettingsRow + toggle, 48px
│ 🔒  Privacy                  ›   │  ← SettingsRow + chevron, 48px
│                                  │
├──────────────────────────────────┤
│                                  │
│        [ Delete Account ]        │  ← destructive button, centered
│                                  │
│                              [+] │  ← FAB, 56×56, bottom-right, z-20
└──────────────────────────────────┘
```

## 3. UI Structure Tree

```
Page: ProfileScreen
├── Header (sticky, z-10)
│   ├── BackButton (24×24 icon)
│   └── Title ("My Profile", 20px semibold)
├── ScrollContent (vertical scroll)
│   ├── AvatarSection
│   │   ├── Avatar (96×96 circle, centered)
│   │   └── ChangePhotoLink (14px, accent color)
│   ├── InfoSection
│   │   ├── SectionHeader ("Account Details")
│   │   ├── InfoRow [name]
│   │   │   ├── Label ("Name", 14px, secondary)
│   │   │   └── Value ("Alex Johnson", 16px, primary)
│   │   ├── InfoRow [email]
│   │   │   ├── Label ("Email", 14px, secondary)
│   │   │   └── Value ("alex@example.com", 16px, primary)
│   │   └── Divider (1px, subtle)
│   ├── SettingsSection
│   │   ├── SectionHeader ("Settings")
│   │   ├── SettingsRow [notifications]
│   │   │   ├── Icon (bell, 20×20)
│   │   │   ├── Label ("Notifications")
│   │   │   └── Toggle (on)
│   │   └── SettingsRow [privacy]
│   │       ├── Icon (lock, 20×20)
│   │       ├── Label ("Privacy")
│   │       └── Chevron (disclosure indicator)
│   └── DangerZone
│       └── DeleteAccountButton (destructive style)
└── FAB (bottom-right, 56×56 circle, z-20)
    └── EditIcon (24×24, white)
```

---

## 4. Layout Rules

- **Page**: Vertical scroll, full height, background `surface.primary`
- **Header**: Sticky top, `z-10`, height 56px, horizontal padding 16px, flex row with centered title
- **AvatarSection**: Centered content, padding 24px top/bottom
- **InfoSection**: Vertical stack, 12px gap between rows, 16px horizontal padding
- **SettingsSection**: Vertical stack, rows are 48px height with icon + label left, action right
- **Divider**: Full width, 1px height, color `border.subtle`
- **FAB**: Position fixed bottom-right, 16px from edges, `z-20`, shadow `elevation.3`

---

## 5. Spacing & Alignment Spec

| Element | Value |
|---------|-------|
| Base grid | 8px |
| Page horizontal padding | 16px |
| Section vertical padding | 24px |
| InfoRow gap (label → value) | 8px |
| InfoSection row gap | 12px |
| SettingsRow height | 48px |
| Avatar size | 96×96px |
| FAB size | 56×56px |
| FAB offset (bottom/right) | 16px |

Spacing rhythm: sections use 24px vertical separation, rows within sections use 12px gap, internal row elements use 8px gap. This creates a consistent 8px-based hierarchy.

---

## 6. Typography Spec

| Element | Font | Size | Weight | Line Height | Letter Spacing |
|---------|------|------|--------|-------------|----------------|
| Header title | Inter | 20px | 600 (semibold) | 28px | 0 |
| Section header | Inter | 12px | 500 (medium) | 16px | 0.5px |
| InfoRow label | Inter | 14px | 400 (regular) | 20px | 0 |
| InfoRow value | Inter | 16px | 400 (regular) | 24px | 0 |
| Link text | Inter | 14px | 500 (medium) | 20px | 0 |
| Button text | Inter | 16px | 600 (semibold) | 24px | 0 |

---

## 7. Component Mapping Table

| Node | Type | Reason |
|------|------|--------|
| BackButton | Primitive | Standard navigation, design system icon button |
| Avatar | Primitive | Design system avatar component, size variant "lg" |
| InfoRow | Shared | Used across profile, settings, and checkout screens |
| SettingsRow | Shared | Used in all settings screens |
| Toggle | Primitive | Design system toggle component |
| FAB | Primitive | Design system FAB, variant "primary" |
| DeleteAccountButton | Feature | Specific to profile screen |

---

## 8. Interaction Model

- **BackButton**: Tap → navigate back (pop screen)
- **ChangePhotoLink**: Tap → open photo picker (camera/gallery action sheet)
- **InfoRow**: Tap → inline edit mode for that field (assumes edit capability)
- **SettingsRow [notifications]**: Toggle → immediate update, no confirmation
- **SettingsRow [privacy]**: Tap → push PrivacySettings screen
- **DeleteAccountButton**: Tap → confirmation dialog → if confirmed, re-authenticate → delete
- **FAB**: Tap → push EditProfile screen
- **Scroll**: Vertical scroll, header remains sticky

---

## 9. Design System Mapping

| Design Value | Token | Status |
|-------------|-------|--------|
| Background white | `surface.primary` | Matched |
| Text #1A1A1A | `text.primary` | Matched |
| Text #6B6B6B | `text.secondary` | Matched |
| Accent #2563EB | `color.accent.primary` | Matched |
| Border #E5E5E5 | `border.subtle` | Matched |
| FAB shadow | `elevation.3` | Matched |
| Delete red #DC2626 | `color.destructive` | Matched |
| Avatar background #F3F4F6 | — | NEW TOKEN REQUIRED: `surface.avatar.placeholder` |
| SettingsRow height 48px | — | NEW TOKEN REQUIRED: `size.settings-row` |

---

## 10. Implementation Plan

```
features/profile/
├── ProfileScreen.tsx
├── components/
│   ├── AvatarSection.tsx
│   ├── InfoSection.tsx
│   ├── SettingsSection.tsx
│   └── DangerZone.tsx
└── hooks/
    └── useProfileData.ts

shared/components/
├── InfoRow.tsx       (if not already extracted)
└── SettingsRow.tsx   (if not already extracted)
```

Reuse: BackButton, Avatar, Toggle, FAB from design system. InfoRow and SettingsRow should be promoted to shared if used by multiple features (check existing codebase). DeleteAccountButton is profile-specific, build inline.

---

## 11. Open Questions

- **Inline edit on InfoRow**: The design shows values but no edit affordance. Inferred tap-to-edit — confirm with designer.
- **Notifications toggle**: Does this call an API immediately or optimistically update? Assumed immediate API call with rollback on failure.
- **Photo picker**: Is there an existing photo picker flow or does this need to be built? Check codebase for `ImagePicker` or similar.
- **Delete account flow**: What is the re-authentication method? PIN, biometric, or password? Not specified in design.
- **Avatar placeholder**: Design shows a gray circle for users without a photo — need the placeholder color token (`surface.avatar.placeholder`).
