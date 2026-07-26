# Company Routine

## Daily
- บันทึกงานสำเร็จ ปัญหา การตัดสินใจ และงานค้าง
- เลือก 3 งานสำคัญของวันถัดไป

## Weekly
- สรุปความคืบหน้าโครงการ
- ตรวจงานค้าง โอกาสขาย และการเงิน

## Monthly
- สรุปผลประกอบการ
- ตรวจเป้าหมายบริษัทและประสิทธิภาพ Agent

## Telegram Intake
- เมื่อ CEO/MD ส่งบันทึก ความคิด หรือสิ่งที่ต้องทำผ่าน Telegram ให้เลขาแยกประเภทข้อมูลก่อนบันทึก
- ข้อมูลทรัพย์สินหรือประวัติซ่อมบำรุง ให้บันทึกในไฟล์ asset ที่เกี่ยวข้อง
- คำสั่งที่เป็นงานชัดเจน ให้สร้าง Paperclip task ทันที และตอบกลับด้วยชื่อ Task, Task ID, Assignee, Priority และ Status
- หลังบันทึก Company Brain สำเร็จ ให้ตอบกลับ Telegram ว่าบันทึกสำเร็จ พร้อม Commit ID และสถานะ GitHub Sync
- หากข้อมูลซ้ำกับข้อความก่อนหน้า ให้ deduplicate และตอบกลับว่ารวมเป็นรายการเดียวแล้ว

## Telegram Permanent Response Loop
- Effective 2026-07-26, the secretary must check the approved Telegram bot inbox on every assigned heartbeat before generic Company Brain maintenance.
- Use the approved runtime Telegram configuration only; do not store bot tokens, chat IDs, or secret values in the Company Brain.
- If Telegram webhook delivery is not configured, use `getUpdates` polling, process every pending update, and advance the offset only after updates are categorized, acted on, and acknowledged.
- If the message is a concrete CEO/MD assignment, create the Paperclip task first, then reply in Telegram with Task title, Task ID, Assignee, Priority, and Status.
- If the message updates Company Brain data, append dated notes to the relevant files, commit the change, push to GitHub, and reply in Telegram with the commit ID and GitHub sync result.
- If the message is only a greeting or status check, reply with a concise secretary availability/status acknowledgement.
- If required credentials, approved chat target, Paperclip task creation, Telegram delivery, or GitHub push fails, escalate the exact failure to CEO/MD and record the blocker in the issue.

## Telegram Resource Control Update - 2026-07-26
- CEO/MD clarified that the secretary does not need to wait for Telegram replies continuously if doing so wastes tokens or runtime resources.
- Default mode: process Telegram only during assigned heartbeats, explicit Paperclip wakes, scheduled checks, or a lightweight monitor approved by engineering.
- Do not run an always-on high-frequency polling loop unless CEO/MD explicitly approves the resource cost.
- Acknowledge Telegram after actual processing is completed; do not send repeated idle/status pings just to prove the secretary is online.
- INF-198 remains the engineering path for durable chat-target configuration; its implementation should prefer webhook or low-frequency monitored polling over token-heavy continuous polling.
