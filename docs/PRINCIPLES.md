# AiMe — Principles

*These aren't rules invented for this project. They're patterns that emerged from building it — things that turned out to be true in practice, not just in theory. Some come from power systems engineering. Some come from getting things wrong first.*

*As I continue to build, I come back to these principles to update them and to remind myself why I'm doing this in the first place — because on a project of this scale it's easy to get caught up in the details and lose sight of the bigger picture. I'm hoping these principles resonate with those who want to embark on something similar, and serve as a starting point for developing their own.*

*These principles are themselves subject to revision. A principle that stops being true in practice should be updated or removed, not defended.*

---

## On Your Data

**Your data is only yours if it lives on your machine.**
Every cloud service that holds your data can change its terms, get acquired, get breached, or simply decide to do something different with it. The only meaningful guarantee of data ownership is physical custody. If your private data lives on your hardware, you control it. If it lives on someone else's server, you're borrowing access.

**The most sensitive data is the most useful data.**
Health records, financial history, message content, location patterns — this is the data that would actually improve your life if an AI could reason over it. It's also the data no cloud service should have. Local AI makes it possible to have both: the full power of AI reasoning over your most personal data, without giving that data to anyone else.

**Your data doesn't need to be organized to be useful.**
The impulse to "clean up first" is one of the biggest blockers to getting value from personal data. AiMe builds a clean searchable layer on top of whatever mess exists. Old emails in a folder you haven't opened in years, duplicate photos across three devices, financial records in three different formats — all of it becomes queryable without touching a single file. Start where you are.

**Never delete — archive.**
Deletion creates permanent uncertainty: "did I delete the right thing? What if I need that later?" Archiving eliminates the uncertainty. Everything is retrievable. The analytical layer just stops looking at archived items by default. The fear of "what if I lose that" is a structural problem with deletion as a design choice, not a personal failing.

**Derived data inherits the sensitivity of its inputs.**
If you combine public information with even one piece of sensitive personal data — location, health, financial history — the result is sensitive. This is the aggregation problem: innocuous pieces combine into a fingerprint. The rule: the output of any analysis is at least as sensitive as the most sensitive input. Build pipelines with this in mind from the start.

---

## On Privacy

**Privacy is about appropriate access, not secrecy.**
Private data isn't shameful data. It's data that belongs in some contexts and not others. Your medical history is appropriate for your doctor. Your financial records are appropriate for your accountant. Your location at 11pm is appropriate for your family. None of these belong on an advertising server. Privacy is about routing data to the right places, not about hiding things.

**Security through architecture is more reliable than security through encryption alone.**
Encryption protects data in transit and at rest. Architecture determines whether the data needs to travel or be stored externally at all. A system designed so that sensitive data never leaves your network doesn't need to depend on encryption being unbroken — the data simply isn't reachable. The best defense is not needing a defense.

**The powered-off drive is the most secure one.**
One of the most effective security measures in AiMe is an archive drive that's off by default. An attacker who doesn't know it exists can't reach it. Powering it on requires a deliberate action in a system the attacker would also need to compromise. This isn't obscurity as a substitute for security — it's a structural layer that makes the attack sequence harder. Real security uses multiple layers, and some of those layers can be physical.

**Install as little as possible.**
Every software package installed is a potential attack surface, a future compatibility problem, and something that needs to be maintained. The discipline: install only what's genuinely needed, verify what you're installing before you install it, and remove what's no longer used. Open-source model weights hosted locally carry no ongoing exposure — the risk is in packages that reach outward, not weights that sit inert. Prefer solutions built on what's already present over solutions that require new dependencies.

**Notifications should carry signals, not data.**
When the system sends you a push notification, it sends a signal — "something needs your attention" — and a link back to your private network where the actual content lives. The notification service never sees what the notification is about. This matters because notification payloads pass through external servers. Keep the personal content off those servers structurally.

---

## On AI

**AI is the reasoning layer. Scripts are the execution layer. You are the decision layer.**
These three roles need to stay separate. AI is good at reasoning over complex or ambiguous situations and recommending a course of action. Scripts are good at executing defined tasks reliably and repeatably. Humans are good at making consequential decisions and bearing responsibility for them. Mixing these roles creates systems where it's unclear who — or what — is actually in charge.

**Local AI first. External AI as last resort.**
For anything involving personal data, local models running on your own hardware are the correct default. They're slower and less capable than the best cloud models. That's a tradeoff worth making for the data privacy guarantee. External AI models serve a role — complex reasoning, open-ended synthesis, situations where local model capability isn't sufficient — but they should be the exception, not the default.

**The data never goes to the model. The model comes to the data.**
Cloud AI services work by sending your data to their servers where the model runs. Local AI inverts this: the model runs on your hardware, where the data already lives. This isn't just a privacy benefit — it changes what's possible. You can ask questions about data you'd never send to a cloud service.

**Weights local, API never.**
Open-source AI models can be downloaded and run locally. This is entirely different from using the same company's API, which routes your data through their servers. A model whose weights live on your hardware is yours. A model running on someone else's server is a service you're borrowing. These are not the same thing, even if the model is technically the same.

**AI should recommend, not act.**
An AI that takes actions autonomously on your behalf has a blast radius — the scope of what can go wrong. Keeping AI in a recommendation role and requiring human confirmation for any consequential action bounds that blast radius. You can always override a recommendation. An action that's already been taken is harder to undo. The confirmation step is not friction; it's a feature.

**Only automate what you've proven manually first.**
An automated process you don't understand is a black box that will fail in ways you can't diagnose. The manual version is also the fallback when automation fails. The correct sequence: do it manually until you understand it, then automate it, then verify the automation matches the manual process. Automating something you've never done yourself creates an undebuggable system.

---

## On System Design

**Name things for their actual role.**
A node called "relay" is a relay. A node called "gateway" is a gateway. A node called "vault" holds things securely. Names that reflect the role survive hardware swaps and architecture changes. Names that reflect the hardware become lies the moment the hardware changes. Accurate naming reduces the mental overhead of working with a system.

**One source of truth per piece of information.**
When the same information lives in two places, the two places diverge. Every time. Which one is right? Now you have a meta-problem on top of the original problem. Pick one home for each piece of data and make everything else a pointer to it.

**Design for the failure modes, not just the happy path.**
Every component fails eventually. The question is whether the failure is recoverable, whether it's detectable, and how much it affects everything else. A system designed for the happy path falls over completely when anything goes wrong. A system designed around failure modes degrades gracefully and recovers cleanly.

**Eliminate constraints through architecture, not through careful procedure.**
When a process requires executing steps in a specific order to avoid a failure, the right fix is usually to redesign the system so the failure mode can't occur — not to add better instructions for the order. Careful procedures get forgotten. Architecture changes are permanent.

**Gray means unknown. Green means verified.**
Status indicators that default to green when data is missing are actively dangerous. An unknown state is not a good state. Every dashboard and status table should distinguish between "known good," "known bad," and "unknown." Unknown is always displayed in gray. Only confirmed good states get green.

**Clean up before restoring, not after.**
When something is already broken and needs fixing, that's the right time to do the cleanup work that's been accumulating. Use your outages.

---

## On Working With AI

**Explicit context beats implicit memory.**
The most reliable way to work with an AI assistant isn't to rely on it remembering things across sessions — it's to load the relevant context explicitly at the start of each session. This is more reliable, more auditable, and more portable across different AI tools. The intelligence lives in the documentation, not in the AI's memory.

**The best mental model is the one you already know.**
Abstract systems become concrete when explained in vocabulary you already use. A power systems engineer understands "AI as protection relay, scripts as circuit breakers, human as operator" immediately. The goal is mapping new concepts to existing expertise, not replacing that expertise with new vocabulary. Whatever your background, that vocabulary is the one that makes abstract architecture concrete.

**Document the decisions, not just the code.**
Code tells you what the system does. Documentation tells you why it does it that way and what was considered and rejected. When something breaks or needs to change, the context for the original decision is the most valuable thing you can have.

**Trust but verify. Always.**
An AI can be confidently wrong. Before acting on anything an AI tells you about the state of a system, run a read-only check. The runtime is ground truth. The AI is a thinking partner, not an oracle.

**A long streak is harder to break than willpower.**
Consistency in maintenance doesn't come from discipline. It comes from systems that make the consistent behavior the path of least resistance and make the inconsistent behavior visible. Streak counters, commit histories, status dashboards — these create accountability without requiring ongoing motivation.

---

## On Process

**Proactive beats reactive — surface things before you ask.**
The goal isn't a better search tool. It's a system that watches what's happening and tells you what's relevant before you think to look. Design every alert and automation around the question: "when would this information be useful?" not "how can someone find this if they look?"

**Log by exception. Notify by exception.**
A system that surfaces everything surfaces nothing. Logs should capture the full record — every event, every state change, every heartbeat. Notifications should carry only what actually needs human attention. Write everything to the log; alert only when something crosses a threshold that warrants action. This is not in conflict with wanting to verify things. Verification is available on demand via the log. Notification is reserved for genuine signals.

**Trust the system by default. Verify when you need to.**
These are two modes of the same design, not a contradiction. In normal operation, you trust the system — the dashboard is green, things fired as scheduled, no alerts. When something feels off, the full record is there: logs, timestamps, status indicators, diffs. The system is designed to be audited. You just don't have to audit it continuously. Trust is the default mode. Verify is the access mode.

**Start conservative. Iterate toward what you actually want.**
You won't know what you really want until you see it working. A conservative first version that does less is easier to extend than an ambitious first version that does too much wrong. The correct sequence: build the minimal version that proves the concept, use it long enough to know what's actually missing, then add what's genuinely needed.

**Document why you ruled something out.**
Decisions to *not* do something are the ones most likely to get relitigated. Six months later, you won't remember why you decided against a particular approach — you'll just see the gap and start exploring the same options again. Write down what you considered, what you tried, and why you stopped. The absence of a feature is a decision, not an oversight. Treat it as one.

**Plan before building. Always.**
Starting without defined names, structures, or documentation creates technical debt that costs five to ten times as much to clean up as it would have cost to design upfront. Thirty minutes of design prevents weeks of cleanup.

**Prove it small before scaling it.**
Build the simplest version that demonstrates the concept works. If it doesn't work at small scale, it definitely won't work at large scale. If it does work, you know exactly what you're scaling.

**Broken state is diagnostic data.**
When something breaks, the break tells you something true about how the system actually works versus how you thought it worked. Read the break first. Fix it second.

**Fun is a sustainability requirement, not a luxury.**
A multi-year solo project only gets finished if you're still working on it in year two. Quick wins, interesting tangents, and engaging problems that aren't the most critical thing to build — these aren't distractions. They're what keeps a long project alive between the hard sessions.

**Good enough now beats perfect never.**
The first version of anything will be wrong in some way. You won't know how until you see it working. Ship the version that works, observe how you actually use it, then refine.

---

*Last updated: 2026-05-31 · Concepts and design by Andrew Tan · Written with help from Claude*
