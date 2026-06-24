# 🎨 Day 1 Teaching Slides — v2 Outline

> 2 deck: **เช้า (คุม UNO Q + input)** / **บ่าย (เทรนด้วย Edge Impulse)**
> เนื้อหาต่อสไลด์กระชับพอขึ้นจอ ยกไป Canva/Gamma หรือแปลงเป็น PPTX (Sarabun) ได้เลย
> โทน: เหลือง/ดำ/ขาว (โลโก้ Coding Thailand) · font Sarabun/Inter · code block พื้นเข้ม

---

# ☀️ DECK เช้า — "คุม UNO Q ให้อยู่มือ"

### S1 · Title
- Coding Thailand 2026 — Edge AI Workshop · Day 1
- Arduino UNO Q × Modulino × Edge Impulse
- Mentor: ผศ.ดร.สัญชัย เอียดปราบ · คณะวิศวกรรมศาสตร์ ม.บูรพา

### S2 · งานนี้เดินยังไง (3 วัน)
- Day 1 = สร้างฐาน (วันนี้) · Day 2 = ต่อยอด prototype (ทำเอง) · Day 3 = pitch
- วันนี้: **เช้าคุมบอร์ด+input / บ่ายเทรน model ลงบอร์ด** ทุกทีมเดินเส้นเดียวกัน

### S3 · กฎห้อง
- มีคำถามยกมือ ไม่ต้องรอ · ทำเป็นทีม · ติดเกิน 5 นาทีบอก TA
- ใช้ AI/เครื่องมือได้ แต่อธิบายให้ได้ว่าทำอะไร

### S4 · Edge AI คืออะไร
- Cloud AI: ส่งขึ้น cloud / ช้า / ต้องเน็ต — Edge AI: ทำบนอุปกรณ์ / เร็ว / ไม่ต้องเน็ต / private
- ตัวอย่าง: fall detector, smart camera, ตรวจเสียงเครื่องจักร

### S5 · ทำไม UNO Q — สองสมอง ★
- **MCU side:** อ่าน sensor / คุม output ทันที (Modulino)
- **Linux side:** รัน AI, กล้อง USB, ไมค์ USB, คุย Edge Impulse
- จำไว้: input คนละแบบเข้าคนละฝั่ง — บ่ายจะได้ไม่งง

### S6 · วันนี้จะได้อะไร
- เช้า: บอร์ดเป็นของทีม + ต่อ input ครบ 3 (sensor/กล้อง/ไมค์)
- บ่าย: model V1 + รันบนบอร์ดจริง + prediction log + ส่ง fork

### S7 · Reset & First Boot — ทำไม
- บอร์ดวนมาจากที่อื่น รหัส/ชื่อ/Wi-Fi เดิมไม่ใช่ของเรา → ตั้งใหม่ให้เป็นของทีม
- ⚠️ บอร์ดไม่ boot? เช็ก **jumper pin** ค้างก่อน (ถอดออก)

### S8 · Reset — ทำยังไง (ไม่ต้อง flash)
- เสียบ USB → App Lab เห็นบอร์ด (login ให้เอง) → **Settings**
- ตั้ง 3 อย่าง: ชื่อ `team-XX-q` · Change password (จดไว้) · Wi-Fi ให้ตรงคอม
- เปิด SSH ไว้เผื่อ Day 2
- 🚦 ผ่าน = เห็นชื่อทีม + Wi-Fi ติด + รู้รหัส

### S9 · Modulino — Plug & Play
- ต่อ Qwiic เสียบแล้วใช้ ไม่ต้องบัดกรี · เสียบผิดด้านเข้าไม่ได้ (ปลอดภัย)
- ต่อเรียง: sensor ก่อน → output หลัง

### S10 · Input 1 — Sensor (Qwiic, MCU side)
- ต่อ Modulino Movement → เปิด example อ่านค่า → Run
- 🚦 ขยับ sensor แล้วเลขขยับตาม

### S11 · Input 2 — Webcam (USB, Linux side)
- เสียบ **powered USB hub** (มีไฟเลี้ยง) → เห็นภาพสด
- ⚠️ ตอนใช้กล้อง: บอร์ดอยู่ Wi-Fi **อย่าต่อบอร์ดเข้าคอม** ไม่งั้นหากล้องไม่เจอ
- เช็ก: `lsusb` / `ls /dev/video*`
- 🚦 เห็นภาพจากกล้อง

### S12 · Input 3 — Mic (USB, Linux side)
- เสียบ mic เข้า hub → `arecord -l` → พูดแล้ว level ขยับ
- 🚦 จับเสียงได้

### S13 · เช้า→บ่าย
- 3 input นี้ บ่ายเลือก 1 อย่างส่งเข้า Edge Impulse ไปสอน AI
- เริ่มคิด: ทีมอยากสอน AI ให้ "มอง / ฟัง / รู้สึก" อะไร?

---

# 🌤️ DECK บ่าย — "เทรนจริงด้วย Edge Impulse"

### S14 · Edge Impulse คืออะไร
- platform เทรน Edge AI ผ่านเว็บ ฟรี (free tier)
- Pipeline: **Collect → Train → Deploy → Test** (แล้ววนแก้)

### S15 · Bias — AI จำ shortcut ผิดจุด ★
- เก็บจากคนเดียว/ฉากเดียว/ระยะเดียว → AI จำ "คน/ฉาก/ระยะ" แทน class
- เช็ก: *"เปลี่ยนคน เปลี่ยนห้องแล้ว ยังทายได้ไหม?"*

### S16 · เลือก input + ออกแบบ class
- กี่ class? แต่ละ class ต่างกันด้วยอะไร? edge case ที่สับสน?
- เก็บกี่ตัวอย่าง/class? เก็บจากใคร/ที่ไหนบ้าง?

### S17 · เชื่อม UNO Q เข้า Edge Impulse ★
- **กล้อง/ไมค์:** shell บนบอร์ด → `edge-impulse-linux` → login → เลือก project
- **Modulino sensor:** ผ่าน App Lab brick หรือ data-forwarder (เข้าตรงแบบกล้องไม่ได้)
- 🚦 เห็น input ตัวเองไหลเข้า Studio ก่อน ค่อยเก็บ data

### S18 · เก็บ data ให้ดี
- แต่ละ class จำนวนใกล้กัน · สลับคน/มุม/แสง/ระยะ/ความเร็ว
- ให้คนที่ไม่ได้เก็บลองใช้ด้วย

### S19 · Create Impulse + Feature Explorer
- Feature Explorer = "ข้อมูลพร้อมไหม"
- จุดแต่ละ class แยกเป็นก้อน = ดี · ทับกันเยอะ = data สับสน กลับไปแก้ก่อน train

### S20 · Train + Confusion Matrix
- เลือก model ขนาดเล็กสุดที่ลง UNO Q ได้ (ดู option บนจอวันนั้น)
- Confusion Matrix = "โมเดลตอบได้แค่ไหน" · diagonal สูง = ดี · off-diagonal สูง = สับสน

### S21 · Deploy ลง UNO Q
- Edge Impulse → Deployment → target **Arduino UNO Q** → Build → download
- App Lab → import model → เลือก input → Run บนบอร์ด
- 🚦 ป้อน input จริงแล้ว model ตอบบนบอร์ดได้

### S22 · เทส 10 cases
- 5 ปกติ + 5 ท้าทาย (ก้ำกึ่ง / เร็วผิดปกติ / คนใหม่ / ใกล้เคียงแต่ไม่ใช่)
- จดลง `predictions.csv` · เคสไหนผิด? เพราะอะไร?
- (เหลือเวลา → เก็บ data เพิ่ม → V2)

### S23 · ส่งงาน + ปิดวัน
- Fork: กรอก hardware-check + model + predictions + รูปรันบนบอร์ด + ตอบ 3 ข้อ
- โชว์ทีมละ 1–2 นาที: โจทย์ / class / V1 ทำได้แค่ไหน / 1 อย่างที่เรียนรู้
- Day 2 = ปล่อยให้ทำเอง 🚀

---

## หมายเหตุตอนทำสไลด์จริง
- ใส่รูปบอร์ด/Modulino จริงจาก store.arduino.cc
- สไลด์ ★ (S5, S8, S15, S17) คือหัวใจ — ใส่ diagram ช่วย
- code block ใช้ฟอนต์ monospace พื้นเข้ม
