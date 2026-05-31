# AiMe — Data Classification Policy
**Version:** 1.2
**Date:** 2026-05-12
**Written with help from Claude.**

---

## What This Document Is

One of the first things built for AiMe was a policy for deciding what data can go where. Not as a theoretical exercise — as a practical gate. Before designing any pipeline, indexing any data, or routing any query to an AI model, the data involved gets classified. The tier assignment drives every downstream decision: which hardware processes it, whether it can leave the network, whether it gets logged.

This document is the policy. It's structured as a decision system, not a lookup table. Four rules cover the vast majority of cases. The tables below are worked examples of those rules applied to specific domains — reference them when you need to check a specific case.

**The four rules:**

1. Does it identify me or directly reveal my behavior, health, or finances?
   → **Sealed or local only. No exceptions.**

2. Could it identify me or reveal patterns *if combined* with something else?
   → **Local only. Aggregation rule applies. Most sensitive input tier wins.**

3. Is it amounts, metadata, or operational data with no identity signal?
   → **Local preferred. External OK with minimal review.**

4. Is it infrastructure or telemetry only — no personal content at all?
   → **Unrestricted.**

---

## Tier Definitions

| Tier | Short name | External AI | Definition |
|---|---|---|---|
| **T1 🔒** | Sealed | Never | Maximum sensitivity. Combines personal identity, behavioral patterns, cryptographic keys, or clinical detail. Requires explicit unlock before any AI reasoning. Examples: estate documents, clinical mental health records, personal context history. |
| **T1** | Local only | Never | Sensitive personal data. Physiological measurements, financial transactions, location history, email content, raw journal entries. Never touches an external AI regardless of sanitization. |
| **T2 🔑** | Policy gate | With explicit approval only | Local by default. Can go external only after declaring exactly what data is being sent, what was removed and why it's safe, and receiving explicit confirmation. No bypassing. |
| **T2** | Safe to send | With minimal review | Amounts, product names, maintenance schedules, published content. No account numbers, no personal details. External is acceptable. |
| **T3** | Unrestricted | Unrestricted | Infrastructure and operational data only. System measurements, service status, power readings. No personal content. |

---

## How to Use This Policy

**Run the four rules above — don't memorize the tables.**

The tables below are reference material for edge cases. The rules cover everything. When a new use case comes up, run the rules first. The examples will agree with the rules every time.

The one rule to hold onto: **derived data inherits the maximum tier of any input.** Combine public information with even one piece of sensitive personal data and the result is sensitive. One local-only input makes the whole output local-only. No exceptions.

---

## Working With External AI

The mental model when sharing anything with an external AI service:

**Share structure, not data.**

It's fine to describe how a system works, what a schema looks like, what decisions were made and why. It's not fine to paste actual values — transactions, health readings, message content, location coordinates. The line: *describing the shape of data* is safe; *sharing an actual value that could identify you* is not.

**Minimize your footprint.**

Every conversation on an external AI service is data on someone else's server. Old conversations that contain any personal detail should be archived and cleared when they're no longer needed for active work. Elimination is impossible — every cloud interaction leaves some trace. But active footprint reduction is the right posture. The question to ask periodically: does this conversation need to remain accessible on this service, or can it be deleted?

**Telemetry and infrastructure questions are unrestricted.**

Questions about how the home server is structured, what a script does, how to configure a service — none of this contains personal data. External AI is appropriate for all of this. The restriction is specifically on data that flows through or is processed by that AI infrastructure.

**Never share credentials with any external AI.**
API keys, passwords, authentication tokens, and session secrets should never appear in any external AI conversation — not even partially, not even for debugging. If something needs to be redacted before sharing, redact it before typing it. Once a credential appears in a conversation on an external server, treat it as potentially compromised and rotate it.

**The aggregation rule applies to AI context too.**

If a conversation starts with infrastructure questions and gradually accumulates personal details — a health reading here, a location there, a financial note later — the conversation as a whole becomes more sensitive than any individual message. Treat the cumulative content of a long session the same way you'd treat a single message with all of that content combined.

---

## The Aggregation Rule

If you combine public information with even one piece of sensitive personal data — location, health, financial history — the result is sensitive. Innocuous pieces combine into a fingerprint that identifies you even when no single piece would.

**The rule:** any derived or indexed data inherits the maximum tier of any contributing input — not the average. One sensitive source makes the whole pipeline sensitive.

Examples:
- An index spanning email + financial records + calendar → **Local only**
- A log capturing observations about yourself over time → **Local only** (behavioral fingerprint by accumulation)
- A summary combining medical history + location + purchase data → **Sealed 🔒**
- Power usage statistics with no personal content → **Unrestricted**

---

## Use Case Classification

### Infrastructure

| Use Case | Tier | Rationale |
|---|---|---|
| Node telemetry (temperature, load, uptime) | Unrestricted | System metrics only |
| Smart outlet power readings | Unrestricted | Watts, not behavior |
| Service status and watchdog events | Unrestricted | Operational |
| Dashboard builds and inventory | Unrestricted | Infrastructure metadata |

---

### Productivity

| Use Case | Tier | Rationale |
|---|---|---|
| Task capture | Local only | Task content reveals priorities, commitments, relationships |
| Task triage and classification | Local only | Processing local-only content |
| Context-aware notifications | Local only | Requires location + schedule + task content — aggregation rule applies |
| Journaling (raw entries) | Local only | Behavioral fingerprint by design |
| Journaling (themes only) | Policy gate 🔑 | Abstracted content — external with explicit approval |

---

### Finance

| Use Case | Tier | Rationale |
|---|---|---|
| Rewards and credits (balances, expiry) | Safe to send | Amounts and product names only — no account numbers |
| Gift cards (balances only) | Safe to send | No financial identity |
| Card optimizer (purchase category suggestions) | Safe to send | Category-level only — no transaction history |
| Transaction history and cost basis | Local only | Full financial records |
| Portfolio and investments | Local only | Holdings and values |
| Cash flow and spending patterns | Local only | Income and spending behavior |
| Tax data | Local only | Income, deductions, taxable events |
| Bank and investment statements | Local only | Raw financial records |

---

### Health

| Use Case | Tier | Rationale |
|---|---|---|
| Fitness and workout logs | Local only | Health data with behavioral patterns |
| Sleep ring data (heart rate, temperature) | Local only | Physiological signals at daily cadence |
| Sleep debt and recovery tracking | Local only | Sleep schedule and quality over time |
| Personal health profile | Sealed 🔒 | Medical record — diagnoses, medications, family history |
| Mental health history | Sealed 🔒 | Clinical record — diagnoses and treatment |
| Health inference for anxiety patterns | Sealed 🔒 | Combines sealed health profile with current symptoms |
| Medical questionnaire help | Sealed 🔒 | Draws from sealed health profile |

---

### Travel and Location

| Use Case | Tier | Rationale |
|---|---|---|
| Trip logging and movement patterns | Local only | Reveals schedule, home absence windows, destinations |
| Real-time location sharing | Local only | Live location — highest real-time exposure |
| Email content (for travel confirmations) | Local only | Email content, even when parsing only confirmations |
| Travel post drafting — final output for publication | Safe to send | Content intended for public posting |

---

### Media

| Use Case | Tier | Rationale |
|---|---|---|
| Photo and video ingestion and tagging | Local only | Personal photos — faces, locations, timestamps |
| AI curation and deduplication | Local only | Processing local-only content |
| Private or hidden media | Local only | Personal media — assume sensitive |
| Published travel post — final output | Safe to send | Published output, not raw source material |

---

### Personal

| Use Case | Tier | Rationale |
|---|---|---|
| Consumables tracking (purchase timing) | Safe to send | No identity signal |
| Vehicle maintenance log | Safe to send | Service history, no financial detail |
| Email spam and subscription scanning | Local only | Email content reveals behavior and subscriptions |
| Observations about yourself over time | Local only | Behavioral fingerprint by accumulation |
| Personal context history | Sealed 🔒 | Aggregates all tiers — maximum sensitivity by aggregation rule |

---

### Relationships

| Use Case | Tier | Rationale |
|---|---|---|
| Message and conversation archives | Sealed 🔒 | Interpersonal content and behavioral fingerprint |
| Relationship history | Sealed 🔒 | Highest relational sensitivity |

---

### Estate and Legacy

All estate and legacy use cases are **Sealed 🔒** — no exceptions.

| Use Case |
|---|
| Will and beneficiary documentation |
| Asset inventory (accounts, property, digital assets) |
| Notification plan (who gets told what, in what order) |
| Data deletion instructions |
| Cryptographic key storage and emergency access |

---

## Key Rules

**No reclassifying upward.**
Once something is classified as local-only or sealed, it doesn't get promoted to a looser tier because it would be convenient. Reclassifying stricter (moving toward sealed) is always fine. Reclassifying looser requires a new discussion with documented rationale.

**Classify before building.**
Any new use case gets a tier assigned before any pipeline is designed. Build first and classify later is how sensitive data ends up in the wrong place.

**Default conservative.**
When a use case is ambiguous, assign the stricter tier and relax only after deliberate reasoning. Start local, expand carefully.

**Certain providers are excluded regardless of tier.**
Some external AI providers are excluded from use entirely — not because of what data they'd receive, but because of who operates them. This exclusion is enforced at the architecture level: no data of any sensitivity goes to these providers, ever. This is a structural decision, not a per-request policy check.

**Model routing rules are in ARCHITECTURE.md.**
The specific rules for which hardware handles which tier, and what external AI is permitted for T2 data, are maintained in the architecture documentation rather than here. This policy defines the tiers; the architecture documentation defines the routing.

---

*This policy was established during an early architecture session of the AiMe build as part of defining use cases and data sensitivity tiers. It governs all subsequent pipeline and AI architecture decisions.*

*Written with help from Claude.*