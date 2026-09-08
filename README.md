# ADLC in Action — Hands-on

Branch `handson` คือ Workshop แบบ Step-by-step สำหรับเรียน ADLC ผ่านการสร้างเกม ผู้เข้าร่วมเริ่มจาก repository ที่มี Agent instructions, Skills และ Project Binding แต่ยังไม่มีตัวเกม

สร้างเกมด้วย Coding Agent ที่คุณเลือก แล้วปรับเกมจากหลักฐาน ผ่าน Intent สองรอบ ใช้เวลาประมาณ 2–3 ชั่วโมง ไม่รวมติดตั้งเครื่องมือ

**ผู้ทดลองคนแรกคือคุณ** โครงเริ่มต้นตั้งใจไม่มีเกมสำเร็จรูป Code, tests และ artifacts จะเกิดขึ้นเมื่อทำทีละ Step

## สิ่งที่จะได้เมื่อจบ

- Intent 1: เกมทายเลข 1–100 ที่เล่นจบหนึ่งรอบได้
- Intent 2: เพิ่มปุ่ม “เล่นอีกครั้ง” และตรวจว่าการเริ่มรอบสองเพิ่มขึ้นหรือไม่
- Artifact chain: `intent → spec + plan → code + tests → validation → decision → release → observation → resolution`

```text
Intent → Generate ↔ Validate → Govern → Deploy → Observe
  ↑                                                   |
  └──────────────────── signal ใหม่ ─────────────────┘
```

Step เป็นเส้นทางการเรียน ไม่ใช่ pipeline บังคับของ ADLC ในงานจริง Generate กับ Validate ทำงานเป็น feedback loop และ Observe ส่ง signal กลับไปสร้าง Intent ใหม่ได้

## ก่อนเริ่ม

- ติดตั้ง [Git](https://git-scm.com/downloads), [uv](https://docs.astral.sh/uv/getting-started/installation/), Python 3 or later และ browser
- เปิด repo ใน Coding Agent ที่อ่าน/เขียนไฟล์และรันคำสั่งในเครื่องได้
- อ่าน [กติกา ADLC สำหรับ Agent](AGENTS.md) และ [Game Project Binding](game-profile.md)
- ทุก Agent ใช้ project-local Skills ชุดเดียวกันใต้ `.agents/skills/gfit-adlc-*`; ไม่ต้องติดตั้ง skill pack แบบ global
- หาก Agent ไม่ discover Skills อัตโนมัติ ให้ prompt ระบุ path ของ `SKILL.md` โดยตรง

**คัดลอก prompt ของแต่ละ Step ทั้งก้อน** ทุก prompt ระบุ `AGENTS.md`, `game-profile.md` และ Skills ที่ต้องใช้ การพิมพ์ชื่อ Step อย่างเดียวไม่รับประกันว่า Agent จะโหลด binding ครบ

## Step 0 — ตรวจความพร้อม (5–10 นาที)

```text
ฉันเป็นผู้ทดลอง ADLC in Action ทำเฉพาะ Step 0 ของ README.md
อ่าน AGENTS.md และ game-profile.md
ตรวจ frontmatter ของ Skills ทั้งหกไฟล์:
.agents/skills/gfit-adlc-intent/SKILL.md
.agents/skills/gfit-adlc-generate/SKILL.md
.agents/skills/gfit-adlc-validate/SKILL.md
.agents/skills/gfit-adlc-govern/SKILL.md
.agents/skills/gfit-adlc-deploy/SKILL.md
.agents/skills/gfit-adlc-observe/SKILL.md
ตรวจ Git, uv, Python 3 or later และความสามารถอ่าน/เขียนไฟล์กับรันคำสั่ง
ยังไม่สร้างเกม ไม่ติดตั้ง global skills และไม่ทำ Step ถัดไป
รายงาน Skills ทั้ง 6 และสิ่งที่ยังขาดก่อนเริ่ม
```

ตรวจเอง: Agent พบ Skills 6 ตัวและยังไม่มี `app/` ถ้าขาด Python ให้ติดตั้ง Python 3 เวอร์ชันที่ uv รองรับ โดยไม่ต้องตรงกับ minor version ที่กำหนดไว้ล่วงหน้า

## Step 1 — Intent 1: เล่นจบหนึ่งรอบ (10 นาที)

```text
ทำเฉพาะ Step 1 อ่าน AGENTS.md, game-profile.md และ .agents/skills/gfit-adlc-intent/SKILL.md
ใช้ Game Project Binding สร้าง artifacts/intent-001/intent.md สำหรับผู้เล่นใหม่ที่เริ่มและจบรอบแรกได้ด้วยตัวเอง
ใช้ target และ guardrails ของ Intent 1 จาก profile แยกสมมติฐานจากหลักฐานจริง
หยุดให้ฉันอ่าน ห้ามเริ่มเขียนเกม
```

**Govern checkpoint:** ตรวจ metric denominator, time window และข้อจำกัดของ self-test แล้วส่ง `ยืนยัน Intent 1 ตามไฟล์นี้`

## Step 2 — Generate ↔ Validate: Spec และ Plan (15 นาที)

```text
ทำเฉพาะ Step 2 อ่าน AGENTS.md, game-profile.md, .agents/skills/gfit-adlc-generate/SKILL.md และ .agents/skills/gfit-adlc-validate/SKILL.md
อ่าน Intent 1 ที่ยืนยันแล้ว สร้าง spec.md และ plan.md ใน artifacts/intent-001/
ให้ Validate กำหนด mapping G01–G10 ก่อน แล้วตรวจเอกสารและส่ง gaps กลับให้ Generate แก้
แบ่งงานเป็น game logic, web flow และ telemetry พร้อม proof ของแต่ละส่วน
ยังไม่เขียน implementation และหยุดให้ฉันตรวจ
```

**Govern checkpoint:** ตรวจ scope, commands และ acceptance mapping แล้วส่ง `อนุมัติ Spec และ Plan ของ Intent 1`

## Step 3 — Generate ↔ Validate: สร้าง v1 (25–40 นาที)

```text
ทำเฉพาะ Step 3 อ่าน AGENTS.md, game-profile.md, .agents/skills/gfit-adlc-generate/SKILL.md และ .agents/skills/gfit-adlc-validate/SKILL.md
Implement Spec/Plan ของ Intent 1 ที่อนุมัติแล้วตาม stack และ commands ใน profile
Validate กำหนด behavior proof ก่อน; ต้องเห็น failing test ด้วยเหตุผลที่คาดไว้ก่อน Generate ทำ implementation ทีละ slice
วน feedback จนตรวจ G01–G10 ครบ สร้าง environment และ lock files ตาม game-profile.md
เก็บหลักฐานจริงใน artifacts/intent-001/validation.md แล้วหยุดก่อน Govern
```

ตรวจเอง: อ่านหลักฐาน red/green อย่างน้อยหนึ่งกรณี แล้วรัน `uv run pytest -q`

## Step 4 — Govern v1 (10 นาที)

```text
ทำเฉพาะ Step 4 อ่าน AGENTS.md, game-profile.md และ .agents/skills/gfit-adlc-govern/SKILL.md
ตรวจ revision เทียบ Intent, Spec และ validation ของ Intent 1
สร้าง artifacts/intent-001/decision.md พร้อม recommendation Approve/Revise/Stop และให้ human_decision เป็น pending
ให้วิธีเปิดเกมชั่วคราวด้วย source=test และกรณี smoke test หยุดให้ฉันลองและตัดสินใจ
```

ทดลอง input ผิด, win, loss และ refresh แล้วตอบ `Approve สำหรับ localhost v1; ผล smoke test คือ ...` หรือ `Revise: ...`

## Step 5 — Deploy v1 บนเครื่อง (5 นาที)

```text
ทำเฉพาะ Step 5 อ่าน AGENTS.md, game-profile.md และ .agents/skills/gfit-adlc-deploy/SKILL.md
ตรวจว่า decision อนุมัติ revision ปัจจุบันและ target localhost แล้ว
สร้าง artifacts/intent-001/release.md พร้อม revision, วิธีเปิด/หยุด, health check และ rollback
เปิดเกมตาม local release command หากทำได้ ห้ามอ้างว่าเปิดแล้วจนกว่าจะตรวจ response จริง
```

เปิด [เกมบนเครื่อง](http://127.0.0.1:8000) และหยุดด้วย Ctrl+C

## Step 6 — Observe ↔ Govern v1 (10–15 นาที)

เก็บ session แบบ `source=real` โดยไม่ชี้นำให้ replay และรอ follow-up window ครบ Self-test หลาย session ต้องติดป้ายว่าเป็นผู้ทดลองคนเดียว

```text
ทำเฉพาะ Step 6 อ่าน AGENTS.md, game-profile.md, .agents/skills/gfit-adlc-observe/SKILL.md และ .agents/skills/gfit-adlc-govern/SKILL.md
วิเคราะห์ telemetry จริงของ v1 ลง artifacts/intent-001/observation.md
ระบุ source, cutoff, eligible sample, completion/replay และข้อจำกัด ถ้าข้อมูลไม่พอให้รายงาน insufficient evidence
สร้าง resolution.md พร้อม recommendation Resolved/Iterate/Stop แต่ให้ human_resolution เป็น pending
หยุดให้ฉันตัดสิน ห้ามสร้าง Intent 2 อัตโนมัติ
```

ตอบ `Resolved`, `Iterate` หรือ `Stop` พร้อมเหตุผล การเลือก Iterate เพื่อเรียนต่อไม่เท่ากับยืนยันว่า Intent 1 สำเร็จ

## Step 7 — Intent 2: อยากเริ่มรอบสอง (10 นาที)

```text
ทำเฉพาะ Step 7 อ่าน AGENTS.md, game-profile.md และ .agents/skills/gfit-adlc-intent/SKILL.md
อ่าน observation.md และ resolution.md ของ Intent 1
เปรียบเทียบปุ่มเล่นอีกครั้ง ระดับความยาก และคะแนนแบบสั้น ๆ แล้วใช้ intervention ที่ profile กำหนด
สร้าง artifacts/intent-002/intent.md ด้วย target และ guardrails ของ Intent 2
หยุดให้ฉันยืนยัน ห้ามแก้เกม
```

**Govern checkpoint:** ตรวจว่า Agent ไม่สรุปว่าเวลาเล่นนานเท่ากับความสนุก แล้วส่ง `ยืนยัน Intent 2 ตามไฟล์นี้`

## Step 8 — Generate ↔ Validate: Spec และ Plan v2 (10 นาที)

```text
ทำเฉพาะ Step 8 อ่าน AGENTS.md, game-profile.md, .agents/skills/gfit-adlc-generate/SKILL.md และ .agents/skills/gfit-adlc-validate/SKILL.md
สร้าง spec.md และ plan.md ใน artifacts/intent-002/ จาก Intent ที่ยืนยันแล้ว
ให้ Validate ตรวจ R01–R03, regression G01–G09 และส่วน G10 ที่เปลี่ยน แล้วส่ง gaps กลับให้ Generate แก้
ระบุ session/round lifecycle การรักษา baseline และหยุดก่อน implementation
```

**Govern checkpoint:** ตรวจว่าไม่มีฟีเจอร์เกิน scope แล้วส่ง `อนุมัติ Spec และ Plan ของ Intent 2`

## Step 9 — Generate ↔ Validate: สร้าง v2 (20–30 นาที)

```text
ทำเฉพาะ Step 9 อ่าน AGENTS.md, game-profile.md, .agents/skills/gfit-adlc-generate/SKILL.md และ .agents/skills/gfit-adlc-validate/SKILL.md
Implement เฉพาะ Plan ของ Intent 2 ทดสอบ replay หลังชนะ/แพ้และ regression
Validate กำหนด proof ก่อนและส่ง failures กลับให้ Generate แก้จนหลักฐานครบ
รักษา dependency lock และหลักฐาน v1 ถ้าไม่จำเป็นต้องเปลี่ยน
เก็บ artifacts/intent-002/validation.md จากผลจริง แล้วหยุดก่อน Govern
```

ตรวจเอง: replay รักษา session_id แต่สร้าง round_id ใหม่ และข้อมูล v1 ไม่ถูกติดป้ายใหม่

## Step 10A — Govern v2 (10 นาที)

```text
ทำเฉพาะ Step 10A อ่าน AGENTS.md, game-profile.md และ .agents/skills/gfit-adlc-govern/SKILL.md
สร้าง decision.md ของ Intent 2 จาก revision และหลักฐานปัจจุบัน
แนะนำ Approve/Revise/Stop ให้ human_decision เป็น pending และหยุดให้ฉัน smoke test กับตัดสินใจ
```

## Step 10B — Deploy v2 บนเครื่อง (5 นาที)

```text
ทำเฉพาะ Step 10B อ่าน AGENTS.md, game-profile.md และ .agents/skills/gfit-adlc-deploy/SKILL.md
ตรวจว่า decision อนุมัติ revision ปัจจุบันและ localhost v2
สร้าง release.md เปิด v2 ตาม command ใน profile และตรวจ response กับ telemetry labels ตามจริง
หยุดก่อน Observe
```

## Step 11 — Observe ↔ Govern → Intent ถัดไป (15 นาที)

```text
ทำเฉพาะ Step 11 อ่าน AGENTS.md, game-profile.md, .agents/skills/gfit-adlc-observe/SKILL.md และ .agents/skills/gfit-adlc-govern/SKILL.md
ใช้ telemetry/events.jsonl จากการเล่นจริง วิเคราะห์ v1/v2 ลง artifacts/intent-002/observation.md
ระบุ source, cutoff, eligible sample, completion/replay และข้อจำกัด ถ้าข้อมูลไม่พอให้รายงาน INSUFFICIENT EVIDENCE
ใช้ observation.md เป็นฐานของ resolution ห้ามสร้างข้อมูลหรือตัวเลขสมมติแทนผลผู้เล่น
สร้าง resolution.md พร้อม recommendation แต่ให้ human_resolution เป็น pending
หยุดให้ฉันตัดสิน เสนอ Intent ถัดไปได้แต่ห้ามสร้างหรือ implement อัตโนมัติ
```

ตรวจเอง: สูตรและตัวหารถูกต้อง แยก test data จาก real data และไม่สรุปว่า Intent สำเร็จเมื่อหลักฐานไม่พอหรือ guardrail ไม่ผ่าน

## หยุดและกลับมาทำต่อ

บอก Agent ว่า “หยุดที่ Step นี้” กลับมาด้วยการคัดลอก prompt เต็มของ Step ที่ต้องการทำต่อ ซึ่งระบุ `AGENTS.md`, `game-profile.md` และ Skills ที่เกี่ยวข้อง ใช้ local Git commit เป็น audit trail ได้หลังตรวจ diff ห้าม commit `.env`, `.venv` หรือ `telemetry/events.jsonl`

## Completion checklist

- [ ] เกมทั้งสอง Intent ผ่าน acceptance ที่เกี่ยวข้องและคุณทดลองจริง
- [ ] แต่ละ Intent มี intent, spec, plan, validation, decision, release, observation และ resolution
- [ ] Intent 2 ใช้ข้อมูลจริงที่ระบุ sample, cutoff และข้อจำกัดชัดเจน
- [ ] ไม่มีการแต่งผลตรวจ การอนุมัติ release หรือข้อมูลผู้เล่น
- [ ] อธิบายได้ว่า Generate ↔ Validate ทำงานคู่กันและ Observe ส่ง signal กลับ Intent อย่างไร

จด feedback ใน `artifacts/pilot-notes.md`: Agent/model, Step ที่ติด, เวลาที่ใช้, prompt ที่ต้องแก้ และความต่างจากผลคาดหวัง โดยไม่ใส่ข้อมูลบัญชีหรือข้อมูลส่วนบุคคล
