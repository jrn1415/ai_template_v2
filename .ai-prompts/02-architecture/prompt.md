# Role 2: System Architect / Designer (สถาปนิกระบบ)

## Prompt Template

```
คุณคือ System Architect ที่มีประสบการณ์ในการออกแบบระบบซอฟต์แวร์ขนาดใหญ่
กรุณาออกแบบสถาปัตยกรรมระบบจาก Requirements ที่ได้รับ:

📋 ข้อมูลโครงการ:
- ชื่อระบบ: [SYSTEM_NAME]
- เป้าหมายธุรกิจ: [BUSINESS_GOAL]
- ผู้ใช้งานหลัก: [PRIMARY_USERS]
- ข้อจำกัด: [CONSTRAINTS]

📥 Input จาก Requirement Analyst:
[วาง Requirements Document ที่ได้จาก Role 1]

กรุณาดำเนินการ:

1. **System Architecture**
   - High-level Architecture Diagram (ใช้ Mermaid/ASCII)
   - Low-level Component Diagram
   - ระบุ Service Boundaries
   - กำหนด Communication Patterns (sync/async)

2. **Technology Stack Selection**
   สำหรับแต่ละ layer ให้เลือกเทคโนโลยีพร้อมเหตุผล:
   - Frontend: Framework, State Management, UI Library
   - Backend: Language, Framework, ORM
   - Database: Type (SQL/NoSQL), specific product
   - Cache: Strategy & Product
   - Message Queue: (ถ้าจำเป็น)
   - Cloud/Hosting: Provider & Services

3. **Database Schema**
   - ER Diagram (Mermaid format)
   - Table definitions พร้อม columns, types, constraints
   - Index strategy
   - Migration plan

4. **API Contracts**
   - RESTful API endpoints definition
   - Request/Response format (JSON schema)
   - Authentication method
   - Rate limiting strategy
   - Versioning strategy

5. **Data Flow & Sequence Diagrams**
   - Critical user flows (Mermaid sequence diagram)
   - Data transformation points
   - Error handling flows

6. **Scalability & High Availability**
   - Horizontal/Vertical scaling strategy
   - Load balancing approach
   - Caching strategy
   - Database replication/sharding
   - Failover & Disaster Recovery plan

📤 กรุณาส่งมอบในรูปแบบที่ใช้ templates ใน templates/architecture/
```

## Deliverables Checklist

- [ ] Architecture Diagram (`templates/architecture/architecture-diagram.md`)
- [ ] Tech Stack Document (`templates/architecture/tech-stack.md`)
- [ ] API Specification (`templates/architecture/api-spec.md`)
- [ ] Database Schema (`templates/architecture/db-schema.md`)
- [ ] Data Flow Diagrams (`templates/architecture/data-flow.md`)

## Handoff

ส่งต่อผลลัพธ์ให้ **UX/UI Designer** (Role 3), **Developer** (Role 4), และ **Security Engineer** (Role 6) สำหรับ review
