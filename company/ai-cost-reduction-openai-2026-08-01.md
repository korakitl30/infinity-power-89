# AI Cost Reduction: OpenAI Migration

## 2026-08-01 Update

Source assignment: INF-521 / Telegram request from CEO/MD: "เปิด task ให้ย้าย ai มาใช้ openai ราคาถูกลง 80%" ("Open a task to move AI to OpenAI and make the price 80% cheaper").

### Decision / Direction

- Move company AI usage toward OpenAI where it can reduce cost while preserving acceptable quality.
- Target reduction: 80% versus current AI spend baseline.
- Do not assume the target is achieved until current provider/model usage and monthly token volume are audited.
- Use OpenAI model selection by workload: optimize accuracy first, then move each workload to the cheapest model that still meets the required quality.
- Use lower-cost OpenAI operating modes for non-urgent work: Batch API, Flex processing, prompt caching, shorter prompts, fewer requests, and smaller models.

### Current OpenAI Cost Assumptions Checked On 2026-08-01

- OpenAI pricing is per 1M tokens and varies by model, context length, cached input, and service tier.
- OpenAI pricing page lists `gpt-5.6-luna` materially cheaper than `gpt-5.6-terra` and `gpt-5.6-sol`; this makes `gpt-5.6-luna` the first candidate for routine secretary summaries, categorization, extraction, and other low-risk drafting.
- OpenAI cost optimization guidance recommends reducing requests, minimizing tokens, selecting smaller models, and using Batch API/Flex processing for lower-priority async work.
- Batch API can reduce eligible asynchronous request cost by 50% compared with synchronous API use and has a 24-hour turnaround target.
- Prompt caching should be used for repeated long prefixes such as Company Brain instructions, agent role prompts, schemas, and stable business context; cache hit/write metrics must be logged to prove savings.

Official references checked:
- https://developers.openai.com/api/docs/pricing
- https://developers.openai.com/api/docs/guides/model-selection
- https://developers.openai.com/api/docs/guides/cost-optimization
- https://developers.openai.com/api/docs/guides/batch
- https://developers.openai.com/api/docs/guides/flex-processing
- https://developers.openai.com/api/docs/guides/prompt-caching

### Migration Plan

1. Audit current AI usage.
   - Identify every active AI provider, API key, model, endpoint, scheduled agent, and automation.
   - Export last 30 days of spend, request counts, token counts, and use cases.
   - Tag each workload as realtime, near-realtime, async, or manual.

2. Define model routing.
   - Routine extraction/summarization/classification: trial `gpt-5.6-luna` first.
   - Higher-stakes business reasoning, strategy, or final customer-facing drafts: benchmark `gpt-5.6-terra` or stronger model only where quality requires it.
   - Long repeated Company Brain prompts: structure static context first and enable prompt caching.
   - Offline/backlog work: route to Batch API or Flex processing where response time is not critical.

3. Build migration controls.
   - Centralize model/provider configuration in one place.
   - Add per-workload token and cost logging.
   - Add monthly budget alerts and a hard spend review threshold.
   - Keep rollback path to current provider until quality and savings are verified.

4. Verify 80% reduction.
   - Compare 7-day OpenAI pilot cost against normalized prior-provider baseline.
   - Measure quality on representative secretary, sales, operations, and CFO tasks.
   - Mark migration complete only if cost reduction is at least 80% without unacceptable quality loss.

### Risks / Unknowns

- Current AI provider, exact models, and monthly baseline cost are not yet documented in the Company Brain.
- A pure provider swap may not reach 80%; savings likely require model routing, prompt compression, caching, and async processing.
- Some CEO/MD-facing work may need a stronger model than the cheapest option.

### Follow-Up Tasks Suggested

- Create an engineering audit task for current AI provider/model usage and 30-day cost baseline.
- Create an implementation task to centralize OpenAI model routing, caching, and spend logging.
- Create a verification task for a 7-day cost/quality pilot before declaring the 80% reduction complete.
