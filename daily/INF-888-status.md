# INF-888: L4 Lamp Cost & Profit Calculation — Status & Blocker

**Issue**: INF-888 — คำนวณต้นทุนและกำไร โคมไฟ L4  
**Status**: 🔴 **BLOCKED** — Missing selling price data  
**Parent**: INF-884 ติดตามการสั่งทำโคมไฟ L4 และ ลงบันทึกในระบบ drive  
**Date**: 2026-08-18

---

## Current Situation

### Data Received ✅
- **Product Code**: L4 (โคมไฟแขวนผนัง — wall-mounted pendant lamp)
- **Quantity**: 4 lamps
- **Unit Cost**: 820 CNY/lamp (ordered from China, manufacturing in progress)
- **Status**: 1 lamp delivered; 3 lamps awaiting delivery
- **Location**: 15th-floor conference room hotel

### Calculations Possible ✅
With cost data only, I can compute:
1. **Total Raw Cost**: 820 CNY/lamp × 4 = 3,280 CNY total
2. **Cost in THB**: 3,280 CNY ÷ exchange rate = ฿X

### Calculations Blocked ❌
Without selling price, cannot compute:
1. **Selling price per lamp** — (ราคาขาย/โคม)
2. **Total selling revenue** — (ราคาขายรวม 4 โคม)
3. **Profit per lamp** — (ราคาขาย - ต้นทุน)
4. **Total profit** — (กำไรรวม)
5. **Gross margin %** — (อัตรากำไรขั้นต้น)

---

## Blocker

**Issue**: Selling price (ราคาขาย) not provided in INF-888 description

**Required Data**:
- ❓ **Selling price per lamp** (in THB or CNY)
- ⚠️ May also need: CNY→THB exchange rate if cost should be converted

---

## Workaround / Template

Once MD/CEO provides selling price, I can immediately compute a full financial summary:

| Item | Calculation | Value |
|------|-------------|-------|
| Unit Cost | 820 CNY/lamp | 820 CNY |
| **Selling Price/lamp** | ❓ TBD | ❓ TBD |
| Profit/lamp | Selling - Cost | ❓ TBD |
| **Total Cost (4 lamps)** | 820 × 4 | 3,280 CNY |
| **Total Selling (4 lamps)** | Price × 4 | ❓ TBD |
| **Total Profit (4 lamps)** | Selling - Cost | ❓ TBD |
| **Gross Margin %** | (Profit / Selling) × 100 | ❓ TBD |

---

## Next Action

**Blocker Owner**: MD or CEO (whoever controls pricing)  
**Blocker Action**: Provide selling price per lamp (ราคาขาย/โคม)

Once provided:
1. Secretary will complete all profit calculations
2. Document results in Company Brain
3. Mark INF-888 as `done`

---

## Alternative: Check Parent Issue INF-884

May contain pricing info in parent scope. Check INF-884 comments for selling price clarification.

---

**Created**: 2026-08-18 (Agent 7c12ca06...)  
**Status**: BLOCKED — Awaiting selling price input
