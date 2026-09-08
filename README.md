# GFIT ADLC Skill Core

Branch `main` เก็บกติกาสำหรับ Coding Agent และ ADLC Skills ที่นำไปใช้ซ้ำกับ project อื่นได้ โดยไม่ผูกกับภาษา, framework, artifact path, test command หรือ deployment target

```text
Intent → Generate ↔ Validate → Govern → Deploy → Observe
  ↑                                                   |
  └──────────────────── outcome signal ───────────────┘
```

## สิ่งที่อยู่ใน Branch นี้

```text
AGENTS.md                         กติกากลางและการเลือกใช้ Skills
.agents/skills/gfit-adlc-*/      ADLC Skill Core ทั้ง 6 modes
README.md                         คู่มือของ Core branch
```

| Mode | Skill | หน้าที่หลัก |
|---|---|---|
| Intent | `gfit-adlc-intent` | เปลี่ยน outcome ที่ต้องการให้เป็น hypothesis และตัวชี้วัด |
| Generate | `gfit-adlc-generate` | สร้างหรือแก้ spec, plan, implementation และ artifacts |
| Validate | `gfit-adlc-validate` | กำหนด proof ตรวจสิ่งที่สร้าง และส่ง feedback |
| Govern | `gfit-adlc-govern` | เตรียมหลักฐานให้มนุษย์ตัดสินใจ |
| Deploy | `gfit-adlc-deploy` | นำ revision ที่อนุมัติไปยัง target อย่างกู้คืนได้ |
| Observe | `gfit-adlc-observe` | วิเคราะห์ outcome signals และ guardrails จากหลักฐาน |

Generate และ Validate เป็นคนละความรับผิดชอบใน feedback loop เดียวกัน ส่วนมนุษย์เป็นผู้ยืนยัน Intent, อนุมัติขอบเขต, ตัดสิน release และ resolve ผลลัพธ์

## นำไปใช้กับ Project

1. คัดลอก `AGENTS.md` และ `.agents/` ไปไว้ที่ root ของ project
2. เพิ่ม Project Binding ที่ระบุ domain rules, paths, tools, commands, policies, metrics, decision owners และ deployment targets
3. ให้ Coding Agent อ่าน `AGENTS.md`, Project Binding และ `SKILL.md` ของ mode ที่ต้องใช้
4. เก็บ proposed, approved, executed และ observed states แยกจากกัน และบันทึกหลักฐานตามจริง

ถ้า Project Binding ยังไม่ครบ Agent ต้องทำส่วนที่ไม่ติดข้อจำกัดก่อน ห้ามเดา validation command, target, signal, approval หรือผลลัพธ์ที่ไม่มีหลักฐาน

## Branches

| Branch | ใช้สำหรับ | เนื้อหาเฉพาะ |
|---|---|---|
| `main` | นำ ADLC Skill Core ไปใช้กับ project | `AGENTS.md` และ `.agents/skills/` |
| `handson` | เรียน ADLC ผ่านการสร้างและปรับเกม | คู่มือ Step-by-step และ Game Project Binding |
| `docs` | นำเสนอหัวข้อ ADLC in Action | PowerPoint และ HTML visual companion |

สำหรับ Workshop ให้ clone branch `handson` โดยตรง:

```bash
git clone --branch handson <repository-url>
```

สำหรับสื่อนำเสนอ ให้ clone branch `docs`:

```bash
git clone --branch docs <repository-url>
```

## การดูแล Skill Core

แก้ `AGENTS.md` หรือ `.agents/skills/` บน `main` ก่อนเสมอ จากนั้นคัดลอกสอง path นี้ไปยัง `handson` แล้ว commit บน branch นั้น Branch `docs` ไม่มี Agent instructions หรือ Skills และทุก branch รักษาเนื้อหาเฉพาะของตัวเองโดยไม่ merge เข้าหากัน
