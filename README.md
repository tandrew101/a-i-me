# AiMe

A local analytical layer built on hardware you own, running inference you control, over data that never leaves your network without explicit permission.

Built by a power systems engineer / project manager who realized the architecture behind his day job was too powerful an idea to leave at work.

*Planning to build this yourself? Jump to [For Builders](#for-builders).*

> **A note on the name:**
>
> The name is **AiMe**. Read it three ways:
>
> 1. *AI Me* — a model of yourself.
> 2. *Aim me* — give me direction.
> 3. *AI me* — let AI process me, make me legible to myself.
>
> The deeper idea: the mess is fine. AI does not need your data to be clean or
> organized to work with it. AiMe takes on the administrative layer of adult life —
> the tracking, the filing, the remembering, the following up — so your mind can
> focus on the parts of life that actually require a human.
> The name is settled. The project is not going anywhere.

---

## Table of Contents

| | | |
|---|---|---|
| [The Core Idea](#the-core-idea) | [Why Build This](#why-build-this) | [Current State](#current-state) |
| [Core Use Cases](#core-use-cases) | [How It Works](#how-it-works) | [Documents](#documents) |
| | [Philosophy](#philosophy) | [For Builders](#for-builders) |

---

## The Core Idea

### For power systems engineers

**CYME** is commercial power systems analysis software used by utilities and engineering
firms worldwide — it is the tool engineers open when they need to model an electric
distribution system. **CYME Gateway** is the integration layer that automatically builds
that model from real-world data sources so that the engineer does not have to build it
by hand:

- **GIS** (Geographic Information System) — asset locations, network topology, equipment specs
- **SCADA** (Supervisory Control and Data Acquisition) — real-time operational state
- **AMI** (Advanced Metering Infrastructure) — smart meter consumption and power quality data

Gateway ingests all of it, resolves conflicts, fills gaps, and hands you a queryable
network model. The analytical tools — fault analysis, load flow, contingency simulation
— plug into that model and run on top of it.

AiMe applies this exact architecture to a person instead of a power system:

| CYME Gateway | Layer | AiMe |
|---|---|---|
| GIS, SCADA, AMI feeds | Data sources | Banks, health devices, email, calendar, photos |
| Gateway ingestion layer | Collection perimeter | `relay` — Raspberry Pi |
| CYME network model | Control plane | `gateway` — MacBook Air M1 |
| Fault analysis, load flow, DMS | Analytical layers | Finance, GTD, Health, Travel, Media |
| Compute servers | Heavy workloads | `compute` — MacBook Pro (on demand) |
| SCADA historians / legacy systems | Data servers | `vault` — Windows, MS Money, RAG |

### For everyone else

Imagine you could build a complete, structured model of your own life — your finances,
health, travel, communications, and habits — the same way engineers build a digital
model of a power grid. Then imagine being able to ask that model questions and get
real answers grounded in your actual data, not generic advice.

That is what AiMe does.

```
Your data (banks, health devices, email, calendar, photos)
                          ↓
               Collection perimeter
                          ↓
                    Control plane
                          ↓
       Finance · Health · Travel · GTD · Media
                          ↓
              Heavy compute (on demand)
              Data servers (always-on)
```

---

## Core Use Cases

The project started with a specific frustration: manually downloading bank and credit
card statements every month, importing them into personal accounting software, and
reconciling everything by hand. It was tedious, error-prone, and consumed time that
could have been spent on literally anything else. The question was simple — can a
local AI handle this? The answer turned out to be yes, and then much more than that.

### Financial statement automation and reconciliation

The genesis use case. Every bank, credit card, and investment account generates
statements. Downloading them, converting formats, importing, checking for anomalies,
tracking category spend — all mechanical work that follows predictable rules. AiMe
automates the pipeline end to end: detect when statements are ready, download, convert,
import, flag anything unusual for human review. What used to take an afternoon becomes
a confirmation tap.

### Routine automation — the cognitive overhead reclaim

During a single planning session, every recurring routine was mapped out — daily,
weekly, monthly, quarterly, annually. Then automation targets were layered on top.
The result: a calendar year of tasks that felt overwhelming collapsed into a manageable
structure where most of the work is either handled automatically or surfaced at exactly
the right moment as a confirmation prompt. This is the use case that revealed the full
power of the architecture — not any single automation, but the cumulative effect of
removing friction everywhere simultaneously.

### Sleep and recovery scoring

Three devices capture sleep data: a dedicated sleep ring as the primary source, a
smartwatch as a gap-filler, and sleep earbuds as a secondary reference. No single
device is perfect. AiMe reads all three, applies a consistent scoring model, and
produces a unified daily recovery assessment. Context flags — travel, unusual activity,
substances — are logged manually and factored in automatically. The system knows the
difference between a low HRV reading on a normal night and the same reading after a
red-eye flight. One score, grounded in all available data.

### Rewards and credits tracking — stop leaving money on the table

Hotel free night certificates that expire unused. Quarterly credits that roll over
and disappear. Monthly perks that require manual activation. The average person with
multiple travel credit cards leaves hundreds of dollars per year unredeemed simply
because tracking expiry dates across a dozen programs is cognitively exhausting.
AiMe monitors every balance, every expiry, every activation requirement, and surfaces
reminders at the right time — 60 days out, 30 days, two weeks, the day before.

### Car maintenance intelligence

A 12-year maintenance log for a 2001 Audi and a 2003 Lexus. The dashboards model each
vehicle's systems using a circuit breaker architecture — every component mapped to the
bus it belongs to, status tracked, service queue prioritized by urgency. The question
"when did I last change the timing belt?" stops being something you have to remember
and becomes something you can ask. Eventually: cross-reference with financial records
to calculate true cost of ownership and inform keep-versus-replace decisions with
actual data.

### Trip reconstruction and narrative generation

You took a trip in late 2023. You remember a great meal but can't recall where — you
paid by credit card but never kept the receipt. AiMe cross-references location history,
credit card records, calendar entries, and geotagged photos to reconstruct the full
itinerary. Then it goes further: draft a narrative summary of the trip, anchored by
the photos and enriched by the financial and location data. Memory becomes queryable.
Experiences become stories automatically.

### Decision archaeology — understanding how you got here

AiMe was built through hundreds of AI-assisted conversations — architecture decisions,
tradeoffs, things tried and abandoned. That history exists as exportable conversation
data. The `chatgpt-parser.html` tool built for this project parses and indexes those
exports, tagging conversations by topic and making them searchable.

The application: AiMe will eventually reconstruct its own origin story from that data.
When did the Pi's role get demoted to edge-only? When was the CYME analogy first
articulated? What drove the shift from polling-based to event-driven automation? The
answers exist in the conversation history. A RAG pipeline (a technique where an AI
searches your own documents before answering, rather than relying on generic training)
over that corpus makes them queryable.

The pattern generalizes to any domain where decisions accumulate: medical history,
financial choices, professional pivots. Not just what happened — but why it was
decided, what alternatives were considered, and what was known at the time.

### Open loop surfacing — nothing gets permanently lost

You connected with someone, had a genuinely promising exchange, and then life got busy.
Weeks later you remember the conversation existed but have no idea where the thread
went. AiMe treats these as GTD (Getting Things Done) open loops — unresolved items
that deserve a periodic review. The system surfaces them: "you were in touch with
this person in March, the conversation was warm, you never followed up — still want
to?" Applied to any domain where threads go cold: professional contacts, unfinished
projects, promised follow-ups, conversations that ended mid-thought. Nothing is
deleted. Everything is reviewable.

---

## Why Build This

Every time a use case came together, the same instinct fired: *I want the full power
of AI working on this — but I am not comfortable feeding my personal data into a
cloud service I do not control.* That tension is what AiMe resolves. Data sovereignty
was the original driver. The rest of the benefits emerged from building toward it.

### 1. Data sovereignty — your data does not leave without explicit approval

Finance, health, location, and communication data run on local inference by default.
Any external call requires explicitly declaring what data is being sent, what
sanitization was applied, and why it is safe — before anything leaves the network.

Once data hits an external server, the expectation of removal is zero regardless of
stated retention policy. Local by default prevents the problem entirely.

### 2. AI over your actual data — questions that were previously unanswerable

The clearest demonstration: you took a trip in late 2023, you remember a great meal
but cannot recall where — you paid by credit card but never kept the receipt.
Cross-reference location history, credit card records, calendar entries, and photos
with geolocation and timestamps. Reconstruct the itinerary. Draft the narrative.

No consumer AI product can do this. They do not have your data. Local inference plus
a RAG pipeline over your personal data corpus is the only architecture that answers
questions like this without sending your location and financial history to a third party.

### 3. Single pane of glass — everything in one place

Most people's data is scattered across dozens of services that do not talk to each
other. Sleep data in one app. Finances in a desktop program. Calendar in an email
client. Photos in cloud storage. Location history in a mapping service.

AiMe builds a unified analytical layer over all of it without requiring you to migrate
or consolidate anything. The raw data stays where it lives. The mess is fine — that is
the whole point. You do not need one perfect service. You need one good integration layer.

### 4. Environmental impact — efficiency as a design value

Every node in this system was chosen or configured to minimize idle power draw — see
the node table in How It Works for the full comparison. The always-on nodes draw
between 3W and 8W each. The high-performance laptop that handles heavy workloads
sleeps at 1-3W and wakes only when needed. Smart plug monitoring captures energy
consumption data that feeds a planned efficiency dashboard. The hypothesis: local
Apple Silicon inference is meaningfully more efficient per query than cloud
alternatives, especially for structured, repetitive tasks.

### 5. Resilience — you are not dead in the water when a cloud service goes down

When a cloud AI has an outage, changes pricing, or deprecates a model, the system
keeps running. Local inference provides partial functionality even when the internet
is unavailable — like an N-1 contingency in a distribution system. Not at full
capacity, but not on the floor either.

### 6. No platform lock-in

Built on open components: Ollama (local AI inference), LlamaIndex (RAG pipeline),
Tailscale (encrypted mesh networking), Kasa smart plugs (power orchestration), and
plain markdown files for memory and context. No single point of failure that could
break the whole system.

---

## How It Works

### The Node Mesh

Tailscale (a WireGuard-based encrypted mesh VPN) connects all devices under a single
private network accessible from anywhere. Every node is reachable by hostname from
every other node regardless of physical location or ISP.

| Node | Device | Always-on | Idle draw † | Purpose |
|---|---|---|---|---|
| `relay` | Raspberry Pi 3B | ✅ | ~3–4W | Collection perimeter, Kasa control, mesh exit node — the only node hard-rebootable via smart plug |
| `gateway` | MacBook Air M1 | ✅ | ~3–8W | Control plane — Caddy reverse proxy, GTD dashboard, shared scripts, log aggregation |
| `compute` | MacBook Pro 16" | ❌ On-demand | ~1–3W sleeping / ~20W+ active | Heavy AI workloads — woken via Kasa power cycle, sleeps otherwise |
| `vault` | Galaxy Book (Windows) | ✅ | ~5W | MS Money, LlamaIndex RAG pipeline, Windows-native runtime |
| `viewer` | MacBook Air M3 | ❌ Travel | ~3–8W | Travel thin client — DeepSeek R1 14B via Ollama, fully offline AI fallback |

*† Idle draw figures are estimates based on published hardware specs. Measured values from Kasa smart plug telemetry will replace these once the energy monitoring pipeline is restored — see Current State.*

**relay** deserves its name twice over: it is a protective relay in the power systems
sense (operates independently of the system it protects) and a traffic relay (exit
node, subnet router, Kasa bridge). If the gateway hangs, relay cycles its power
outlet. If relay itself hangs, its own hardware watchdog reboots it autonomously.
The rest of the system can fail completely; relay brings it back.

### Power Orchestration

Kasa smart plugs give the system physical control over hardware — the Pi can wake the
compute laptop by cycling its dock power outlet. An external archive drive is powered
off by default, invisible and inaccessible until explicitly activated. Energy
monitoring captures power consumption data for the efficiency dashboard.

Watchdog architecture runs two layers, because single-point watchdogs have their own
failure modes:

| Layer | Mechanism | Status |
|---|---|---|
| Layer 1 | Pi hardware watchdog — self-recovery, 15-second timeout | ✅ Running |
| Layer 2 | gateway LaunchAgent — polls Pi, cycles Pi-Power outlet on failure | 🔧 Planned |

### The AI Stack

| Complexity | Example tasks | Model | Node |
|---|---|---|---|
| Low | GTD triage, tracker queries | Mistral 7B | gateway (always-on) |
| Medium | Financial queries, cross-reference | DeepSeek R1 14B | compute |
| High | Code, deep reasoning | Larger models | compute |
| External | Open-ended reasoning, sanitized data only | Claude API | Last resort |

The governing model — drawn directly from power systems:

```
AI       =  protection relay   (detects, reasons, recommends)
Scripts  =  circuit breakers   (execute defined actions reliably)
Human    =  operator           (decides when to close the breaker)
```

Every consequential action requires explicit human confirmation. The AI recommends.
The human gates. The script executes.

---

## Philosophy

### ADHD-friendly by design — remove friction, build momentum

Friction removal is the primary goal. Every manual routine in this system is a
candidate for automation. The endgame is not a more organized to-do list — it is
eliminating the cognitive overhead of remembering to do things at all. When all
recurring routines were mapped out and then layered with automation targets, a load
that felt overwhelming became genuinely manageable. That is the signal the
architecture is working.

The priority system evolved to reflect how a multi-year build actually gets finished.
Urgent items first. Important items next. Then quick wins that build momentum — fun
sessions that ship something beat grinding sessions that stall. A third axis emerged
over time: proof-of-concept work. Before committing something to the architecture,
build a small version first and prove it works. The iMessage gateway is being tested
empirically before becoming a dependency. The Pushover loop was built as a standalone
circuit before being wired into the broader automation. Confidence before scale.
All three matter as much as urgency.

### OCD-friendly — trust but verify

The system is designed for effortless verification, not elimination of oversight.
The autopay example: payments were being scheduled manually due to a reasonable
concern about silent failures. The solution is not to stop checking — it is to have
the system confirm that payments processed and flag the ones that did not, before the
recovery window closes. You still verify. You just do not do it yourself every time.

The same pattern runs throughout: credit expiry alerts, system health checks,
connectivity monitoring. The system watches so you do not have to watch constantly —
but it always tells you what it saw. The same instinct eventually extended to the
build itself — prove something works at small scale before wiring it into the
architecture.

### Human always in the loop — agents as last resort

A power system operator does not send an autonomous robot to close a breaker. They
assess the situation, make a decision, and execute. AI agents are only used here when
a simple script genuinely cannot do the job. The reason: the blast radius of an agent
bug is far larger than a script bug. Scripts are auditable, debuggable, and bounded.
Agents can chain unexpected actions before anyone notices something went wrong.

### Redundancy at every tier — N-1 everywhere, N-2 where it counts

Every critical path has at least one fallback. Several have two:

| Concern | Primary | Backup | Last resort |
|---|---|---|---|
| Windows execution | vault (native) | compute (Parallels) | viewer (Parallels, travel) |
| Pi recovery | Hardware watchdog | gateway cycles Pi-Power | — |
| File storage | iCloud | gateway sync copy | — |
| Local inference | Always-on small model | On-demand large model | Claude API |

No single failure takes the system down. Most double failures do not either.

### Deterministic execution, probabilistic reasoning — kept deliberately separate

**Deterministic:** scripts, file operations, power cycles, system commands. Same input
always produces the same output. Auditable, debuggable, bounded blast radius.

**Probabilistic:** local models, RAG retrieval, recovery scoring, consumption
predictions. Reasoning over uncertain inputs, producing best-estimate outputs that
improve over time.

The architectural rule: probabilistic reasoning tells you *what* to do. Deterministic
execution decides *how* it gets done. The human confirmation gate sits between them —
the circuit breaker between the reasoning layer and the execution layer. A
probabilistic output never directly triggers a consequential action without a
deterministic confirmation step in between.

### Self-regulating — like 5/3/1, not a fixed plan

5/3/1 is a strength training methodology built on a specific insight: you do not go
all-out every session. You work at a percentage of your tested maximum, then
recalculate that maximum from real performance data — not what you planned. Stronger
than expected? The program adjusts up. Running a deficit? It accounts for that rather
than grinding you through a weight you cannot handle. The program improves by
measuring what actually happened.

AiMe applies the same principle throughout. The sleep tracker maintains a rolling
sleep debt and ratchets sleep need upward when persistent deficit is detected — rather
than letting the system normalize chronic under-sleep as a new baseline. The
consumables tracker adjusts reorder timing based on actual usage patterns and upcoming
trips, not fixed calendar intervals. The system observes actual outputs, compares them
to targets, and adjusts parameters accordingly.

### Simple by design — graceful manual fallback

Every automation has a manual path that requires nothing new to learn. If the
Pushover loop breaks, the monthly maintenance still gets done manually. If the iMessage
gateway goes down, questions still get answered via a terminal session. The system
saves your bandwidth for what matters; it does not create new fragile dependencies
that collapse everything when they break.

### Use what you have — optimize, then upgrade

This project runs on hardware that already existed. Nothing was purchased specifically
for it until the foundation was stable enough to benefit from better hardware. The
Raspberry Pi sitting in a drawer turned out to be the most important node in the
system. Use what you have, make it work well within those constraints, and upgrade
when stability justifies it.

### Clean layer over raw data — no cleanup required

You do not need to organize your existing data to use it. AiMe builds an analytical
layer on top of data where it lives — emails stay in the email client, financial
records stay in the accounting software, photos stay in cloud storage. Old emails,
duplicate photos, years of unorganized files — all become searchable and queryable
without touching a single one of them. The mess is fine. Cleanup becomes optional,
not prerequisite.

---

## Current State

The infrastructure is built and running. The RAG pipeline and AI triage layer are
designed but not yet implemented. An external AI (Claude, policy-gated) currently
serves as the reasoning layer for planning and non-sensitive tasks.

| Layer | What it is | Status |
|---|---|---|
| Data sources | Banks, health devices, email, calendar, photos | 🔧 Partial — manual ingestion today |
| Collection perimeter | relay (Pi), Kasa polling, Tailscale mesh | ✅ Running |
| Control plane | gateway (M1), Caddy, dashboard, shared scripts | ✅ Running |
| Analytical layers | Finance, GTD, Health, Travel, Media | 🔧 In progress — trackers built, pipelines not yet wired |
| Heavy compute | compute (MBP), on-demand inference | ✅ Infrastructure ready |
| Data servers | vault (Windows), MS Money, LlamaIndex, RAG | ❌ Offline — restore pending |

**What is running now:**
- Encrypted mesh network across all nodes with key expiry policy configured
- Raspberry Pi with hardware watchdog, thermal management, persistent journal logging
- Always-on gateway with reverse proxy, GTD dashboard, automated daily build pipeline
- Fully offline local AI fallback on travel node (DeepSeek R1 14B via Ollama)
- Rewards and credits tracker — persistent artifact, conversationally updatable
- Car maintenance dashboards — circuit breaker model for vehicle systems
- Strength training tracker — cycle logs, PR tracking, training max progression
- Historical chat export parser — bulk import of past conversations for RAG ingestion
- Manual routine system with automation targets mapped across every cadence
- Routine overhead dashboard — monthly cognitive load before and after automation

**What is being built next:**
- Pushover confirmation loop — proving the confirm → execute architecture end to end
- iMessage gateway — route questions to local AI models via text message
- RAG pipeline — LlamaIndex over email, financial records, health data, calendar
- Automated sleep and recovery scoring from device APIs

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

---

## For Builders

I started thinking about this project about a year ago. I didn't actually begin
building anything until around Q4 2025 and since then, I've been working on it on
and off as I've been able to find time and energy to continue. The project started in
ChatGPT, where several hundred conversations worth of architecture decisions and
design tradeoffs accumulated. It moved to Claude as the work became more structured.
The `chatgpt-parser.html` tool was built specifically to preserve that history and
prepare it for eventual RAG ingestion — so no conversation is lost regardless of
which platform it happened on. Ironically, a system designed to reclaim time takes
time to build. AiMe will eventually help reconstruct exactly when and how it came
together — which is one of the use cases you read about above.

This project is meant to be a blueprint, not a product. There is no hosted version,
no subscription, no vendor. Everything here runs on hardware I own, under my control.
My goal is to show that this kind of system is buildable — and to document it well
enough that others can build their own without starting from scratch. Fork it, adapt
it, make it yours. It is free, and intended to stay that way. For anyone who finds
value in it and wants to contribute back, a donation option will be available.

One honest caveat: this is not plug-and-play. It took real time, real decisions, and
a willingness to break things and figure out why. AI-assisted tools like Claude make
it dramatically more accessible than it would have been a few years ago — that is how
much of this got built. But accessible is not the same as risk-free. AI can produce
code that runs, looks right, and contains problems you will not catch unless you know
what questions to ask. If you are building something that touches your personal data
or runs on your home network, understand what you are deploying. Ask questions.
Verify. The architecture in these docs is built with that habit in mind. Bring the
same habit to your own build.

---

*Last updated: 2026-05-03 15:37 ET*
