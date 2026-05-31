# AI Model Comparison — Claude, ChatGPT, and Local Models
*Part of the AiMe project documentation · Last reviewed May 2026*
*Written with help from Claude*

---

## Table of Contents
1. [Quick Comparison](#quick-comparison)
2. [Why Claude for AiMe](#why-claude-for-aime)
3. [Where ChatGPT Has the Edge](#where-chatgpt-has-the-edge)
4. [Desktop Apps and Browser-Based Access](#desktop-apps-and-browser-based-access)
5. [Pricing and Deadlines](#pricing-and-deadlines)
6. [Local Models — Why They're Non-Negotiable](#local-models--why-theyre-non-negotiable)
7. [Most of AiMe Doesn't Need AI at All](#most-of-aime-doesnt-need-ai-at-all)
8. [Portability — Any AI Can Read the System](#portability--any-ai-can-read-the-system)
9. [Future: Gemini and Other Models](#future-gemini-and-other-models)
10. [Creating Presentations from This Doc](#creating-presentations-from-this-doc)
11. [Choosing the Right Model](#choosing-the-right-model)

---

*Note: This comparison covers the web-based interfaces for Claude and ChatGPT — the chat products you use in a browser. Both companies also offer agentic tools for automated coding and file operations; those are covered separately in the [Desktop Apps and Browser-Based Access](#desktop-apps-and-browser-based-access) section. The ChatGPT column reflects documented capabilities as of mid-2026; Claude has been the primary tool used throughout AiMe's build and the comparison is based on that experience.*

## Quick Comparison

| Feature | Claude (Anthropic) | ChatGPT (OpenAI) | Local (self-hosted) |
|---|---|---|---|
| **Context window** | 200K words of input — large enough to hold all four master files simultaneously | ~128K (varies by plan) | 32–65K depending on model |
| **Context handling** | Explicit signal when full; structured handoff strategy possible | Silently forgets early context with no signal | Hard limit; no signal |
| **Project files** | Shared across all chats in a project — true multi-session reference | Per-chat by default; Projects add some persistence | No projects concept; single session only |
| **Project-specific behavior** | Full custom instructions per project (AiMe project behaves differently than a health or finance project) | Global custom instructions only — not per-topic | Fixed at model creation time |
| **Persistent documents** | Artifacts — downloadable, updatable files created during conversation | Canvas — similar, less mature | Not available |
| **Usage limits** | Visible daily message limits — can interrupt long sessions | Higher thresholds; rarely hit | No limits whatsoever |
| **Data privacy** | Data sent to Anthropic's servers | Data sent to OpenAI's servers | 100% local — nothing leaves your network |
| **Monthly cost** | ~$20/month | ~$20/month | One-time hardware cost only |
| **Image generation** | No | Yes (built-in) | Yes (via separate local tools) |
| **Code execution** | Runs HTML and JavaScript in browser; cannot run Python or shell | Runs Python server-side in a sandboxed environment | No built-in execution |
| **Web search** | Yes (optional) | Yes (optional) | No |
| **Conservatism** | More cautious; surfaces uncertainty; pushes back on risky actions | More permissive; executes faster but with less friction | Varies by model |
| **Following long instructions** | Excellent for multi-step operational workflows | Good; can drift on very long instruction sets | Good for focused tasks; weaker on complex chains |
| **Performance in long sessions** | Can slow down as context window fills — a signal to open a continuation chat | Generally stable | Generally stable within context limits |

---

## Why Claude for Building AiMe

The following are specific reasons Claude has worked well for the AiMe build — not a general endorsement. Your experience building something different may lead to different conclusions.

### 1. The context window is large enough to hold the whole system

The four master files that describe AiMe's current state consume roughly a third of Claude's 200K-word context window. That's a lot — but it means Claude can read the full architecture, the current break state, the planned work, and the operating procedures simultaneously before proposing anything. Every session starts from a complete picture.

Local models typically offer 32–65K words of context. That's often not enough to hold all four master files at once, which means working with partial context or summarizing aggressively. This is the single biggest practical advantage of cloud models for complex, long-running builds.

### 2. The context limit is honest

Claude signals when a conversation is getting full — and noticeably slows down before it hits the limit. This is honest and manageable. The AiMe workflow responds with a "running checkpoint" strategy: at every major phase, Claude updates a ready-to-paste summary. If context runs out, paste that summary into a new chat and continue — clean handoff, no lost work.

ChatGPT's approach is "graceful degradation": the conversation continues but earlier context quietly disappears. You never know what's been forgotten. For work where a decision made two hours ago still matters, silent forgetting is worse than an explicit limit.

### 3. Different rules for different topics

Claude lets you configure each project independently. The AiMe build project behaves differently than a health project, a finance project, or a travel project — different instructions, different defaults, different behaviors. This matters because AiMe spans many sensitive domains and each deserves its own handling rules.

ChatGPT's custom instructions are global — one setting applies everywhere.

### 4. Artifacts survive the session

Claude creates persistent, downloadable documents during conversations — code files, session summaries, reference tables, planning documents. These can be updated in place as the conversation evolves. The session summary artifact is what gets uploaded to the project at the end of every build session, preserving the decision record.

### 5. Pushback is a feature

Claude will flag when something seems risky, ask clarifying questions, and push back on approaches that conflict with established principles. For infrastructure work — running commands on always-on servers, editing production scripts, making architectural decisions — a model that says "are you sure?" is genuinely useful. Mistakes in this context are hard to undo.

### 6. An unexpected benefit: domain-specific explanation

One discovery during the build: Claude can be instructed to explain architectural concepts using the vocabulary from a specific field. For a power systems engineer, "AI as protection relay, scripts as circuit breakers, human as operator" immediately maps a complex new concept onto existing expertise. This isn't a standard feature — it's a result of how the session instructions were written — but it made a real difference in how quickly design decisions landed.

---

## Where ChatGPT Has the Edge

*Based on documented capabilities — Claude has been the primary tool used throughout this build.*

### 1. No visible usage limits
On ChatGPT's paid plan, you can work through long sessions without hitting daily rate limits. Claude's limits are real and can interrupt flow on high-output days. This is the most practically significant difference for intensive building sessions.

### 2. Image generation built in
ChatGPT can generate images directly in the conversation. Claude cannot. For visual work — mockups, illustrations, diagrams — ChatGPT has a clear advantage.

### 3. Python code execution
ChatGPT can run Python inside the conversation. You can upload a spreadsheet and ask for analysis; ChatGPT runs the code and shows you results. Claude can write the code but cannot run it.

For AiMe specifically, running code on the home server against real data is the better approach anyway — it has real file access, no sandbox limitations, and stays on private infrastructure. But for quick analysis tasks without a local setup, ChatGPT's execution environment is useful.

### 4. Lower friction for casual use
The AiMe workflow requires maintaining operating documents, following a session ritual, and managing parallel conversations. This is by design — it reflects how the builder thinks and what makes the system work. For someone who wants quick answers without maintaining infrastructure documentation, ChatGPT's more forgiving approach feels more natural.

---

## Desktop Apps and Browser-Based Access

Both Claude and ChatGPT offer desktop applications in addition to browser access. AiMe uses the browser-based version only.

**Why browser-based:** Desktop applications request deeper system access — file system permissions, background processes, operating system integrations. For a system designed around data sovereignty and controlled outgoing connections, granting an AI application broad local access contradicts the architecture. The browser version provides all the capability needed for building and conversation work without additional access grants.

**Agentic coding tools:** Both Anthropic and OpenAI offer terminal-based tools for automated coding — they can read and write files, run commands, and execute multi-step changes directly. These are powerful but route work through external servers. For AiMe's private data, this isn't appropriate. The equivalent capability is built directly into the local infrastructure using scripts and the home server's own API.

---

## Pricing and Deadlines

| | Claude | ChatGPT |
|---|---|---|
| **Monthly** | ~$20/month | ~$20/month |
| **Annual** | Not currently using | ~$200/year |
| **Local models** | Hardware cost only (one-time) | Not available |

**On annual subscriptions:** An annual ChatGPT subscription that auto-renews is worth auditing — if local models cover most of the use cases and Claude handles the rest, the case for a third paid subscription gets thin. Always export conversation history before cancelling any AI service.

**Financial reality of the build phase:** Maintaining consistent AI access during active building runs ~$20–40/month in subscription costs. Once the local inference pipeline is fully operational, the majority of day-to-day queries shift to local models — no per-session cost, no usage limits, just the electricity draw of hardware that's already running for other purposes.

---

## Local Models — Why They're Non-Negotiable

Local inference means the AI runs entirely on your own hardware. Nothing leaves the network. This isn't a backup option or a cost-saving measure — for personal data, it's the only legitimate option.

**What local models unlock:**
- **Sensitive personal data** — health records, financial details, message content, location history cannot go to an external server. Local models handle this without restriction or data policy review.
- **No usage limits** — the message routing service that checks for new texts needs to call an AI many times per day. A cloud API call on every message would be expensive and slow. Local models handle this continuously at no marginal cost.
- **No API costs** — calling a cloud AI API charges per use. Beyond a certain volume, local inference is dramatically cheaper. AiMe also routes certain queries through a locally-generated, sanitized prompt that gets pasted into Claude's web interface — avoiding API costs while still getting cloud-quality answers when needed.
- **Offline operation** — local inference works during travel, network outages, and without any internet connection. The travel laptop has a full AI model available with no network dependency.
- **Speed for simple tasks** — a small local model answering a quick question can be faster than a round-trip to a cloud service.

**Current local model performance** (measured on AiMe hardware):

| Setup | Speed | Best use |
|---|---|---|
| Small model, always-on (Apple M1, 8GB) | ~7 tokens/sec | Fast routing, basic questions |
| Mid model, travel node (Apple M3, 16GB) | ~10 tokens/sec | Best current interactive reasoning |
| Mid model, desktop (Intel, 32GB) | ~2 tokens/sec | Background analysis |
| Large model, desktop (Intel, 32GB) | ~1 token/sec | Deep synthesis, batch use |

The desktop here is a 2019 Intel laptop — older architecture, no Apple Silicon acceleration. The travel node runs the same models 4× faster. A newer always-on desktop (planned) would enable much larger models at higher speeds.

**The model weights used here are open source.** Downloading and running them locally carries no data exposure. The rule: use the weights on your own hardware, never call the model developer's external API. These are different products even when the underlying model is technically the same.

**Why cloud AI is still needed for some things:**
- **Context limits** — local models typically offer 32–65K words of context vs Claude's 200K. Holding all four master files simultaneously requires the larger window.
- **Complex reasoning** — large-scale architectural decisions, long document synthesis, and high-quality code generation at scale still benefit from the largest cloud models.
- **Speed** — at 1 token/second, a 2,000-word answer takes over 30 minutes on the desktop node. For anything time-sensitive, cloud models are faster until the hardware upgrade lands.

The target: sensitive personal data stays local always; infrastructure and design work uses cloud with sanitized inputs; the boundary is enforced by a deliberate data classification policy.

### A note on RAG

One of the more powerful applications of local AI is RAG — Retrieval Augmented Generation. The idea: instead of sending your documents to a cloud AI and asking questions, you index your documents locally, retrieve the most relevant sections for a given question, and feed only those sections to a local model for synthesis. The result: you can ask questions about thousands of pages of personal documents (emails, financial records, health history, notes) without any of that content leaving your network.

This is the next major layer being built for AiMe. The design is locked. The technical approach has been validated. It's the gateway to "ask anything about your own life and get a real answer from your own data."

---

## Most of AiMe Doesn't Need AI at All

This is worth stating clearly: the majority of AiMe's running infrastructure is just software.

The daily routines, scheduled checks, notification deliveries, data collection, and dashboard updates all run as scripts, system services, and background watchers. No AI involved. A small computer polls smart outlets every 60 seconds. An automated task checks sleep ring data every morning at 8am. The message listener watches for new texts and delivers responses. None of this requires language model inference — it requires well-written scripts and reliable scheduling.

AI is used heavily during the **building phase** — designing the system, writing the code, making architectural decisions. During **operation**, AI handles the tasks that genuinely require reasoning: interpreting ambiguous requests, synthesizing information across multiple sources, and making judgment calls that rules can't capture. Everything else runs deterministically.

The goal is not an AI-dependent system, but a system where AI handles the parts that benefit from it and gets out of the way for everything else.

---

## Portability — Any AI Can Read the System

One of the less obvious properties of this architecture is how portable it is across AI tools.

The system's state lives in four plain text files: what's been built, what's broken, what's planned, and how to work with it. Any AI model — Claude, ChatGPT, a local model, future tools not yet released — can read these files and understand the current state of the system. No proprietary memory format, no lock-in.

This means AiMe grows with AI capability improvements rather than depending on them. When a better local model is released, it plugs in. When a better cloud model is available, it reads the same files. The intelligence is in the documented system, not in any particular AI's memory.

---

## Future: Gemini and Other Models

**Gemini (Google):** Notable for a context window far larger than any other current model — useful for loading an entire email archive into a single session. Its deep integration with Google's products is relevant to email processing pipelines. Worth evaluating for specific use cases.

**On Gmail and Gemini:** If you already use Gmail, Google has your email data. Using Gemini to query that data doesn't expose the underlying emails further — Google already has them. What it does add is query intent: Google would also know what questions you're asking about your email, which reveals behavioral patterns and priorities. Whether that tradeoff is acceptable depends on what you're asking. Worth thinking through carefully before using for anything sensitive.

**Principles for evaluating any new model:**
- Does it support project-scoped context (not just global memory)?
- Can it consistently follow long, detailed operational instructions?
- Does it signal context limits explicitly or degrade silently?
- What is the data handling policy for the specific use case being considered?

The current approach: use Claude for building and design work, local models for personal data, other tools evaluated when a specific use case justifies it.

---

## Choosing the Right Model

| If you need to... | Use |
|---|---|
| Build infrastructure, make architectural decisions | Claude (web interface) |
| Process personal health, financial, or message data | Local only |
| Generate images or run quick data analysis | ChatGPT |
| Work offline or without internet | Local model on travel or desktop node |
| Handle very long documents or full system context | Claude or Gemini |
| Run scheduled tasks, automations, or recurring jobs | Scripts — no AI needed |
| Ask questions about your own documents and data | Local RAG pipeline (in progress) |
| Work with someone else's AiMe-style system | Read their master files — any AI model works |

### Known local models by use case

| Use case | Current approach |
|---|---|
| Quick iMessage responses | Small always-on model (7B class) |
| Interactive reasoning, analysis | Mid-size model on travel node (14B class) |
| Deep synthesis, complex code | Large model on desktop node (32B class) — slow |
| Personal document Q&A | Local RAG pipeline — design locked, building now |
| Image understanding and tagging | Not yet implemented — Session E (media pipeline) |