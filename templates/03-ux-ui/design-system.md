# Design System

## Project: [SYSTEM_NAME]

---

## 1. Color Palette

### Primary Colors
| Name | Hex | RGB | Usage |
|------|-----|-----|-------|
| Primary | #[HEX] | rgb(R,G,B) | Main actions, links |
| Primary Light | #[HEX] | rgb(R,G,B) | Hover states, backgrounds |
| Primary Dark | #[HEX] | rgb(R,G,B) | Active states |

### Secondary Colors
| Name | Hex | RGB | Usage |
|------|-----|-----|-------|
| Secondary | #[HEX] | rgb(R,G,B) | Secondary actions |
| Secondary Light | #[HEX] | rgb(R,G,B) | |
| Secondary Dark | #[HEX] | rgb(R,G,B) | |

### Neutral Colors
| Name | Hex | Usage |
|------|-----|-------|
| Gray-900 | #111827 | Headings, primary text |
| Gray-700 | #374151 | Body text |
| Gray-500 | #6B7280 | Secondary text |
| Gray-300 | #D1D5DB | Borders |
| Gray-100 | #F3F4F6 | Backgrounds |
| White | #FFFFFF | Cards, surfaces |

### Semantic Colors
| Name | Hex | Usage |
|------|-----|-------|
| Success | #10B981 | Success messages, positive |
| Warning | #F59E0B | Warning messages, caution |
| Error | #EF4444 | Error messages, destructive |
| Info | #3B82F6 | Information messages |

---

## 2. Typography

### Font Family
- **Headings**: [Font Name], sans-serif
- **Body**: [Font Name], sans-serif
- **Code**: [Font Name], monospace

### Type Scale
| Level | Size | Weight | Line Height | Usage |
|-------|------|--------|-------------|-------|
| H1 | 36px / 2.25rem | Bold (700) | 1.2 | Page titles |
| H2 | 30px / 1.875rem | Semibold (600) | 1.3 | Section headers |
| H3 | 24px / 1.5rem | Semibold (600) | 1.3 | Subsections |
| H4 | 20px / 1.25rem | Medium (500) | 1.4 | Card titles |
| Body | 16px / 1rem | Regular (400) | 1.5 | Body text |
| Small | 14px / 0.875rem | Regular (400) | 1.5 | Captions, labels |
| XSmall | 12px / 0.75rem | Regular (400) | 1.5 | Metadata, badges |

---

## 3. Spacing

**Base unit**: 4px

| Token | Value | Usage |
|-------|-------|-------|
| space-1 | 4px | Inline spacing |
| space-2 | 8px | Tight spacing |
| space-3 | 12px | Component internal |
| space-4 | 16px | Standard gap |
| space-6 | 24px | Section gap |
| space-8 | 32px | Large gap |
| space-12 | 48px | Section spacing |
| space-16 | 64px | Page sections |

---

## 4. Components

### Buttons

| Variant | Background | Text | Border | Usage |
|---------|-----------|------|--------|-------|
| Primary | Primary | White | None | Main actions |
| Secondary | White | Primary | Primary | Secondary actions |
| Outline | Transparent | Gray-700 | Gray-300 | Tertiary actions |
| Danger | Error | White | None | Destructive actions |
| Ghost | Transparent | Primary | None | Subtle actions |

**Sizes**: Small (32px), Medium (40px), Large (48px)
**States**: Default, Hover, Active, Focus, Disabled, Loading

### Inputs

| State | Border | Background | Label |
|-------|--------|-----------|-------|
| Default | Gray-300 | White | Gray-500 |
| Focus | Primary | White | Primary |
| Error | Error | Error-50 | Error |
| Disabled | Gray-200 | Gray-50 | Gray-400 |

### Cards
- Border radius: 8px
- Shadow: `0 1px 3px rgba(0,0,0,0.1)`
- Padding: space-4 (16px)

---

## 5. Breakpoints

| Breakpoint | Min Width | Container | Columns |
|------------|-----------|-----------|---------|
| Mobile | 0px | 100% | 4 |
| Tablet | 768px | 720px | 8 |
| Desktop | 1024px | 960px | 12 |
| Large | 1440px | 1200px | 12 |

---

## 6. Elevation / Shadow

| Level | Shadow | Usage |
|-------|--------|-------|
| 0 | none | Flat elements |
| 1 | `0 1px 2px rgba(0,0,0,0.05)` | Cards, raised elements |
| 2 | `0 4px 6px rgba(0,0,0,0.1)` | Dropdowns, tooltips |
| 3 | `0 10px 15px rgba(0,0,0,0.1)` | Modals, dialogs |
| 4 | `0 20px 25px rgba(0,0,0,0.15)` | Full-screen overlays |

---

## 7. Border Radius

| Token | Value | Usage |
|-------|-------|-------|
| rounded-sm | 4px | Small elements, badges |
| rounded-md | 8px | Buttons, inputs, cards |
| rounded-lg | 12px | Modals, large cards |
| rounded-xl | 16px | Feature sections |
| rounded-full | 9999px | Avatars, pills |

---

## 8. Icons

- **Style**: [Outlined / Filled / Rounded]
- **Library**: [Heroicons / Lucide / Material Icons]
- **Sizes**: 16px (sm), 20px (md), 24px (lg)
- **Color**: Inherit from text color
