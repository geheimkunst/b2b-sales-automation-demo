# Development Journey: B2B Sales Reporting Ecosystem

## The Problem

After two years in B2B sales expansion, I experienced operational bottlenecks daily:
- **Manual data analysis:** 5+ hours per week for report creation
- **Inconsistent reports:** Different sources, different formats
- **Speed vs. Accuracy trade-off:** Fast reports = errors, accurate reports = slow

The question was: **Can I show that I don't just identify problems, but also build solutions?**


---

## My Approach

Instead of theoretically discussing technical skills, I built a working system:

- **Initiative:** Independently purchased license and evaluated the product
- **User perspective:** Understand first, then build
- **Validation > Slide decks:** Test hypotheses with working code

**Result:** A working demo of a B2B sales reporting setup, built in 35 test runs for $3.46. It is a practice project with invented data.

---

## TL;DR

| Metric | Value |
|:-------|:------|
| **Test Runs** | 35 |
| **Total Cost** | $3.46 |
| **Error Types Identified** | 5 |
| **Assistants Built** | 3 |

---

## Phase 1: Setup & Data

**What I did:**
- Platform evaluation and tool selection ([Details](./TOOL-COMPARISON.md))
- Created test dataset: 10 accounts, 15 invoices, 12 tickets, 10 leads
- Correct ID linking (Invoices → Accounts → Tickets)

**Key Learning: Data consistency is the foundation**

> **Problem:** Workflow failed – invoices couldn't be mapped to accounts.
> **Root cause:** Inconsistent IDs (ACC-2024-001 vs. ACC-001).
> **Fix:** Complete regeneration with validation script.

**Transferable:** Early validation saves money. In the real world, this would be an API call to Salesforce – same logic.

---

## Phase 2: Assistants & Prompts

**What I did:**
- Configured Sales Research Assistant
- Iterated prompt from v1.0 (generic) to v2.0 (adapted to data structure)
- Improved score: 3.0/5 → 4.7/5

**Key Learning: Prompt adaptation to data structure makes 70% of the difference**

```
BEFORE: "Analyze the accounts and prioritize them."

AFTER: "Analyze using the following fields:
- mrr_eur (numeric)
- health_score (0-100, where <50 = Churn Risk)
- icp_score (0-100)
```

> Prioritization based on defined scoring formula: **[SCORING.md](./SCORING.md)**

---

## Phase 3: Workflow & Error Marathon

**What I did:**
- Built 7-node workflow (Trigger → Files → Agent → Email)
- Executed 35 test runs
- Documented 5 different error types

### The 5-Phase Error Taxonomy

| Phase | Error | Cost | Fix |
|:------|:------|:-----|:----|
| 1 | File Download (wrong IDs) | $0 | Use File Picker |
| 2 | Schema Mismatch (Markdown instead of JSON) | $0.64 | Explicit output schema |
| 3 | Connection (Gmail not connected) | $0.50 | Integration BEFORE build |
| 4 | Email Rendering (broken Markdown) | $0 | Plain text instead of HTML |
| 5 | Production (stable) | $0.49 | - |

**Key Learning: Early validation saves money**

> 80% of costs occurred in Phase 2 because the Agent was already executing.
> **Solution:** Validation BEFORE expensive LLM calls.

---

## Test Results

| Assistant | Score | Highlights |
|:----------|:------|:-----------|
| Sales Research | 4.7/5 | Data structure, Churn Risk detection |
| Customer Support | 5.0/5 | Structured knowledge, Security rules |
| HR Policy | 5.0/5 | DACH-specific, Language rules |

**Scoring Criteria:**
- Data Accuracy (30%)
- Context Understanding (25%)
- Output Structure (20%)
- Rule Adherence (15%)
- Added Value (10%)

---

## Next Steps

- **Production Scale:** Monitoring, alerting, multi-user support
- **Custom API Integration:** Integration without no-code platform
- **Observability:** LangSmith/Helicone for LLM metrics
