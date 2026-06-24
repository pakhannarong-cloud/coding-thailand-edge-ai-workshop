# 🌅 Morning Lab — คุม UNO Q ให้อยู่มือ

> จบเช้านี้: บอร์ดเป็นของทีม + ต่อ input ครบ 3 แบบ (sensor / กล้อง / ไมค์)
> ทำเป็นทีม เดินตาม checkpoint อย่ารีบแซง

---

## ส่วนที่ 1 — Reset + First Boot (09:40–10:30)

บอร์ดที่ได้มาเคยมีคนอื่นใช้ รหัส/ชื่อ/Wi-Fi เดิมไม่ใช่ของเรา เราจะ reset ให้เป็นของทีม

### ทำไมต้อง reset
- ไม่รู้รหัสเดิม → ตั้งใหม่ให้รู้
- Wi-Fi เดิมไม่ใช่ของห้องนี้ → ต่อใหม่
- ชื่อบอร์ดซ้ำกับทีมอื่นไม่ได้ → ตั้ง `team-XX-q`

### ขั้นตอน (ผ่าน App Lab — ไม่ต้องใช้ jumper / ไม่ต้อง flash)
> ⚠️ ถ้าเสียบแล้วบอร์ดไม่ boot ให้เช็กก่อนว่า **มี jumper pin เสียบค้างอยู่ไหม** — ถ้ามีให้ถอดออก (pin นั้นทำให้ boot ไม่ขึ้น) ดู [`docs/03-troubleshooting.md`](../docs/03-troubleshooting.md)

1. เสียบ USB-C เข้าบอร์ด + laptop รอ ~30–60 วิ ให้ boot
2. เปิด **Arduino App Lab** รอจนเห็นบอร์ด แล้วคลิกเชื่อม (App Lab login เข้าบอร์ดให้เอง แม้ไม่รู้รหัสเดิม)
3. ไปที่ **Settings** ของบอร์ด แล้วตั้งของทีมเอง 3 อย่าง:
   - **ชื่อบอร์ด** (ไอคอนดินสอข้าง device name) → `team-XX-q`
   - **OS password** → กด *Change password* ตั้งรหัสทีม (จดไว้! Day 2 ต้องใช้ตอน SSH)
   - **Wi-Fi** (เลื่อนลงล่างจะเจอ SSID / PASSWORD) → ตั้งให้ตรงกับ Wi-Fi ที่ laptop ใช้
4. เปิด **Remote access (SSH)** ไว้ เผื่อ Day 2 ต้องเข้า shell

> 🚦 **Checkpoint 1:** App Lab เห็นบอร์ดชื่อ `team-XX-q` + ต่อ Wi-Fi ได้ + รู้รหัสตัวเอง
> ❌ บอร์ดตายสนิท App Lab มองไม่เห็น → เช็ก jumper pin + สาย/พอร์ตก่อน ถ้ายังไม่ได้เรียก TA ขอบอร์ดสำรอง **อย่าพยายาม flash เอง**

---

## ส่วนที่ 2 — Input 1: Modulino Sensor (10:30–11:00)

sensor พวกนี้ต่อผ่าน **Qwiic** อ่านโดย MCU side

1. ต่อสาย Qwiic: `UNO Q → Modulino Movement` (เสียบผิดด้านเสียบไม่เข้า ปลอดภัย)
2. ใน App Lab เปิด example อ่าน sensor (Movement / Accelerometer)
3. กด Run → ขยับ sensor → ดูค่าขยับตาม

> 🚦 **Checkpoint 2:** ขยับ sensor แล้วเห็นตัวเลขขยับจริง

---

## ส่วนที่ 3 — Input 2: USB Webcam (11:00–11:30)

กล้องต่อ **USB อ่านโดย Linux side**

1. เสียบ webcam เข้า **powered USB hub** แล้วต่อ hub เข้าบอร์ด
   - ⚠️ ต้องเป็น hub มีไฟเลี้ยง ไม่งั้นบอร์ดไฟไม่พอ reboot เอง
2. เปิด App Lab example ฝั่งกล้อง (camera preview) แล้ว Run
3. เห็นภาพสดจากกล้อง

ถ้ากล้องไม่ขึ้น เปิด shell บนบอร์ด (ปุ่ม `>_` ใน App Lab) ลอง:
```bash
lsusb            # เห็นชื่อกล้องไหม
ls /dev/video*   # มี /dev/video0 ไหม
```

> 🚦 **Checkpoint 3:** เห็นภาพสดจาก webcam

---

## ส่วนที่ 4 — Input 3: USB Mic (11:30–11:50)

ไมค์ต่อ **USB อ่านโดย Linux side**

1. เสียบ mic เข้า powered hub
2. เช็กบน shell:
```bash
arecord -l       # เห็น card ไมค์ไหม
```
3. ลองอัดสั้น ๆ แล้วเห็น level ขยับ (หรือใช้ example เสียงใน App Lab)

> 🚦 **Checkpoint 4:** พูดแล้วเห็นสัญญาณเสียงขยับ

---

## ส่วนที่ 5 — เชื่อมไปบ่าย (11:50–12:00)

จดลง [`morning/hardware-check.md`](../team-template/morning/hardware-check.md) ของ fork:
- ติ๊ก input ที่ต่อผ่านครบ 3
- แปะรูปอย่างละ 1 (sensor ขึ้นค่า / ภาพกล้อง / level เสียง)

บ่ายแต่ละทีมจะ **เลือก 1 input** ส่งเข้า Edge Impulse ไปเทรน เริ่มคิดได้เลยว่าทีมอยากสอน AI ให้ "มอง / ฟัง / รู้สึก" อะไร

---

## 🧠 เกร็ดสำหรับ TA

- input คนละฝั่ง: Modulino = MCU side, กล้อง/ไมค์ = Linux side ผ่าน USB ตอนบ่ายเชื่อม Edge Impulse ทางเข้าจะต่างกันด้วย (sensor ใช้ผ่าน App Lab/brick, กล้อง+ไมค์ใช้ `edge-impulse-linux` ตรง ๆ ได้)
- ถ้าทีมไหนเร็ว ให้ลองต่อ output (Pixels/Buzzer) เพิ่ม เตรียมไว้ตอนบ่าย map ผลทำนาย → output
