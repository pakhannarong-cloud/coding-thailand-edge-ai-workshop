# 💻 Arduino App Lab — ติดตั้ง + ตั้งค่าบอร์ด

> รวบรวมจากหน้างานโดยทีม TA (BUU ENG staff) ปรับเป็นไฟล์ถาวรใน v2

---

## 1. ติดตั้ง App Lab (ทำก่อนวันงาน)

1. โหลดจาก https://www.arduino.cc/en/software/#app-lab-section (เลือก OS ให้ตรง)
2. ติดตั้งตามปกติ
3. เปิดโปรแกรม → ขึ้นหน้า **Welcome to Arduino App Lab** → เสียบบอร์ดได้เลย
   - ยังไม่เสียบ = "No boards found"
   - เสียบแล้ว = ขึ้นการ์ดบอร์ดให้กดเชื่อม

---

## 2. ตั้งค่าบอร์ดให้เป็นของทีม (เช้า)

บอร์ดวนมาจากที่อื่น รหัส/ชื่อ/Wi-Fi เดิมไม่ใช่ของเรา **ไม่ต้อง reflash** — เข้า App Lab → **Settings** แล้วตั้ง 3 อย่าง:

| ตั้งอะไร | ที่ Settings |
|---|---|
| ชื่อบอร์ด | ไอคอนดินสอข้าง device name → `team-XX-q` |
| รหัส (OS password) | **Change password** → ตั้งรหัสทีม + จดไว้ |
| Wi-Fi | เลื่อนลงเจอ **SSID / PASSWORD** → ตั้งให้ตรงกับ Wi-Fi ที่ laptop ใช้ |

หน้า Settings ยังบอก: App Lab version, FQBN (`arduino:zephyr:unoq`), Serial number, Disk storage, **Remote access (SSH)** (เปิดไว้เผื่อ Day 2)

> 💡 App Lab login เข้าบอร์ดให้อัตโนมัติ แม้ไม่รู้รหัสเดิม — เพราะงั้นรหัสที่คนรอบก่อนตั้งไว้ "ไม่บล็อก" การทำ workshop เราแค่ตั้งรหัสใหม่ทับให้รู้

---

## 3. การเชื่อมบอร์ด: USB vs Wi-Fi

- **ตอน setup ครั้งแรก:** ต่อ USB-C เข้า laptop โดยตรง (เสถียรสุด)
- **ตอนใช้กล้อง/ไมค์:** ให้บอร์ดอยู่บน **Wi-Fi** แล้ว peripheral เสียบ hub — **อย่าต่อบอร์ดเข้าคอมพร้อมใช้กล้อง** (ดูเหตุผลใน [troubleshooting](03-troubleshooting.md))
- เงื่อนไขสำคัญ: บอร์ดกับ laptop ต้องอยู่ **Wi-Fi ตัวเดียวกัน** ไม่งั้น App Lab หาบอร์ดไม่เจอ

---

## 4. เปิด bash shell บนบอร์ด

ใน App Lab มีปุ่ม **`>_`** (มุมล่าง) เปิด shell บนบอร์ดได้ตรง ใช้ตอนเช็ก/ติดตั้งฝั่ง Linux เช่น `ls /dev/video*`, `arecord -l`, หรือรัน `edge-impulse-linux`
