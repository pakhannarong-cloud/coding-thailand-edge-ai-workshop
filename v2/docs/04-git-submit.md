# 🐙 ส่งงานผ่าน Fork — Git 101

> รวบรวมจากหน้างานโดยทีม TA (BUU ENG staff) ปรับให้ตรงกับ template เบาของ v2
> วันแรกใช้ git แค่ "ส่งงาน" พอ ไม่ต้องลึก ทำผ่านเว็บ GitHub ได้ทั้งหมด ไม่ต้อง clone

---

## 1) Fork repo (ทำครั้งเดียวต่อทีม)

1. เข้า repo หลัก แล้วกด **Fork** (มุมขวาบน)
2. ตั้งชื่อ repo (ใช้ชื่อเดิมก็ได้) → **Create fork**
3. **ถ้ากด Fork แล้ว error** = เคย fork ไว้แล้ว → กดโลโก้ GitHub ไปหน้า dashboard → หา repo ที่เคยสร้าง (มักชื่อเดิม) แล้วใช้อันนั้น

> ⚠️ ก่อนแก้ทุกครั้ง เช็กว่าอยู่ใน **repo ของทีมเอง** ไม่ใช่ repo หลัก ไม่งั้น commit ผิดที่

---

## 2) แก้ + commit ผ่านเว็บ

1. เปิดไฟล์ที่จะกรอก (เช่น `afternoon/model.md`)
2. กด **ไอคอนดินสอ** (Edit)
3. กรอกเนื้อหา
4. กด **Commit changes**
5. ใส่ commit message สั้นๆ (เช่น `submit model.md`) + ใส่ชื่อทีม/สมาชิกใน description → **Propose changes**

> ถ้าแก้บน repo หลัก GitHub จะสร้าง branch ใน fork ของทีมให้เอง แล้วเปิดเป็น Pull Request — อันนี้โอเค ใช้ส่งงานได้

---

## 3) เช็กว่าส่งแล้วจริง

1. กดชื่อ repo ของทีม → ไปแท็บ **Commits**
2. เห็น commit ของทีมโผล่ = อัปเดตแล้ว

---

## สิ่งที่ต้องส่งให้ครบ (ดู [TEAM-README](../team-template/README.md))

- [ ] `morning/hardware-check.md` — input 3 ตัว + รูป
- [ ] `afternoon/model.md` — EI link + accuracy + confusion matrix
- [ ] `afternoon/predictions.csv` — ≥10 cases
- [ ] รูป/คลิป model รันบนบอร์ด ใน `assets/`
- [ ] ตอบสั้น 3 ข้อใน README

> วันแรกพอแค่นี้ Day 2 ค่อยลง git ลึกขึ้น (branch, PR review) ตอนปล่อยให้ทำเอง
