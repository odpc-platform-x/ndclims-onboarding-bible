# HANDOFF — NDCLIMS Onboarding Bible

อ่านไฟล์นี้ก่อนแก้ `index.html` (= onboarding bible) หรือ `ndclims-it-runbook.html` ในโฟลเดอร์นี้

## นี่คืออะไร

เอกสาร onboarding แบบ interactive HTML (self-contained, ไม่มี build step) สำหรับระบบ NDCLIMS (Thai national disease-control LIMS) แยก 2 เล่ม:

| ไฟล์                      | อ่านโดย                             | เนื้อหา                                                                      |
| ------------------------- | ----------------------------------- | ---------------------------------------------------------------------------- |
| `index.html`              | เจ้าหน้าที่ / Lab Admin / ผู้บริหาร | ขั้นตอน 0–7 ในการเริ่มใช้ระบบที่ deploy แล้ว, งานประจำวัน, เตรียมไฟล์ import |
| `ndclims-it-runbook.html` | IT / super admin                    | ตั้งค่า tenant ใหม่, หนุนงาน import, integration, ops ระบบ live              |

`index.html` คือไฟล์เดียวกับ onboarding bible เดิม (เปลี่ยนชื่อเป็น `index.html` เพื่อให้ root path ของ GitHub Pages เปิดตรงเข้าเล่มนี้ — ดูหัวข้อ Hosting ด้านล่าง)

Publish อยู่ที่: [odpc-platform-x.github.io/ndclims-onboarding-bible](https://odpc-platform-x.github.io/ndclims-onboarding-bible) (bible) และ `.../ndclims-it-runbook.html` (IT) — repo: `github.com/odpc-platform-x/ndclims-onboarding-bible`

ไฟล์อยู่นอก repo `ndclims` โดยตั้งใจ (`~/Developer/bible/ndclims/` — คนละที่กับ repo โปรเจกต์จริงที่ `~/Developer/hybridge/ndclims/`) — ไม่ใช่ source code ของโปรเจกต์ เป็นเอกสาร แต่ **ทุก fact ในนี้ต้องตรงกับโค้ดจริงในโปรเจกต์ NDCLIMS** เพราะ verify มาจากการอ่านโค้ดตรงๆ ไม่ใช่เดา ดู [`README.md`](./README.md) สำหรับลิงก์ระบบจริงและ tech stack

## กฎเวลาแก้

1. **ห้ามเขียนจากความจำ** — ถ้า field/validation/endpoint/role อะไรเปลี่ยนใน backend ต้องเปิดไฟล์โค้ดจริงอ่านก่อนแก้ตาราง/ข้อความในเอกสาร
2. **grep หา string เดิมก่อนแก้** — fact หนึ่งตัวมักปรากฏซ้ำหลายจุด (เช่น กฎ column ของไฟล์ import ปรากฏทั้งในตารางคอลัมน์ appendix และตาราง error-translation ที่หน้า "เตรียมไฟล์ยังไงให้ผ่าน") แก้จุดเดียวแล้วลืมจุดอื่น = เอกสารขัดแย้งกันเอง
3. **แก้ข้อความไทยด้วย python3 + utf-8 เท่านั้น** — `sed`/`perl` เปล่าๆ ใน shell ของเครื่องนี้ทำ encoding ไทยพังแบบเงียบ (พิสูจน์แล้วรอบก่อน) ใช้ python script อ่าน/เขียนด้วย `encoding='utf-8'` ชัดเจน หรือใช้ Edit tool ตรงๆ
4. **verify หลังแก้เสมอ**: เสิร์ฟ local ด้วย `python3 -m http.server` (ห้ามเปิดแบบ `file://` — browser บล็อกบาง fetch/localStorage), เช็ก light + `data-theme="dark"` ทั้งคู่, เช็ก `documentElement.scrollWidth <= clientWidth` (ไม่ล้นแนวนอน)

## Source-of-truth mapping (ต้องเปิดอ่านไฟล์เหล่านี้ในโปรเจกต์ `ndclims` จริง ก่อนแก้ fact ที่เกี่ยวข้อง)

อ้างอิงจาก path ใน repo `ndclims` (สมมติ path ท้องถิ่นเดิม `~/Developer/hybridge/ndclims/` — เช็ค path จริงก่อนใช้ เพราะ repo อาจย้าย):

| เนื้อหาในเอกสาร                                                                                                     | ไฟล์โค้ดต้นทาง                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| คอลัมน์/validation rule/error message ของไฟล์ import ทั้ง 5 ชนิด (users, patients, lab-tests, packages, lab-orders) | `apps/backend/src/modules/import/import.constants.ts`, `apps/backend/src/modules/import/import.service.ts`                                       |
| สิทธิ์เข้าถึง import (`SETTINGS_MANAGE`), branch ของผู้อัปโหลด                                                      | `apps/backend/src/modules/import/import.routes.ts`                                                                                               |
| ลำดับ onboarding บังคับ, การสร้าง company+branch+admin                                                              | `apps/backend/src/modules/super-admin/super-admin.service.ts`                                                                                    |
| central catalog (หมวดหมู่/รายการตรวจ default)                                                                       | `apps/backend/src/modules/super-admin/central-catalog.service.ts` (หรือชื่อไฟล์ที่เทียบเท่าในโมดูลเดียวกัน — เช็คตำแหน่งจริงถ้าไฟล์ถูก refactor) |
| plan × feature entitlement matrix                                                                                   | `supabase/migrations/20260724000001_control_plane_entitlements.sql`                                                                              |
| 8 role ที่ seed มาให้, permission format                                                                            | `supabase/migrations/20260101000001_initial_schema.sql`                                                                                          |
| feature gate map (เมนูไหนโผล่ตาม plan)                                                                              | `apps/backend/src/app.ts`                                                                                                                        |

ถ้าเปิดแล้วไฟล์/path ไม่ตรง (ถูกย้าย/rename) — หาไฟล์จริงด้วย `grep`/`find` ในโปรเจกต์ก่อน อย่าสมมติว่า path เดิมยังถูก

## Design system (คงไว้เวลาแก้/เพิ่มเนื้อหา)

- Token 3 ชั้นเหมือนกันทั้ง 2 ไฟล์: `:root` (light) → `@media (prefers-color-scheme:dark){:root:not([data-theme="light"])}` → `:root[data-theme="dark"]` (manual override) — แก้สีต้องแก้ทั้ง 3 บล็อกให้ตรงกัน
- ธีมสองไฟล์ตั้งใจให้ต่างกันเพื่อบอกว่ากำลังเปิดเล่มไหน — ห้ามผสม:
  - Onboarding bible = "Verification Ledger" (เขียว/emerald accent, tick-ruler/checklist motif)
  - IT runbook = "Instrument Register" (brass/amber accent, grid-paper/control-room motif)
- Self-contained เด็ดขาด — ห้ามอ้าง CDN/font/รูปภาพภายนอก ทุกอย่างต้อง inline (รูปภาพ = base64 data URI)
- `<meta charset="utf-8">` ต้องอยู่ครบ
- Cross-link ระหว่างไฟล์เป็น relative path เสมอ (`./ndclims-it-runbook.html` ไม่ใช่ absolute URL) — เผื่อย้ายโฟลเดอร์/host ที่ path ไหนก็ได้

## Hosting บน GitHub Pages

- ชื่อไฟล์ปัจจุบันเป็น lowercase-kebab-case อยู่แล้ว ใช้ได้ตรงกับ GH Pages (host case-sensitive) ไม่ต้องเปลี่ยน
- ลิงก์ข้ามไฟล์เป็น relative อยู่แล้ว → ใช้ได้ทั้งบน user page (`username.github.io/`) และ project page (`username.github.io/repo/`) โดยไม่ต้องแก้อะไร
- `index.html` (= copy ของ onboarding bible) ทำไว้แล้ว ให้ root path ของเว็บเปิดตรงเข้าเล่มผู้ใช้ทันที — ถ้าแก้เนื้อหา bible ต้องแก้ `index.html` โดยตรง (เป็นไฟล์เดียวกัน ไม่ใช่ symlink)
- ถ้าจะผูก custom domain ต้องเพิ่มไฟล์ `CNAME` แยกต่างหาก ไม่กระทบไฟล์ 2 ไฟล์นี้เลย
