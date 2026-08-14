# Company Routine

⚠️ **DEPRECATED SECTIONS (2026-08-14)**: Sections marked with ❌ refer to Telegram operations, which have been disabled effective 2026-08-14 (INF-877, INF-879). See `decisions.md` for the new operating model. These sections are preserved for historical audit only.

## Daily
- บันทึกงานสำเร็จ ปัญหา การตัดสินใจ และงานค้าง
- เลือก 3 งานสำคัญของวันถัดไป

## Weekly
- สรุปความคืบหน้าโครงการ
- ตรวจงานค้าง โอกาสขาย และการเงิน

## Monthly
- สรุปผลประกอบการ
- ตรวจเป้าหมายบริษัทและประสิทธิภาพ Agent

## ❌ Telegram Intake (DEPRECATED — 2026-08-14)

**Do not execute.** This section documents the superseded Telegram intake workflow.

Previously, when MD sent updates through Telegram:
- เมื่อ MD ส่งบันทึก ความคิด หรือสิ่งที่ต้องทำผ่าน Telegram ให้เลขาแยกประเภทข้อมูลก่อนบันทึก
- ข้อมูลทรัพย์สินหรือประวัติซ่อมบำรุง ให้บันทึกในไฟล์ asset ที่เกี่ยวข้อง
- คำสั่งที่เป็นงานชัดเจน ให้สร้าง Paperclip task ทันที และตอบกลับด้วยชื่อ Task, Task ID, Assignee, Priority และ Status
- หลังบันทึก Company Brain สำเร็จ ให้ตอบกลับ Telegram ว่าบันทึกสำเร็จ พร้อม Commit ID และสถานะ GitHub Sync
- หากข้อมูลซ้ำกับข้อความก่อนหน้า ให้ deduplicate และตอบกลับว่ารวมเป็นรายการเดียวแล้ว

**Superseded by**: Paperclip issue-based workflow and CEO coordination model (2026-08-14).

## ❌ Telegram Permanent Response Loop (DEPRECATED — 2026-08-14)

**Do not execute.** This section documents the superseded Telegram polling workflow.

Previously, effective 2026-07-26, the secretary checked Telegram on every assigned heartbeat:
- Use the approved runtime Telegram configuration; do not store bot tokens, chat IDs, or secret values in the Company Brain
- If Telegram webhook delivery not configured, use `getUpdates` polling, process every update, advance offset only after categorization/action/acknowledgement
- Concrete MD assignment → create Paperclip task → reply in Telegram with Task title, ID, Assignee, Priority, Status
- Company Brain update message → append dated notes → commit → push → reply in Telegram with commit ID and GitHub sync result
- Greeting or status check → reply with secretary availability/status acknowledgement
- If any required step fails → escalate exact failure to MD and record blocker in issue

**Superseded by**: Paperclip issue-based workflow and CEO coordination model (2026-08-14).

## ❌ Telegram Resource Control Update - 2026-07-26 (DEPRECATED — 2026-08-14)

**Do not execute.** This section documents optimization rules for the now-disabled Telegram polling.

Previously, MD clarified resource constraints for Telegram operations:
- Secretary should not wait for Telegram replies continuously if it wastes tokens or runtime resources
- Default mode: process Telegram only during assigned heartbeats, explicit Paperclip wakes, scheduled checks, or lightweight engineering-approved monitor
- Never run always-on high-frequency polling unless MD explicitly approved resource cost
- Acknowledge Telegram only after actual processing completed; no repeated idle/status pings
- INF-198 owned engineering path for durable chat-target configuration, preferring webhook or low-frequency monitored polling

**Superseded by**: Telegram is now disabled entirely; this resource optimization is no longer relevant (2026-08-14).

## ❌ Telegram Scheduled Cadence - 2026-07-26 (DEPRECATED — 2026-08-14)

**Do not execute.** This section documents the now-canceled scheduled Telegram routines.

Previously, MD approved resource-saving Telegram cadence:
- Check and process Telegram intake every 4 hours
- Every morning, send MD a concise reminder of tasks needing follow-up
- Morning reminders include open tasks, pending MD confirmations, items marked Follow-up or Pending in Company Brain
- No idle acknowledgements between scheduled checks unless new processed update, blocker, or explicit MD request
- INF-199 owned scheduler/monitor setup for 4-hour intake cadence and morning follow-up reminders

**Superseded by**: Telegram routines are now canceled entirely; CEO coordination replaces scheduled reminders (2026-08-14).

## Follow-Up File Maintenance - 2026-07-26 (Updated 2026-08-14)
- `company/follow_up.md` is the canonical follow-up list for MD and CEO queries.
- **Updated (2026-08-14)**: Previously updated during Telegram 4-hour intake; now updated during Paperclip issue triage and CEO coordination.
- Maintenance rules:
  - New assignment → add task to the appropriate priority section (🔴/🟡/🟢).
  - Completed item → move it to ✅ Completed with the completion date.
  - Priority change → move task to the new section.
  - Never duplicate a task; if it already exists, update status in place.
- Keep task wording short (e.g., "Change Volvo engine oil", "Send Proposal Office 15").
- Update `Last Updated` timestamp on every write.
- Commit and push `company/follow_up.md` together with any other Company Brain changes.
- **Note (2026-08-14)**: Follow-up list is no longer directly sourced from Telegram intake; it is maintained through Paperclip issue review and CEO coordination of business outcomes.

## ❌ Telegram Scheduled Routine Implementation - 2026-07-26 (DEPRECATED — 2026-08-14)

**Do not execute.** These Telegram routines have been canceled.

Previously, INF-201 created two active Paperclip routines:
- `Secretary Telegram 4-hour intake` — assigned to Infinity Power Executive Secretary, high priority, schedule trigger `0 */4 * * *` in `Etc/UTC`
- `Secretary morning follow-up reminder` — assigned to Infinity Power Executive Secretary, high priority, schedule trigger `0 9 * * *` in `Asia/Bangkok`
- Both used `coalesce_if_active` concurrency and `skip_missed` catch-up behavior
- Routine descriptions included credential-resolution, Telegram acknowledgement, Paperclip task creation, Company Brain append/commit/push, offset update, and fallback-comment requirements

**Superseded by**: CEO coordination model; these routines should be canceled in Paperclip (2026-08-14).

## Direct Calendar Reminders - 2026-07-26 (Updated 2026-08-14)
- Direct MD Calendar event creation was previously blocked pending OAuth/delegated-access setup.
- INF-210 confirmed the secretary runtime needs Calendar event creation connector and approved Calendar API OAuth path.
- INF-224 is the unblock path: Paperclip admin/engineering must provide Calendar-capable access and MD must authorize the correct calendar.
- **Updated (2026-08-14)**: Telegram reminders are no longer a fallback; **Telegram is disabled.** Calendar event creation and Paperclip issue tracking are the primary notification channels.
- If Calendar API access is available: create direct MD Calendar events for reminders and follow-ups.
- If Calendar API access is unavailable: use Paperclip issues and CEO coordination for all follow-ups and reminders.
