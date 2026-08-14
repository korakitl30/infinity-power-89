# New Operating Model — CEO Coordination (2026-08-14)

**Effective Date**: 2026-08-14 (INF-877, INF-879)

**Previous Model (DEPRECATED)**: MD → Telegram → Secretary → Paperclip Task/Company Brain

**New Model (ACTIVE)**: MD → CEO → Responsible Agent → Actual External Outcome → Verification → CEO → MD

---

## Principles

### 1. Telegram is Disabled
- **No Telegram polling** — The Secretary does not check or process Telegram messages.
- **No Telegram acknowledgements** — The Secretary does not reply via Telegram.
- **No Telegram delivery channels** — Assignment, follow-up, or reminder notifications no longer flow through Telegram.
- **Exception**: Historical Telegram records remain in Company Brain for audit trail; marked as superseded by this decision.

### 2. Telegram Delivery is NOT Task Completion
- Sending a message to Telegram, receiving a Telegram acknowledgement, or updating Telegram metadata **does not prove a business task is completed.**
- **Completion requires**: The actual external business outcome must be verified by the CEO.
- Example: "Create budget proposal" is not complete when Telegram acknowledges receipt; it is complete when the budget proposal exists, is reviewed, and is approved by the CEO.

### 3. CEO Coordinates All External Outcomes
- The **CEO is the gatekeeper for business outcome verification**.
- When the Secretary completes a task, it is not done until the CEO confirms:
  1. The external outcome exists and is correct (e.g., email sent, document created, partner contacted).
  2. The outcome meets the MD's original intent.
  3. Any required approvals or reviews are satisfied.
- The CEO reports back to the MD that the task is complete.

### 4. Secretary Stays Focused on Company Brain and Paperclip
- The Secretary maintains the Company Brain as the single source of truth.
- The Secretary creates and updates Paperclip tasks for assignments.
- The Secretary monitors Paperclip issue status and proposes follow-up tasks.
- The Secretary does not wait for external party replies; CEO handles that coordination.

---

## Workflow

### Assignment
1. **MD gives assignment** to the CEO (verbally, meeting, email, or other channel — not Telegram).
2. **CEO forwards to Secretary** through Paperclip issue or explicit coordination message.
3. **Secretary creates or updates Paperclip task** with details, priority, and external delivery method.
4. **Secretary documents assignment** in Company Brain (project, priority, or daily log) if relevant.

### Execution
1. **Agent/Responsible party** works on the task (email client, external partner, document creation, etc.).
2. **Task proceeds** in Paperclip with status updates (in_progress, pending_external, etc.).
3. **Secretary does NOT** send Telegram pings, wait for Telegram replies, or treat Telegram delivery as progress.

### Verification
1. **Actual outcome is delivered** (email sent, document received, partner confirmed, budget approved, etc.).
2. **CEO verifies** the outcome matches the MD's intent and is complete.
3. **CEO reports completion** to the Secretary or MD (through Paperclip issue, email, or meeting).

### Completion
1. **Secretary updates Paperclip task** to `done` or `in_review` (with CEO approval state).
2. **Secretary documents outcome** in Company Brain (decision log, project status, daily log).
3. **Secretary commits and pushes** Company Brain changes to GitHub.
4. **Task is complete** — the external outcome is verified and recorded.

---

## Key Changes from Previous Model

| Aspect | Previous (Telegram) | New (CEO Coordination) |
|--------|----------------------|----------------------|
| **Assignment channel** | MD → Telegram → Secretary | MD → CEO → Secretary (Paperclip) |
| **Completion signal** | Telegram message received | CEO confirms external outcome is correct |
| **Follow-up method** | Telegram 4-hour polling + morning reminder | CEO coordination + Paperclip status |
| **File/image intake** | Telegram media download + Drive upload | Paperclip attachments or Drive sharing |
| **Acknowledgement** | Telegram reply with commit ID | Paperclip issue comment or CEO report |
| **Source of truth** | Company Brain + Telegram chat history | Company Brain + Paperclip issue thread |

---

## Transition Notes

### Canceled Routines
- ❌ `Secretary Telegram 4-hour intake` (was `0 */4 * * * Etc/UTC`)
- ❌ `Secretary morning follow-up reminder` (was `0 9 * * * Asia/Bangkok`)

### Archived References
- Telegram bot token, chat ID, and offset tracking are no longer used.
- Historical Telegram entries in `routine.md` and `decisions.md` are marked as deprecated but preserved for audit.

### New Responsibilities
- Secretary monitors Paperclip issue backlog and proposes follow-up tasks.
- Secretary coordinates with CEO for outcome verification (inline in issue, email, or meeting).
- Secretary ensures Company Brain reflects CEO-verified outcomes, not just assignments.

---

## For External Partners / Vendors

- **No Telegram notification expected** — Vendors should not expect Telegram replies from the Secretary.
- **Communication channels**:
  - Email (MD, CEO, or assigned Agent)
  - Paperclip issue (if vendor has access)
  - Direct phone/video calls (scheduled via CEO)
  - Google Calendar invites (for meetings and reminders)

---

## Contacts & Escalation

- **MD**: Final decision maker; sets direction and approves outcomes.
- **CEO**: Coordinates business outcomes; verifies completion; reports to MD.
- **Secretary**: Maintains Company Brain; creates and tracks Paperclip tasks; documents outcomes.
- **Responsible Agent**: Executes the task (may be Secretary, third-party tool, or external vendor).

---

**Decision authority**: MD (Infinity Power 89)  
**Documentation authority**: Executive Secretary  
**Implementation date**: 2026-08-14  
**Tracked in Paperclip**: INF-877 (MD Decision), INF-879 (Update Company Brain)
