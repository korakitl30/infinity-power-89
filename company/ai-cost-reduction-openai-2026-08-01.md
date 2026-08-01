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

---

## INF-523 Audit Results — 2026-08-01

Completed by: Founding Engineer (agent 28f86427). Source: live DB query from `cost_events`, `agents`, `routines`, `company_secrets`, `agent_config_revisions`. Data covers 2026-07-22 (instance creation) to 2026-08-01.

### AI Provider Inventory

| Provider | Adapter | Connection Method | API Key Location | Billing Type |
|----------|---------|------------------|-----------------|--------------|
| **OpenAI** | `codex_local` | ChatGPT account OAuth | No API key in vault — uses ChatGPT account connection | Subscription-included |
| **Anthropic Claude** | `claude_local` | Paperclip platform subscription | No API key in vault — injected by Paperclip harness | Subscription-included |

**No direct API keys for OpenAI or Anthropic are stored in the company secrets vault.** Both providers are accessed through Paperclip's platform connection layer.

### Agent Provider Mapping

| Agent | Adapter | Model | Status |
|-------|---------|-------|--------|
| Infinity Power Executive Secretary | `codex_local` / OpenAI | Platform default (ChatGPT) | Active |
| CEO | `codex_local` / OpenAI | Platform default — error: `gpt-5.3-codex-spark` not supported | Error |
| Founding Engineer - Sales Systems & Automation | `claude_local` / Anthropic | `claude-sonnet-4-6` | Active |
| Marketing Team Lead - Website & Design | `codex_local` / OpenAI | Platform default | Idle |
| Website Builder - Lead Generation Site | `codex_local` / OpenAI | Platform default | Idle |
| Visual Designer - Social and Website Assets | `codex_local` / OpenAI | Platform default | Idle |
| Video Material Producer - Sales Content | `codex_local` / OpenAI | Platform default | Idle |
| Account and Finance Manager | `codex_local` / OpenAI | Platform default | Paused |

Note: No agent has a model explicitly configured in `adapter_config`. All `codex_local` agents use the platform-default ChatGPT model. The CEO agent is in error state because `gpt-5.3-codex-spark` is not available on the connected ChatGPT account tier.

### 30-Day Token Volume (2026-07-22 to 2026-08-01)

#### OpenAI (`codex_local`)
| Metric | Value |
|--------|-------|
| Total requests | 816 |
| Total input tokens | 324,105,843 (~324M) |
| Total output tokens | 3,601,072 (~3.6M) |
| Cached input tokens | 293,837,440 (~294M) |
| Cache hit rate | **90.7%** |
| Net uncached input | ~30.3M tokens |
| Direct cost billed | $0 (subscription-included) |

#### Anthropic Claude (`claude_local`)
| Metric | Value |
|--------|-------|
| Total requests | 186 |
| Total input tokens | 17,749 (net — almost all context is cached) |
| Total output tokens | 1,157,545 (~1.16M) |
| Cached input tokens | 159,298,995 (~159M) |
| Models used | `claude-sonnet-4-6` (primary), `claude-sonnet-4-5` (older) |
| Direct cost billed | $0 (subscription-included) |

### By-Workload Breakdown

| Workload | Agent | Provider | Category | Requests | Input Tokens | Output Tokens |
|----------|-------|----------|----------|----------|--------------|---------------|
| Telegram 4h intake + morning brief | Secretary | OpenAI | **near-realtime / async** | 710 | 219.2M | 2.78M |
| CEO strategic reasoning | CEO | OpenAI | **async** | 70 | 72.5M | 453K |
| Sales systems engineering | Founding Eng | OpenAI | **async** | 21 | 11.6M | 154K |
| Sales systems engineering | Founding Eng | Anthropic | **async** | 10 | <1K net | 234K |
| Website development | Website Builder | OpenAI + Anthropic | **async** | 10 | ~8M | 169K |
| Visual design assets | Visual Designer | OpenAI | **async** | 5 | 6.7M | 82K |
| Marketing coordination | Marketing Lead | OpenAI + Anthropic | **async** | 7 | 4.2M | 106K |
| Financial review | Finance Mgr | OpenAI | **async** | 2 | 967K | 21K |
| Video production scripting | Video Producer | OpenAI | **async** | 1 | 1.25M | 13K |

**No realtime workloads identified.** All current work is either scheduled-async or issue-triggered async.

### Active Scheduled Automations

| Routine | Cron | Timezone | Provider | Runs (30d) | Status |
|---------|------|----------|----------|-----------|--------|
| Secretary Telegram 4-hour intake | `0 */4 * * *` | UTC | OpenAI | 34 | **Active** |
| Secretary morning follow-up reminder | `0 9 * * *` | Asia/Bangkok | OpenAI | 6 | **Active** |
| Daily Sriracha market watch | `0 9 * * *` | Asia/Bangkok | OpenAI | 1 | Archived |
| XAU/USD threshold monitor | `*/5 * * * *` | UTC | OpenAI | 1 | Archived |

### Company Secrets Inventory (No Values Exposed)

| Secret Key | Name | Bound To | Purpose |
|-----------|------|----------|---------|
| `telegram_bot_token` | TELEGRAM_BOT_TOKEN | Secretary, CEO | Telegram bot send |
| `telegram_chat_id` | TELEGRAM_CHAT_ID | Secretary | Telegram MD chat target |
| `settings-secrets-github_access_token` | GITHUB_ACCESS_TOKEN | Secretary, CEO | GitHub company brain push |
| `github_repo_url` | GITHUB_REPO_URL | Secretary, CEO | Company brain repo URL |

### Agent API Keys

| Key Name | Agent | Created | Last Used |
|----------|-------|---------|-----------|
| `secretary-runtime-2026-07-26` | Secretary | 2026-07-26 | Never (unused) |

### Estimated Market-Rate API Cost Equivalent

Since all costs are subscription-included, the baseline is $0 direct per-token billing. Estimated cost if billed at market API rates:

**OpenAI at GPT-4o-mini equivalent rates** (~$0.15/1M input, $0.60/1M output, $0.075/1M cache read):
- Non-cached input: 30.3M × $0.15/1M = **$4.55**
- Cache reads: 293.8M × $0.075/1M = **$22.04**
- Output: 3.6M × $0.60/1M = **$2.16**
- **Subtotal OpenAI: ~$29/month equivalent**

**Anthropic at claude-sonnet-4-6 rates** (~$3/1M input, $15/1M output, $0.30/1M cache read):
- Non-cached input: 17.7K × $3/1M = **$0.05**
- Cache reads: 159.3M × $0.30/1M = **$47.79**
- Output: 1.16M × $15/1M = **$17.36**
- **Subtotal Anthropic: ~$65/month equivalent**

**Total estimated market equivalent: ~$94/month**

### Key Finding: Current Billing Model

The company is NOT paying per token today. Both providers are billed as `subscription_included`. The actual cash cost is the Paperclip platform subscription plus the ChatGPT subscription used for codex_local agents. The 80% reduction goal needs clarification on whether it targets:
1. Paperclip subscription tier change (by eliminating Claude agents), or
2. Future direct API costs when migrating off Paperclip's bundled AI access.

### Migration Recommendations

#### Workloads eligible for `gpt-5.6-luna` (cheapest OpenAI model):
- Secretary Telegram intake (extraction, categorization, task creation) — **async, low-risk**
- Secretary morning brief (summarization) — **async, low-risk**
- Visual Designer (creative briefs, layout descriptions) — **async, low-risk**
- Video Producer (script outlines) — **async, low-risk**
- Finance Manager financial summaries — **async, low-risk**

#### Workloads eligible for Batch API (50% cost reduction vs synchronous):
- Secretary 4-hour intake — response window is hours, not seconds
- Secretary morning brief — 1× daily, no latency requirement
- Website Builder coding tasks — multi-step, hours acceptable

#### Workloads eligible for Flex processing (lowest cost, up to 12h turnaround):
- Marketing analysis and coordination
- Visual design brief generation
- Any overnight background tasks

#### Workloads requiring stronger model (`gpt-5.6-terra` or equivalent):
- CEO strategic reasoning and final business decisions
- Customer-facing proposal drafting
- Complex multi-step engineering tasks (Founding Engineer)

#### Realtime workloads:
- None identified. All current automations are scheduled or async.

#### Migration priority:
1. **Founding Engineer** (claude_local → OpenAI): 1 agent switch, enables elimination of Anthropic dependency
2. **Secretary routines**: Switch to `gpt-5.6-luna` + Batch API; already has 90.7% cache — maintain caching
3. **CEO**: Keep on capable model until error state is resolved (model compatibility issue with ChatGPT account)
4. **Add OPENAI_API_KEY to secrets vault** when moving from ChatGPT account to direct API billing
5. **Add per-workload cost logging** before and after migration to prove 80% reduction

---

## 2026-08-01 Secretary Follow-Up Update

Secretary audit heartbeat at 2026-08-01T03:51Z:

- Verified the OpenAI cost-control assumptions against official OpenAI documentation on 2026-08-01. Pricing still lists `gpt-5.6-luna` materially cheaper than `gpt-5.6-terra` and `gpt-5.6-sol`; cost optimization docs still point to fewer requests, fewer tokens, Batch API, Flex processing, and prompt caching as cost levers.
- Local secretary workspace scan found no additional production provider/model configuration beyond the INF-523 audit results above. Local Codex configuration inspected for this company only showed trusted project roots; model cache files appear to be provider/model catalog metadata, not actual company usage or billing records.
- The secretary runtime could not independently query the Paperclip company secrets endpoint because the endpoint returned authorization denial. Use the INF-523 audit owner results as the current source for secrets inventory.
- Current status: the 80% reduction target remains unproven as a cash-savings claim because current direct token billing is recorded as subscription-included. Do not approve migration completion until the target is clarified and INF-525 completes the cost/quality pilot.
- Named unblock owner/action: CEO/MD must clarify whether the 80% reduction target means reducing Paperclip/ChatGPT subscription spend, eliminating Anthropic dependency, or reducing future direct API billing; migration implementation owner (`28f86427-9313-4fa6-bd43-a3dfa9fc1ed5`) must complete routing/logging and pilot comparison.
