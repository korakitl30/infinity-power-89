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
- Telegram cadence decision: check and process Telegram intake every 4 hours, and send CEO/MD a morning reminder of tasks that need follow-up.

## 2026-07-29
- CEO review decision for INF-422: the updated old daily log was rechecked. The Executive Secretary is authorized to create new Paperclip tasks directly when CEO/MD messages contain concrete assignments or clear follow-up work.
- Control note: the secretary should keep using the existing task-creation rules: create a task immediately for concrete assignments, record the task ID/status in the issue or Telegram reply, and escalate ambiguous business decisions to CEO/MD instead of guessing.

## 2026-08-01
- CEO/MD direction from Telegram assignment INF-521: move company AI usage toward OpenAI with an 80% cost-reduction target.
- Execution control: do not declare the 80% reduction complete until current AI provider/model usage and monthly baseline cost are audited, OpenAI routing is piloted, and cost/quality metrics are compared.
- Cost strategy recorded in `company/ai-cost-reduction-openai-2026-08-01.md`: use cheaper OpenAI models for routine work, prompt caching for repeated Company Brain context, and Batch API/Flex processing for eligible asynchronous workloads.
