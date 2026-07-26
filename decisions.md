# Decision Log

## 2026-07-22
- ใช้ GitHub Private Repository เป็นที่เก็บ Company Brain
- ให้ AI ทุกตัวใช้ข้อมูลจากแหล่งกลางเดียวกัน
- เริ่มสร้างทีม AI: CFO, Secretary และ Agent เฉพาะทาง
- ใช้ Daily Work เป็นข้อมูลต้นทาง
- การเทรดทองเปลี่ยนเป็นรอ Setup ชัดเจนก่อนเข้า

## 2026-07-26
- Pending confirmation: Use Telegram as a communication channel with the Infinity Power Executive Secretary for CEO/MD messages, daily-update follow-ups, and concrete assignment intake.
- Operational note: Telegram bot access was verified and a confirmation message was sent to the single private chat target visible from bot updates.
- Control required: CEO/MD must confirm that this private Telegram chat is the approved target before relying on it for routine follow-ups.
- Confirmed: CEO/MD replied "Confirm" through Telegram, approving this chat as the secretary communication target.
- Company direction from Telegram daily summary: priority is finding customers and generating revenue; do not build a large AI Company system yet; executives will respond to inbound customers directly; AI does not own Sales yet; Sales Manager starts when customers come in; Company Brain remains the main company information source.
- Telegram resource decision: the secretary should not run a continuous token-heavy Telegram waiting loop by default. Use heartbeat/on-demand/scheduled processing or a lightweight engineering-approved monitor, then acknowledge only after real updates are processed.
