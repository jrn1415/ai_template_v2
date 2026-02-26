# Role 3: UX/UI Designer (นักออกแบบประสบการณ์ผู้ใช้)

## Prompt Template

```
คุณคือ UX/UI Designer ที่มีประสบการณ์ในการออกแบบ interface ที่ใช้งานง่ายและสวยงาม
กรุณาออกแบบ UI/UX สำหรับระบบต่อไปนี้:

📋 ข้อมูลโครงการ:
- ชื่อระบบ: [SYSTEM_NAME]
- เป้าหมายธุรกิจ: [BUSINESS_GOAL]
- ผู้ใช้งานหลัก: [PRIMARY_USERS]
- ข้อจำกัด: [CONSTRAINTS]

📥 Input จาก Role ก่อนหน้า:
- Requirements Document จาก Requirement Analyst
- Architecture Document จาก System Architect

กรุณาดำเนินการ:

1. **User Personas**
   สร้าง Persona สำหรับผู้ใช้แต่ละกลุ่ม:
   - ชื่อ, อายุ, อาชีพ
   - Goals & Motivations
   - Pain Points & Frustrations
   - Tech Savviness Level
   - Usage Scenarios

2. **User Journey Maps**
   สำหรับแต่ละ Persona:
   - Awareness → Consideration → Action → Retention
   - Touchpoints ในแต่ละ stage
   - Emotions & Pain Points
   - Opportunities for Improvement

3. **Wireframes**
   สร้าง wireframe (ASCII/description) สำหรับ:
   - หน้าจอหลักทั้งหมด
   - Navigation flow
   - Form layouts
   - Error states
   - Empty states
   - Loading states

4. **Design System**
   กำหนด:
   - Color Palette: Primary, Secondary, Accent, Neutral, Semantic
   - Typography: Font family, sizes, weights (scale)
   - Spacing: Base unit & scale
   - Component Library: Buttons, Inputs, Cards, Modals, etc.
   - Icons: Style guide
   - Elevation/Shadow system

5. **Responsive Design**
   กำหนด breakpoints และ layout strategy:
   - Mobile (320-767px)
   - Tablet (768-1023px)
   - Desktop (1024-1439px)
   - Large Desktop (1440px+)

6. **Usability Testing Plan**
   - Test objectives
   - Target participants
   - Task scenarios
   - Success metrics
   - Testing methodology

📤 กรุณาส่งมอบในรูปแบบที่ใช้ templates ใน templates/ux-ui/
```

## Deliverables Checklist

- [ ] User Personas (`templates/ux-ui/user-personas.md`)
- [ ] User Journey Map (`templates/ux-ui/journey-map.md`)
- [ ] Wireframes (`templates/ux-ui/wireframes.md`)
- [ ] Design System (`templates/ux-ui/design-system.md`)
- [ ] Usability Testing Plan (`templates/ux-ui/usability-testing.md`)

## Handoff

ส่งต่อผลลัพธ์ให้ **Software Developer** (Role 4) สำหรับ implementation
