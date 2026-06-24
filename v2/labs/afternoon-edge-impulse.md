# ☀️ Afternoon Lab — เทรนจริงด้วย Edge Impulse

> จบบ่ายนี้: train model V1 ได้ + ลง UNO Q รันจริง + เทส 10 cases
> แต่ละทีมเลือก **1 input** (จาก 3 ตัวที่ต่อเช้านี้) ไปสอน AI

---

## ส่วนที่ 1 — เลือก input + ออกแบบ class (13:00–13:30)

ทีมเลือกว่าจะสอน AID ให้ "มอง / ฟัง / รู้สึก" อะไร แล้วนิยาม class:
- กี่ class? แต่ละ class ต่างกันด้วยอะไร?
- จะเก็บกี่ตัวอย่าง/class? เก็บจากใคร ที่ไหน บ้าง?

⚠️ **bias:** ถ้าเก็บจากคนเดียว/ฉากเดียว/ระยะเดียว AI จะจำ "คน/ฉาก/ระยะ" แทน "class" → เปลี่ยนเงื่อนไขแล้วทายพัง
เช็กง่าย: *"ถ้าเปลี่ยนคนหรือเปลี่ยนห้องแล้ว ยังทายได้ไหม?"*

---

## ส่วนที่ 2 — เชื่อม UNO Q เข้า Edge Impulse (13:30–14:00) ★

> ทางเข้าต่างกันตาม input — เลือกตามที่ทีมจะใช้

### ถ้าใช้ Webcam หรือ Mic (Linux side)
เปิด shell บนบอร์ด (`>_` ใน App Lab) แล้ว:
```bash
edge-impulse-linux
```
- login บัญชี Edge Impulse ของทีม → เลือก/สร้าง project
- กล้อง/ไมค์จะถูกจับเป็น sensor ของ device โดยตรง

### ถ้าใช้ Modulino sensor (MCU side)
sensor อยู่ฝั่ง MCU ส่งตรงเข้า Studio เหมือนกล้อง/ไมค์ไม่ได้ ใช้ทางใดทางหนึ่ง:
- **ผ่าน App Lab Edge Impulse brick / ตัวอย่างที่ Arduino เตรียมไว้** (ง่ายสุดสำหรับเด็ก) หรือ
- **Data forwarder over serial:** รัน sketch อ่าน sensor พิมพ์ค่าออก serial แล้วใช้ `edge-impulse-data-forwarder` ส่งเข้า Studio

> 🚦 **Checkpoint 5:** เห็น input ตัวเอง (ภาพ/เสียง/ค่าตัวเลข) ไหลเข้า Edge Impulse Studio จริง
> ❌ ยังไม่เห็น data → หยุดตรงนี้ อย่าเพิ่งเก็บ dataset เรียก TA บอกว่าใช้ input อะไร ค้าง step ไหน

---

## ส่วนที่ 3 — เก็บ data + Train V1 (14:00–14:45)

1. **Data acquisition** → เก็บตาม class ที่ออกแบบ
   - สลับคน / มุม / แสง / ระยะ / ความเร็ว ให้หลากหลาย
   - แต่ละ class จำนวนใกล้กัน
2. **Create Impulse** → เลือก processing block ตาม input + learning block = Classification
3. **Generate features** → ดู scatter / Feature Explorer
   - จุดแต่ละ class แยกเป็นก้อน = ดี / ทับกันเยอะ = data ยังสับสน กลับไปแก้ก่อน train
4. **Train** → ได้ V1
   - เลือก model ขนาด **เล็กที่สุดที่ลง UNO Q ได้** (ดู option ตอน deploy/optimization ใน Studio — ชื่อ option ให้ดูบนจอจริงวันนั้น อย่าจำค่าตายตัวมา)
   - อ่าน **Confusion Matrix:** diagonal สูง = ดี / off-diagonal สูง = สับสน

> 🚦 **Checkpoint 6:** มี model V1 ที่ train จบ + อ่าน confusion matrix ของตัวเองออก

---

## ส่วนที่ 4 — Deploy ลง UNO Q (14:45–15:30) ★

1. ใน Edge Impulse → **Deployment** → เลือก target **Arduino UNO Q**
2. Build → download
3. ใน App Lab → import model → เลือก input ให้ตรง (sensor/กล้อง/ไมค์) → Run บนบอร์ด
4. ป้อน input จริง → ดู predicted class + confidence

> 🚦 **Checkpoint 7:** ป้อน input จริงแล้ว model ตอบบนบอร์ดได้
> ถ้าตอบช้ามาก / แกว่ง / ไม่ตรงเลย ถือว่ายังไม่จบ ลองดู confidence + ปริมาณ data

ถ้าอยากให้ตอบเป็น output จริง (Pixels/Buzzer): map `class → output` + ตั้ง threshold (เช่น confidence < 0.75 → ไม่ตัดสิน)

---

## ส่วนที่ 5 — เทส 10 cases (15:30–16:00)

จดลง [`afternoon/predictions.csv`](../team-template/afternoon/predictions.csv):
- 5 เคสปกติ (ทำตามที่ train)
- 5 เคสท้าทาย: ก้ำกึ่งระหว่าง class / เร็วผิดปกติ / คนหรือของที่ไม่ได้เก็บ data / ใกล้เคียงแต่ไม่ใช่

แล้วดู: เคสไหนผิด? เพราะอะไร? (ถ้าเหลือเวลา เก็บ data เพิ่มในจุดที่ผิด → train V2)

> 🚦 **Checkpoint 8:** มี prediction log ≥10 cases ที่มีทั้งถูกและผิด พร้อมเหตุผลที่น่าจะพลาด

---

## ส่วนที่ 6 — ส่งงาน (16:00–16:30)

กรอก fork ให้ครบ (ดู [`team-template/README.md`](../team-template/README.md)) แล้วโชว์ทีมละ 1–2 นาที:
โจทย์ / class / V1 ทำได้แค่ไหน / 1 อย่างที่เรียนรู้

---

## 🆘 ติดตรงไหน

| อาการ | ทำอะไร |
|---|---|
| data ไม่เข้า Studio | เช็ก input ถูกฝั่งไหม (กล้อง/ไมค์ = `edge-impulse-linux`, sensor = brick/forwarder) |
| accuracy ใน Studio สูงแต่ของจริงพัง | data variation ไม่พอ / bias — เก็บเพิ่มหลายเงื่อนไข |
| deploy แล้ว memory error | ลด model size หรือลดจำนวน class |
| inference ช้า/แกว่ง | ลด window, เพิ่ม overlap, เช็ก confidence threshold |
