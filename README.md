# AiMe

A local analytical layer built on hardware you own, running inference you control, over data that never leaves your network without explicit permission.

Built by a power systems engineer who realized the architecture behind his day job was too useful an idea to leave at work.

*Planning to build this yourself? Jump to [For Builders](#for-builders).*

> **A note on the name:**
>
> The name is **AiMe**. Read it three ways:
>
> 1. *AI Me* — a model of yourself.
> 2. *Aim me* — give me direction.
> 3. *AI me* — let AI process me, make me legible to myself.
>
> The deeper idea: the mess is fine. AI does not need your data to be clean or organized to work with it. AiMe takes on the administrative layer of adult life — the tracking, the filing, the remembering, the following up — so your mind can focus on the parts of life that actually require a human.
>
> The name is settled. The project is not going anywhere.

---

## Table of Contents

| | | |
|---|---|---|
| [The Core Idea](#the-core-idea) | [Why It Works — The Routines Dashboard](#why-it-works--the-routines-dashboard) | [Core Use Cases](#core-use-cases) |
| [Why Build This](#why-build-this) | [What We've Built](#what-weve-built) | [How It Works](#how-it-works) |
| [Philosophy](#philosophy) | [Current State](#current-state) | [Documents](#documents) |
| | [For Builders](#for-builders) | |

---

## The Core Idea

**Getting Things Done** (GTD) is a productivity methodology with one core insight: your brain is a terrible reminder system. Every open loop — every task you need to remember, every commitment you've made, everything you need to do — occupies background processing cycles whether you're consciously thinking about it or not and more importantly, whether you can do anything about it in the moment or not. The overhead is invisible until you eliminate it. At that point, you wonder how you functioned before.

Adult life generates an enormous number of open loops. Not just the obvious ones — the ones that slip. Recurring tasks at every cadence that feel low-priority until they become urgent, expire, or cost you money. Dozens of these accumulate and form a persistent background hum of *what am I forgetting?* that never fully goes away.

GTD solves this by feeding all of these open loops into a trusted system that captures these open loops, organizes them into contextual buckets, and then surfaces them at the right time. GTD is a system with a set of rules and how the actual system looks is really up to the person implementing it.

AiMe fits the mold of this trusted system and even takes this a step further to even anticipate when some of these open loops could show up - giving you the information you need before you even need it.

AiMe is what GTD looks like when you stop managing that system manually and build infrastructure around it instead. The capture is automated. The processing is AI-assisted. The execution is scripted. Open loops don't just get captured — they get handled. Not just less time spent, but cognitive overhead permanently removed.

The routines dashboard is the concrete proof of this. See [Why It Works](#why-it-works--the-routines-dashboard) below.

---

## Why It Works — The Routines Dashboard

The first building session to catalogue all the routines I have did something simple: mapped every recurring task in life. Not just the obvious ones — daily hygiene, weekly in-baskets — but the ones that slip. The bills that need to be paid. Car maintenance like rotating your tires or adding more windshield washer fluid. The canceled flight credit that will expire if you don't use it by a certain day. Every cadence from daily to annual. Almost 60 tasks in total (with even more being added they come to mind).

Then an automation target was assigned to each one. Three categories emerged:

| Bucket | What it means | Example |
|---|---|---|
| 🚫 Off your plate entirely | AiMe handles it end-to-end, confirms it happened | Monthly maintenance scripts run automatically; a notification sent only when something is off |
| ⚡ Reduced to a confirmation tap | AiMe prepares everything, you approve | Rewards credit expiring in 7 days → one-tap reminder; you decide when to use it |
| 🧠 Stays manual | Genuinely requires human judgment or physical presence | Tax planning/preparation, investment decisions, car maintenance |

**The result, quantified:**

| | Hours/year |
|---|---|
| Before AiMe — total recurring task overhead | ~380 |
| Reclaimed at full deployment | ~195 |
| Remaining (genuinely requires a human) | ~185 |

**≈5 forty-hour work weeks freed per year.** Not by working harder — by building a system that handles what doesn't require a human, and surfaces what does at exactly the right moment, in context, without having to remember to check.

This is updated live in the Routines Dashboard — every task, every cadence, every automation status, with a Savings tab showing the full before/after breakdown. The numbers come from actual task data, not estimates. *Work in progress: this reflects approximately 80% of tracked routines. Household chores, outdoor and camping gear, rooftop tent equipment, and several other domains aren't mapped yet. The ~380 hrs/yr figure is a floor, not a ceiling.*

The deeper insight is about cognitive overhead, not just calendar time. A time-based reminder fires at the right moment in the calendar. A contextual reminder fires when the conditions in your actual life — your upcoming schedule, your consumption patterns, your device usage, your behaviors — indicate something needs attention. The time-based reminder requires a human to set up every case. The contextual reminder learns from what's already happening and projects forward.

The background hum of *what am I forgetting* — that quiets. That's the goal of the system, stated plainly.

---

## Core Use Cases

> Use case annotations: **🤖 AI** = requires model inference (classification, synthesis, reasoning) · **⚙️ Mech** = deterministic script, fixed rules, threshold alert — no model needed

### Routine automation — the cognitive overhead reclaim ⚙️ 🤖

*(Full story in [Why It Works](#why-it-works--the-routines-dashboard) above.)*

Every recurring task mapped, quantified, and automated to the extent possible. Most of the work is mechanical — deterministic scripts executing on a schedule, firing alerts on thresholds. AI handles the edge cases: classification, prioritization, context-aware surfacing. The dashboard is the live proof — not a projection, but a running system measuring actual overhead.

### Financial statement automation and reconciliation ⚙️ 🤖

The genesis use case. Every bank, credit card, and investment account generates statements. AiMe automates the pipeline end to end: detect when statements are ready, download via sanctioned OFX/QFX protocols, import to personal accounting software, flag anything unusual for human review. What used to take an afternoon becomes a confirmation tap.

### Rewards and credits tracking — stop leaving money on the table ⚙️

Hotel free night certificates that expire unused. Quarterly credits that roll over and disappear. Monthly perks that require manual activation. The average person with multiple travel cards leaves significant value unredeemed annually — not from carelessness, but from the cognitive overhead of tracking expiry dates across a dozen programs. AiMe monitors every balance, every expiry, every activation requirement, and surfaces reminders at the right time — 60 days out, 30 days, two weeks, the day before. **Running today.** Expiry alerts fire daily at 07:00 via a tiered alert system.

### Sleep and recovery scoring 🤖

Three devices capture sleep data: a dedicated ring as the primary source, a smartwatch as a gap-filler, sleep earbuds as secondary reference. No single device is perfect. AiMe reads all three, applies a consistent scoring model, produces a unified daily recovery assessment. Context flags — travel, unusual activity, substances — are factored in automatically. The system knows the difference between a low HRV reading on a normal night and the same reading after a red-eye flight.

### Car maintenance intelligence ⚙️ 🤖

A 12-year maintenance log for two 20+ year old high mileage used vehicles converted to dashboards showing every critical part, status tracked, service queue prioritized by urgency. "When did I last change the timing belt?" stops being something you have to remember and becomes something you can ask. **Running today** for a 2001 Audi A4 (~300k miles) and a 2003 Lexus ES300 (~200k miles). Eventual goal: cross-reference with financial records to calculate true cost of ownership and inform keep-versus-replace decisions with actual data.

### iMessage AI Assistant 🤖

Text a question to a designated number. The question is routed to an AI model (Mistral 7B) running locally. The reply arrives in iMessage. No external AI, no data leaving the network. **Running today** as a proof of concept — full triage layer and confirm→execute loop in progress.

### Decision archaeology — understanding how you got here 🤖

AiMe was built through hundreds of AI-assisted conversations — architecture decisions, tradeoffs, things tried and abandoned. That history is exportable and parseable. A tool was built specifically for this project which parses and indexes those exports, tagging conversations by topic and making them searchable. Eventually: AiMe reconstructs its own origin story from that data. The pattern generalizes to any domain where decisions accumulate — medical history, financial choices, professional pivots. Not just what happened, but why it was decided and what was known at the time.

---

## Why Build This

### 1. Data sovereignty — your data doesn't leave without explicit approval

Finance, health, location, and communication data run on local inference by default. Any external call requires explicitly declaring what data is being sent and why and explicit approval before anything leaves the network. Once data hits an external server, the expectation of removal is zero regardless of stated retention policy. Local by default prevents the problem entirely.

### 2. Questions that were previously unanswerable 🤖

The clearest demonstration: cross-reference location history, credit card records, calendar entries, and geotagged photos to reconstruct a trip itinerary from years ago. No consumer AI product can do this — they don't have your data. Local inference using your personal data is the only architecture that answers these questions without sending your location and financial history to a third party.

### 3. Single pane of glass — everything in one place ⚙️

Most people's data is scattered across dozens of services that don't talk to each other. Sleep data in one app. Finances in a desktop program. Calendar in an email client. Photos in cloud storage. AiMe builds a unified analytical layer over all of it without requiring migration or consolidation. The raw data stays where it lives. The mess is fine — that's the whole point.

### 4. Watches for you. Only tells you what matters. ⚙️ 🤖

The most underappreciated benefit: AiMe eliminates the cognitive overhead of monitoring, not just the overhead of doing. Right now, staying on top of adult life requires constant low-grade vigilance — checking expiry dates, remembering service intervals, noticing when something is running low. AiMe watches everything and surfaces only what actually needs your attention, only when it matters. Not a better calendar. A behavioral layer using data that is already available.

### 5. Resilience — not dead in the water when a cloud service changes ⚙️

When a cloud AI has an outage, changes pricing, deprecates a model, or shifts policy, AiMe keeps running. Local inference provides partial functionality even when the internet is unavailable. Not at full capacity, but not on the floor either.

### 6. No platform lock-in ⚙️

Built on open components: Ollama (local AI inference), LlamaIndex (RAG pipeline), Tailscale (encrypted mesh networking), Kasa smart plugs (power orchestration), plain markdown files for memory and context. No single point of failure that could break the whole system.

---

## What We've Built

A few things built in the course of this project are interesting as tools and patterns in their own right.

### Edit on any device, version on your own hardware ⚙️

The editing layer is iCloud — accessible from any device, no VPN needed. The versioning layer is a local git repository on the gateway. A single shell script bridges them: rsync iCloud → gateway, preview the diff, commit. Master files edited on an iPhone at a coffee shop are versioned on the home server by evening. No cloud git service involved.

### See exactly what changed before saving to version history ⚙️

A Flask-based web interface running on the gateway — accessible over Tailscale from anywhere — that shows which files changed between iCloud and git HEAD, full colorized inline diffs, a commit message input, and a one-click Sync+Commit button. No terminal required for routine session close-outs. The unstaged diff view catches errors that would otherwise survive to production. Built because the workflow needed a way to verify what actually changed before committing, not just a list of filenames.

### "Doorbell-only" notification architecture ⚙️

A privacy-preserving approach to push notifications: Pushover and iMessage carry only a signal and a Tailscale URL — never the personal content. The content lives on the mesh, served from the gateway. Personal data never passes through external notification servers regardless of what the notification is about. The device just rings; it doesn't know why.

### Data classification as a decision system 🤖

Rather than a lookup table of "what data can go where," the system uses four internalized rules that cover every case. The key insight is the aggregation principle: any derived or indexed data inherits the maximum sensitivity tier of any contributing input — not the average. One sensitive source makes the whole pipeline sensitive. This principle shapes the design of every planned pipeline before a line of code is written.

### Consistent Claude session instructions as a workflow layer 🤖

A working session ritual — grounding checklist, command discipline, Find/Replace format for document edits, close-out steps — is embedded in the master files and loaded at the start of every Claude session. This turns a capable AI into a consistent engineering partner with known behaviors across sessions with "memory" that carries over from session to session. The instructions are themselves a form of infrastructure: they reduce per-session friction and prevent an entire class of errors (wrong node, wrong file, unverified state). Other builders can adopt this pattern directly.

### Command confirmation with a logged audit trail ⚙️

Every state-changing command is flagged explicitly, confirmed before execution, and logged with a timestamp. The discipline is the logging as much as the confirmation. When something breaks three days later, the log shows exactly what changed. A read-only verification step precedes every state-changing command — not because the AI might be wrong, but because docs and runtime diverge, and the runtime is always ground truth.

---

## How It Works

### The Node Mesh

Tailscale (a WireGuard-based encrypted mesh VPN) connects all devices under a single private network accessible from anywhere. Every node is reachable by hostname from every other node regardless of physical location or ISP.

| Node | Device | Always-on | Idle draw † | Purpose |
|---|---|---|---|---|
| `relay` | Raspberry Pi 3B | ✅ | ~3–4W | Collection perimeter, Kasa control, mesh exit node — the only node hard-rebootable via smart plug |
| `gateway` | MacBook Air M1 | ✅ | ~3–8W | Control plane — Caddy reverse proxy, dashboards, iMessage AI, shared scripts, log aggregation |
| `compute` | MacBook Pro 16" | ❌ On-demand | ~1–3W sleeping / ~20W+ active | Primary inference node — DeepSeek R1 32B, woken via Kasa power cycle |
| `vault` | Galaxy Book (Windows) | ✅ | ~5W | MS Money, LlamaIndex RAG pipeline, Windows-native runtime |
| `viewer` | MacBook Air M3 | ❌ Travel | ~3–8W | Travel thin client — DeepSeek R1 14B via Ollama, fully offline AI fallback |

*† Idle draw figures are estimates based on published hardware specs. Measured values from Kasa smart plug telemetry will replace these once the energy monitoring dashboard is complete.*

**relay** deserves its name twice over: it is a protective relay in the power systems sense (operates independently of the system it protects) and a traffic relay (exit node, subnet router, Kasa bridge). If the gateway hangs, relay cycles its power outlet. If relay itself hangs, its own hardware watchdog reboots it autonomously. The rest of the system can fail completely; relay brings it back.

### Power Orchestration ⚙️

Kasa smart plugs give the system physical control over hardware — the Pi can wake the compute laptop by cycling its dock power outlet. An external archive drive is powered off by default, invisible and inaccessible until explicitly activated. Energy monitoring captures power consumption data for the planned efficiency dashboard.

Watchdog architecture runs two layers, because single-point watchdogs have their own failure modes:

| Layer | Mechanism | Status |
|---|---|---|
| Layer 1 | Pi hardware watchdog — self-recovery, 15-second timeout | ✅ Running |
| Layer 2 | gateway LaunchAgent — polls Pi, cycles Pi-Power outlet on failure | 🔧 Planned |

### The AI Stack

| Complexity | Example tasks | Model | Node |
|---|---|---|---|
| Low | GTD triage, iMessage routing, tracker queries | Mistral 7B | gateway (always-on) |
| Medium | Financial queries, cross-reference, reasoning | DeepSeek R1 14B | compute / viewer (travel) |
| High | Code, deep synthesis, complex analysis | DeepSeek R1 32B | compute (on-demand) |
| External | Open-ended reasoning, sanitized data only | Claude API | Last resort |

The governing model — drawn directly from power systems:

```
AI       =  protection relay   (detects, reasons, recommends)
Scripts  =  circuit breakers   (execute defined actions reliably)
Human    =  operator           (decides when to close the breaker)
```

Every consequential action requires explicit human confirmation. The AI recommends. The human gates. The script executes.

---

## Philosophy

### ADHD-friendly by design — remove friction, build momentum

Friction removal is the primary goal. The endgame is not a more organized to-do list — it is eliminating the cognitive overhead of remembering to do things at all. When all recurring routines were mapped and automation targets assigned, a load that felt overwhelming became genuinely manageable. That is the signal the architecture is working.

### OCD-friendly — trust but verify

The system is designed for effortless verification, not elimination of oversight. The autopay example: rather than stop checking, have the system confirm that payments processed and flag the ones that didn't — before the recovery window closes. You still verify. You just don't do it yourself every time. The same instinct applies to the build itself: prove something works at small scale before wiring it into the architecture.

### Human always in the loop

Every automation has a manual fallback. Every consequential action goes through an explicit confirmation gate. AI agents are used here only when a script genuinely cannot do the job — the blast radius of a bug is far larger with an agent than a script. Bounded blast radius is a first-class design requirement, not an afterthought.

### Redundancy at every tier

| Concern | Primary | Backup | Last resort |
|---|---|---|---|
| Windows execution | vault (native) | compute (Parallels) | viewer (Parallels, travel) |
| Pi recovery | Hardware watchdog | gateway cycles Pi-Power | — |
| File storage | iCloud | gateway sync copy | — |
| Local inference | Always-on small model | On-demand large model | Claude API |

No single failure takes the system down. Most double failures don't either.

### Deterministic execution, probabilistic reasoning — kept deliberately separate

**Deterministic:** scripts, file operations, power cycles, system commands. Same input always produces the same output. Auditable, debuggable, bounded blast radius.

**Probabilistic:** local models, RAG retrieval, recovery scoring, consumption predictions. Reasoning over uncertain inputs, producing best-estimate outputs that improve over time.

The architectural rule: probabilistic reasoning tells you *what* to do. Deterministic execution decides *how* it gets done. The human confirmation gate sits between them — the circuit breaker between the reasoning layer and the execution layer.

### Self-regulating — like 5/3/1, not a fixed plan

5/3/1 is a strength training methodology built on one insight: you don't go all-out every session. You work at a percentage of your tested maximum, then recalculate from real performance data — not what you planned. AiMe applies the same principle throughout. The consumables tracker adjusts reorder timing based on actual usage and upcoming trips, not fixed calendar intervals. The system observes actual outputs, compares to targets, and adjusts.

### Clean layer over raw data

You don't need to organize your existing data to use it. AiMe builds an analytical layer on top of data where it lives. Old emails, duplicate photos, years of unorganized files — all become searchable and queryable without touching a single one. The mess is fine. Cleanup becomes optional, not prerequisite.

---

## Current State

The infrastructure is built and running. The RAG pipeline and full AI triage layer are in progress. Several automation services are live.

| Layer | What it is | Status |
|---|---|---|
| Data sources | Banks, health devices, email, calendar, photos | 🔧 Partial — manual ingestion today |
| Collection perimeter | relay (Pi), Kasa polling, Tailscale mesh | ✅ Running |
| Control plane | gateway (M1), Caddy, dashboards, shared scripts | ✅ Running |
| Analytical layers | Finance, GTD, Health, Travel, Media | 🔧 In progress — services live, RAG pipeline pending |
| Heavy compute | compute (MBP), DeepSeek R1 32B, on-demand inference | ✅ Infrastructure and models ready |
| Data servers | vault (Windows), MS Money, LlamaIndex | ✅ Online — RAG pipeline pending |

**Current phase: Phase 1 — Partial Automation (PoC).** Infrastructure built and stable (Phase 0 ✅). Individual pipelines proven at small scale; first AI model set up and operational. Phase 2 target: pipelines wired end-to-end, behavioral notifications replace time-based alerts.

**What is running now:**

**Infrastructure & Mesh**
- Encrypted Tailscale mesh across all nodes, key expiry policy configured
- Raspberry Pi — hardware watchdog, thermal management, persistent journal logging
- Always-on gateway — reverse proxy, automated daily build pipeline

**Automation Services**
- **iMessage AI Assistant** — text a question, Mistral 7B answers locally, reply via iMessage; no external AI, no data off-mesh
- **Diagnostics agent** — daily SSH health reports, doorbell alert on degraded state
- **Rewards expiry alerts** — daily tiered notifications (60d/30d/7d) for credits, points, certificates
- **Monthly maintenance** — Pushover + iMessage confirm→execute loop; updates all nodes on approval

**Trackers & Dashboards**
- **Routine overhead dashboard** — 56 tasks mapped, Savings tab with full before/after breakdown
- **Rewards and credits tracker** — live, updated daily
- **Car maintenance dashboards** — Audi A4 and Lexus ES300
- **5/3/1 training dashboard** — 25+ cycles (2019–2026), AMRAP tracking, TM progression

**AI & Inference**
- Fully offline AI fallback on travel node (DeepSeek R1 14B, M3 Metal-accelerated)
- vault online — MS Money running, LlamaIndex foundation ready (RAG pipeline pending)

**Developer Tools**
- **Git commit UI** — iCloud↔gateway sync with diff preview and one-click commit

**What is being built next:**
- **RAG pipeline** — LlamaIndex over email, financial records, health data, calendar (Session D)
- **iMessage triage layer** — full routing to scripts, tracker queries, confirm→execute loop (Session C)
- **Automated statement import** — OFX/QFX download → MS Money pipeline
- **Recovery scoring dashboard** — Oura API auto-pull, unified daily score from multiple devices
- **Mac Mini M5 Pro** — primary always-on inference node, August 2026

---

## Documents

### Master files — paste at the start of every session

| File | Contents |
|---|---|
| `ARCHITECTURE.md` | Node roster, network layout, AI strategy, design principles |
| `OPS.md` | Current operational state, break state, prioritized work queue |
| `PLAN.md` | Hardware roadmap, AI architecture sessions, full use case backlog |
| `WORKFLOW.md` | How to work with the system — sessions, file management, routines |

### Supplemental reference — paste only when relevant

| File | Paste when... |
|---|---|
| `BENEFITS.md` | Evaluating new use cases or explaining the system to someone new |
| `OUTLOOK_WORKFLOW.md` | Working on email or calendar workflows |
| `ROUTINES.md` | Reviewing routines, running maintenance sessions, pre-travel checks |
| `PROCEDURES.md` | Step-by-step protocols for specific triggered events (iOS updates, backups) |
| `LESSONS_LEARNED.md` | What went wrong, what worked, what changed — the build's institutional memory |

---

## For Builders

Here's the honest version of why I built this.

I've spent a lot of time on this project. Not because I had spare time to fill, but because the alternative is continuing to hand personal financial history, medical data, and behavioral patterns to cloud services whose business model isn't aligned with mine. That tradeoff never sat right. Every time a useful use case came together, the same instinct fired: *I want the full power of AI working on this, but I'm not comfortable feeding my personal data into a system I don't control.* This is the solution I built because nothing existing solved it the way I needed.

Think of it as **an adulting assistant**: everyone has bills to pay, appointments to schedule, credits to use before they expire, and a stack of recurring tasks that are cognitively exhausting to track manually. You don't need to know what SCADA is to benefit from a system that watches your rewards so you don't leave money on the table, reminds you about the battery cycling you've been meaning to do for three months, and tells you when your car is due for service based on actual mileage — not a generic calendar interval. That's what this is, minus the data sovereignty trade-off that every commercial alternative forces on you.

I'm sharing this because AI capability and data sovereignty shouldn't require a trade-off. The tools to build this exist, they're open source, and the architecture is documentable. If this blueprint saves someone months of working through the same patterns, it was worth publishing. It's free, and it's going to stay free. The value of more people owning their data isn't something I'd want to put a price on.

One honest caveat: this isn't plug-and-play. It took real time, real decisions, and a willingness to break things and figure out why. AI-assisted tools like Claude make it dramatically more accessible than it would have been a few years ago — that's how much of this got built. But accessible isn't the same as risk-free. If you're building something that touches your personal data or runs on your home network, understand what you're deploying. Ask questions. Verify. The architecture in these docs is built with that discipline in mind. Bring the same discipline to your own build.

**Fork, adapt, contribute:** [github.com/tandrew101/a-i-me](https://github.com/tandrew101/a-i-me)

---

*Last updated: 2026-05-17 1545 ET*
