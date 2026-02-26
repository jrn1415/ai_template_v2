# Wireframes

## Project: [SYSTEM_NAME]

---

## Screen Inventory

| # | Screen Name | URL/Route | Priority | Status |
|---|------------|-----------|----------|--------|
| 1 | Login | /login | Must | Draft |
| 2 | Dashboard | /dashboard | Must | Draft |
| 3 | [Screen] | /[route] | [Priority] | [Status] |

---

## Screen 1: Login

### Layout (Desktop)
```
┌─────────────────────────────────────────────────────┐
│                     HEADER / LOGO                    │
├─────────────────────┬───────────────────────────────┤
│                     │                               │
│                     │     ┌─────────────────┐       │
│                     │     │    Logo/Brand    │       │
│    Hero Image /     │     │                 │       │
│    Illustration     │     │  [Email Input]  │       │
│                     │     │  [Password]     │       │
│                     │     │  [Login Button] │       │
│                     │     │                 │       │
│                     │     │  Forgot? | Register     │
│                     │     └─────────────────┘       │
│                     │                               │
├─────────────────────┴───────────────────────────────┤
│                     FOOTER                           │
└─────────────────────────────────────────────────────┘
```

### Layout (Mobile)
```
┌──────────────────┐
│   HEADER/LOGO    │
├──────────────────┤
│                  │
│   [Logo/Brand]   │
│                  │
│  [Email Input]   │
│  [Password]      │
│  [Login Button]  │
│                  │
│  Forgot? | Reg   │
│                  │
├──────────────────┤
│     FOOTER       │
└──────────────────┘
```

### Elements
| Element | Type | Validation | Notes |
|---------|------|-----------|-------|
| Email | Text Input | Required, email format | Placeholder: "your@email.com" |
| Password | Password Input | Required, min 8 chars | Show/hide toggle |
| Login | Button (Primary) | - | Full width on mobile |
| Forgot Password | Link | - | Opens recovery flow |
| Register | Link | - | Opens registration |

### States
- **Default**: Empty form
- **Loading**: Button shows spinner
- **Error**: Red border on invalid fields + error message
- **Success**: Redirect to dashboard

---

## Screen 2: Dashboard

### Layout (Desktop)
```
┌─────────────────────────────────────────────────────┐
│  [Logo]   [Nav Items...]            [User] [Notif]  │
├────────┬────────────────────────────────────────────┤
│        │  Welcome, [Name]           [Date Range ▼]  │
│  Sidebar│                                           │
│        │  ┌────────┐ ┌────────┐ ┌────────┐         │
│  [Nav] │  │ Card 1 │ │ Card 2 │ │ Card 3 │         │
│  [Nav] │  │ Metric │ │ Metric │ │ Metric │         │
│  [Nav] │  └────────┘ └────────┘ └────────┘         │
│  [Nav] │                                           │
│  [Nav] │  ┌──────────────────────────────┐         │
│        │  │          Chart/Graph          │         │
│        │  │                              │         │
│        │  └──────────────────────────────┘         │
│        │                                           │
│        │  ┌──────────────────────────────┐         │
│        │  │      Recent Activity Table    │         │
│        │  │                              │         │
│        │  └──────────────────────────────┘         │
├────────┴────────────────────────────────────────────┤
│                     FOOTER                           │
└─────────────────────────────────────────────────────┘
```

### Elements
| Element | Type | Data Source | Notes |
|---------|------|-----------|-------|
| Metric Cards | Card Component | API: /dashboard/stats | Auto-refresh every 30s |
| Chart | Line/Bar Chart | API: /dashboard/chart | Filterable by date range |
| Activity Table | Data Table | API: /activities | Paginated, sortable |

---

## Screen 3: [SCREEN_NAME]

[Follow same structure]

---

## Navigation Flow

```
Login ──→ Dashboard ──→ [Feature A] ──→ [Detail View]
  │                 ├──→ [Feature B] ──→ [Edit View]
  │                 ├──→ [Settings]
  │                 └──→ [Profile]
  └──→ Register ──→ Onboarding ──→ Dashboard
```
