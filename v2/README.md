# Edge AI Workshop — v2 (Day 1 focus)

ปรับจาก v1 ให้ **ง่ายขึ้น เน้นวันแรก เดินพร้อมกันทั้งห้อง** Day 2 ปล่อยให้ทำเอง

## อะไรเปลี่ยนจาก v1
- **เช้า = คุม UNO Q + ต่อ input ครบ 3** (reset, sensor, กล้อง, ไมค์) แทนแตก 4 track ตั้งแต่เช้า
- **บ่าย = Edge Impulse ทั้ง pipeline** (connect → train → deploy → test) เลือก 1 input
- **ตัด git/PR/worksheet 4 ใบ** ออกจากวันแรก เหลือ fork แบบกรอกช่อง เน้นส่งงาน + ตรวจง่าย
- **แก้ workflow ingest ให้ตรงต่อ input** (กล้อง/ไมค์ = edge-impulse-linux, sensor = brick/forwarder)
- **ดึงความรู้หน้างานจากเล่ม TA** เข้ามาเป็นไฟล์ถาวร (App Lab setup / troubleshooting / git submit)

## ไฟล์ในชุดนี้
```
docs/00-facilitator-prep.md   ← ทีมจัดอ่านก่อนงาน (reset 2 ระดับ, Wi-Fi, pre-flight)
docs/01-schedule.md           ← timeline เช้า/บ่าย
docs/02-app-lab-setup.md      ← ติดตั้ง App Lab + ตั้งค่าบอร์ด (จากเล่ม TA)
docs/03-troubleshooting.md    ← เคสจริงหน้างาน (jumper pin, กล้อง/ไมค์, edge-impulse-linux)
docs/04-git-submit.md         ← fork + commit ส่งงาน (จากเล่ม TA)
labs/morning-uno-q.md         ← lab เช้า: reset + 3 input
labs/afternoon-edge-impulse.md← lab บ่าย: train + deploy + test
slides/day1-v2-outline.md     ← สไลด์เช้า/บ่าย (outline ต่อสไลด์)
team-template/                ← fork ส่งงาน (เบาลง)
  README.md · morning/hardware-check.md · afternoon/model.md · afternoon/predictions.csv
```

## เครดิต
ส่วน App Lab / troubleshooting / git submit รวบรวมจากหน้างานโดยทีม TA (BUU ENG staff)

## ยังต้องตัดสิน/ทำต่อ
- [ ] verify บนบอร์ดจริง: App Lab Settings → Change password เปลี่ยนได้โดยไม่ต้องรู้รหัสเก่าไหม
- [ ] ยืนยันชื่อ option model size บนจอจริงวันนั้น
- [ ] แปลง slides outline → PPTX (Sarabun) หรือดันเข้า Canva — บอกได้
- [ ] (ออปชัน) สคริปต์ audit 20 fork ผ่าน GitHub API
