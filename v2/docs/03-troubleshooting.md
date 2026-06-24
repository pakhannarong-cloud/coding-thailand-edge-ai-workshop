# 🆘 Troubleshooting — ของจริงจากหน้างาน

> รวบรวมจากหน้างานโดยทีม TA (BUU ENG staff) — เคสที่เจอจริงในรอบที่แล้ว เปิดไฟล์นี้ก่อนเรียกคน

---

## 1) ต่อแล้วบอร์ดไม่ขึ้น / ไม่ boot

เช็กตามนี้:
- เสียบสายถูกไหม / สายเสียไหม
- ต่อ Wi-Fi ได้ไหม (ถ้าได้ ใช้ผ่าน Wi-Fi เลยสะดวกกว่า)
- ⭐ **มี jumper pin เสียบค้างอยู่ไหม** — pin ที่ใช้เข้าโหมด flash ถ้าลืมถอด **บอร์ดจะ boot ไม่ขึ้น** ถอดออกก่อนเลย (นี่คือสาเหตุ "บอร์ดตาย" ที่เจอบ่อยสุด)

---

## 2) ต่อกล้อง/ไมค์ไม่ขึ้น หรือบอร์ดไม่เชื่อมสักที (รอนานมาก)

หลักการ: ตอนใช้กล้อง/ไมค์ ให้ **บอร์ดอยู่บน Wi-Fi** + กล้อง/ไมค์เสียบ **powered USB hub**
- ⚠️ **อย่าต่อบอร์ดเข้าคอมโดยตรงพร้อมใช้กล้อง** — มันจะหากล้องไม่เจอ
- เปิด App Lab → หาบอร์ดผ่าน Wi-Fi

**ถ้าหาบอร์ดไม่เจอ** → เดาได้เลยว่าบอร์ดกับคอมอยู่คนละ Wi-Fi วิธีแก้:
1. ต่อบอร์ดเข้าคอมตรงๆ ก่อน → เปิด App Lab → **Settings**
2. เลื่อนลงหา **SSID / PASSWORD** → ตั้ง Wi-Fi ให้ตรงกับที่คอมใช้
3. ถอด USB แล้วกลับไปต่อตามรูป (Wi-Fi + hub) เข้าบอร์ดผ่าน Wi-Fi อีกครั้ง

---

## 3) มีปัญหาเรื่อง edge-impulse-linux

ติดตั้งผ่าน bash shell บนบอร์ด (ปุ่ม `>_`):

```bash
nano run.sh
```
วางสคริปต์นี้:
```bash
curl -sL https://deb.nodesource.com/setup_20.x | sudo bash -
sudo apt install -y gcc g++ make build-essential nodejs sox \
  gstreamer1.0-tools gstreamer1.0-plugins-good \
  gstreamer1.0-plugins-base gstreamer1.0-plugins-base-apps
sudo npm install edge-impulse-linux -g --unsafe-perm
ls /dev/video*
arecord -l
```
`ctrl + x` → `y` → `enter` แล้วรัน:
```bash
bash run.sh
```
เสร็จแล้วเรียก:
```bash
edge-impulse-linux
```
จะให้ login → เอา email/password จากหน้า Edge Impulse → **account settings** มากรอก

> 💡 ถ้าทีมจัด pre-install สคริปต์นี้ลงบอร์ดทุกตัวก่อนวันงาน จะข้ามขั้นนี้ได้ ลด Wi-Fi คอขวด

---

## ✨ Magic Trick (ทำก่อนเรียกคน)

1. ทำตาม troubleshooting ข้างบนครบหรือยัง? ถ้าครบแล้วยังไม่ได้ → ข้อ 2
2. **ถอดปลั๊กเสียบใหม่** แล้วดูผล

ถ้ายังไม่ได้จริงๆ → เรียก TA/พี่เลี้ยงมาดู (พร้อมบอกว่าค้าง step ไหน ลองอะไรไปแล้ว)
