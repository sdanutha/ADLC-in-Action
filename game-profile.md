# Game Example Scenario — Project Binding

ไฟล์นี้เติมข้อกำหนดเฉพาะเกมให้ reusable `gfit-adlc-*` Skills ใช้ระหว่าง Hands-on เท่านั้น ข้อกำหนดเหล่านี้ไม่ใช่ส่วนหนึ่งของ ADLC Skill Core

## How to use this binding

- อ่านไฟล์นี้ก่อนทำทุก Step ใน `README.md` ไฟล์นี้เป็นข้อกำหนดหลักสำหรับ stack, paths, acceptance cases, metrics และ local release ของ Game Example Scenario
- ทำเฉพาะ Step ที่ผู้เรียนเลือกและหยุดที่ checkpoint ของ Step นั้น ห้ามทำสอง Intent ภายใน turn เดียว
- เก็บ artifacts และหลักฐานของ Intent ก่อนหน้าไว้ รวมถึงผลที่ fail ห้ามเขียนทับเพื่อทำให้ผลดูผ่าน
- การยืนยัน Intent และการอนุมัติ Spec/Plan เป็น lightweight Govern checkpoints ใช้ workflow เต็มของ `gfit-adlc-govern` ก่อน Deploy และหลัง Observe
- คำสั่งให้เริ่ม Step อนุญาตเฉพาะงานของ Step นั้น ไม่ใช่การอนุมัติ artifact, revision หรือ release
- บันทึก human decision จากคำตอบจริงของผู้เรียนเท่านั้น Agent ให้ recommendation ได้แต่ตัดสินใจแทนไม่ได้

## Creation and execution rules

- สร้าง application files เฉพาะ implementation Steps เท่านั้น ระหว่างสร้าง Spec/Plan ให้หยุดก่อนเขียน code
- เมื่อเริ่ม implementation ให้ใช้ Python 3 ที่มีอยู่ในเครื่อง สร้าง `pyproject.toml` และ `uv.lock` โดยไม่สร้าง `.python-version` เพื่อล็อก minor version เก็บ dependency lock เดิมใน Step ต่อไป เว้นแต่มีเหตุผลที่บันทึกไว้
- แยก game logic ออกจาก HTTP rendering เพื่อทดสอบได้ ใช้ injected randomness ใน tests
- ใช้ random opaque session cookie และ server-side runtime state ห้ามเปิดเผยเลขลับผ่าน HTML, cookie, telemetry หรือ production test endpoint
- จัดทำและบันทึกวิธีตั้งค่า `source=test` สำหรับ validation กับ smoke checks และ `source=real` สำหรับ observation ที่ไม่ชี้นำ ค่าเริ่มต้นเป็น test และ telemetry ต้องอยู่ในเครื่อง
- ห้ามเปลี่ยน label ของ events เดิม เมื่อเปลี่ยน source หรือ version ให้เริ่ม session ใหม่
- Map automated และ manual evidence กับ acceptance IDs ในไฟล์นี้ แก้ test ได้เมื่อมีเหตุผลจาก requirement ที่บันทึกไว้ ห้าม skip หรือลด assertion เพื่อสร้างผล green
- Generated tests ไม่ใช่หลักฐานอิสระในตัวเอง ต้องบันทึก command, result และ manual checks ที่เกี่ยวข้องตามจริง

## Step reporting contract

จบแต่ละ Step ด้วย:

- Step และ Skills ที่ใช้อยู่
- ไฟล์ที่สร้างหรือแก้
- คำสั่งและผลจริง หรือ `NOT RUN`
- สิ่งที่ผู้เรียนต้องตรวจหรือตัดสินใจ
- Step ถัดไปที่พร้อมทำ

แยก technical validation ออกจาก outcome observation เสมอ

## Environment and outputs

- Python 3 or later โดยไม่ล็อก minor version, FastAPI, Jinja2, HTML/CSS, pytest และ uv
- Entrypoint: `app.main:app`
- Test command: `uv run pytest -q`
- Local release: `uv run uvicorn app.main:app --host 127.0.0.1 --port 8000`
- Intent artifacts: `artifacts/intent-001/` และ `artifacts/intent-002/`
- Runtime telemetry: `telemetry/events.jsonl`
- Bind เฉพาะ loopback ไม่มี Node, custom JavaScript, database, LLM API, paid service, public hosting, remote deployment, remote push หรือ global configuration changes

## Game contract

- หน้าแรกมีคำอธิบายและปุ่มเริ่มเกม ภาษาไทย
- สุ่มจำนวนเต็ม 1–100; ทายได้ 7 ครั้ง; ค่าซ้ำที่เป็นเลขถูกช่วงนับเป็นอีกครั้ง
- คำตอบต่ำกว่าเลขลับแสดง “ต่ำไป”; สูงกว่าแสดง “สูงไป”; ถูกแสดงชนะ
- ครั้งที่ 7 ถ้าถูกยังชนะ ถ้าผิดจึงแพ้; เฉลยเลขเมื่อจบเท่านั้น
- ค่าว่าง ไม่ใช่จำนวนเต็ม หรือนอกช่วงถูกปฏิเสธโดยไม่ลดจำนวนครั้ง
- หลังจบไม่รับการทายเพิ่ม ไม่แก้ผลลัพธ์ และไม่บันทึกจบซ้ำ
- v1 ไม่มีปุ่มเล่นซ้ำในหน้าจบ แต่กลับหน้าแรกเพื่อเริ่มรอบใหม่ได้ เป็น baseline ที่มี friction
- v2 เพิ่มปุ่มเล่นอีกครั้งหลังชนะหรือแพ้ เริ่มด้วย 7 ครั้งและเลขสุ่มใหม่ ไม่แสดงปุ่มระหว่างรอบ
- Refresh หรือ redirect ไม่เพิ่มจำนวนทายและไม่เริ่มรอบเอง ใช้ POST แล้ว redirect ไป GET
- เลขลับไม่อยู่ใน HTML, cookie หรือ telemetry ระหว่างเล่น; session ต่างกันไม่แชร์สถานะ
- ไม่มีคะแนน ระดับความยาก leaderboard เสียง login หรือฐานข้อมูลในเส้นทางหลัก

## Acceptance cases

| ID | กรณีที่ต้องพิสูจน์ |
|---|---|
| G01 | เริ่มรอบอยู่ในสถานะ playing และมี 7 ครั้ง |
| G02 | ต่ำไป/สูงไปถูกต้อง และ valid guess ลดจำนวนครั้งหนึ่ง |
| G03 | ทายถูกชนะ รวมถึงถูกครั้งที่ 7 |
| G04 | ผิดครบ 7 ครั้งแพ้ |
| G05 | input ผิดถูกปฏิเสธ จำนวนครั้งและ guess events ไม่เปลี่ยน |
| G06 | จบแล้วไม่รับทายเพิ่มและไม่มี `round_completed` ซ้ำ |
| G07 | สอง session แยกกันและเลขลับไม่รั่วก่อนจบ |
| G08 | หน้าเว็บเริ่ม/ทาย/ผลจบใช้ได้จริง และ refresh ไม่ทำ action ซ้ำ |
| G09 | event schema ถูกต้อง ใช้เวลา UTC และแยก version/source ได้ |
| G10 | v1 จบแล้วไม่มีปุ่ม replay; กลับ home เริ่มรอบใหม่ได้ใน session เดิม |
| R01 | v2 ชนะ/แพ้แล้ว replay ได้ โดย reset attempts/status/round_id |
| R02 | replay รักษา session_id เพิ่ม round_index และ refresh ไม่เพิ่มรอบ |
| R03 | v2 ไม่มี replay ระหว่างเล่น; G01–G09 ยังผ่าน และปรับ G10 เฉพาะส่วนที่เปลี่ยน |

Tests คุมเลขลับผ่าน injected randomness หรือ fixture ห้ามสร้าง secret endpoint ในแอปจริง ผล PASS ต้องมาจากการรันจริง

## Telemetry contract

แต่ละ JSONL event มี `event_id`, UTC ISO 8601 `timestamp`, opaque `session_id`, `round_id`, `round_index`, `version` (`v1`/`v2`), `source` (`real`/`test`) และ `event` (`round_started`/`guess_submitted`/`round_completed`)

- `guess_submitted` มี `attempt` 1–7 และ `result` (`low`/`high`/`correct`)
- `round_completed` มี `outcome` (`won`/`lost`) และ `attempts_used`
- การทายครั้งสุดท้ายบันทึก `guess_submitted` ก่อน `round_completed`
- ไม่เก็บเลขลับหรือ input ดิบที่ไม่จำเป็น
- browser session หนึ่งใน version เดียวใช้ session_id เดิมเมื่อกลับ home หรือ replay
- เปลี่ยน version หรือ restart จน state หายให้เริ่ม session ใหม่ ห้ามรวมข้อมูลข้ามช่วงโดยไม่ระบุ

## Intent metrics

**Intent 1:** ผู้เล่นใหม่เริ่มและจบรอบแรกได้ด้วยตัวเอง

- Pilot target: อย่างน้อย 4 จาก 5 eligible sessions จบรอบแรกภายใน 5 นาที
- Guardrails: ไม่มี observed blocking error และไม่เปิดเผยเลขลับก่อนจบ

**Intent 2:** ลด friction เพื่อให้ผู้เล่นสมัครใจเริ่มรอบที่สอง

- Intervention: ปุ่มเล่นอีกครั้งหลังจบ
- Target: replay rate เพิ่มอย่างน้อย 15 percentage points จาก v1
- Guardrails: completion rate ลดไม่เกิน 5 percentage points และไม่มี observed blocking error

**Completion rate:** session ที่จบรอบแรกภายใน 5 นาที ÷ session ที่เริ่มรอบแรกและมี follow-up ครบ 5 นาที

**Replay rate:** session ที่เริ่มรอบสองภายใน 5 นาทีหลังจบรอบแรก ÷ session ที่จบรอบแรกและมี follow-up ครบ 5 นาที

นับ session ไม่ใช่ events หรือจำนวนรอบ ตัวหารเป็นศูนย์ให้รายงาน N/A แยก test data จาก real data เสมอ Self-test หลาย session จากคนเดียวไม่ใช่ผู้เล่นอิสระหลายคน และ replay เป็น proxy ไม่ใช่หลักฐานโดยตรงว่าผู้เล่นสนุก หาก sample หรือ follow-up window ไม่พอให้รายงาน `INSUFFICIENT EVIDENCE` โดยไม่สร้างข้อมูลทดแทน
