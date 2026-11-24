# Harness Engineering & Agent Orchestration

> Stop building scripts. Start building durable multi-agent systems.

An infrastructure layer around an LLM — the **harness** — that
makes agents survive production. Move past basic while-loops and API wrappers and learn the
patterns that keep agents durable, isolated, memory-aware, and coordinated.




## Setup

### 1. Clone and install

```bash
git clone <this repo url>
cd harness-engineering
npm install
```

### 2. Configure environment variables

Copy `.dev.vars.example` to `.dev.vars` and fill in your keys. An OpenAI API key is the only
hard requirement; individual lessons note any extra services they need.

```
OPENAI_API_KEY=sk-...
```

### 3. Run things

```bash
npm run dev    # start the app: harness server (:8787) + inspector UI (:5173)
npm run docs   # serve the lesson notes with VitePress
npm run typecheck
```

`npm run dev` boots the **Harness Inspector** — a chat pane on the left and a live
event-stream pane on the right. Out of the box the agent is a stub: submit a task and
you'll see the harness emit `workflow.started` → a "no agent yet" log → `workflow.completed`.
You build the real (brittle) agent loop in Lesson 1.


## Tech stack

- **Runtime:** Node.js + TypeScript, run with `tsx` (no build step for the server).
- **Server:** Express + `ws` — hosts the harness and streams its event log to the browser over one WebSocket.
- **LLM:** OpenAI (GPT-5.5) via the Vercel AI SDK (server-side only; the harness owns the transport).
- **UI:** Vite + React, styled with prompt-kit (shadcn/ui + Tailwind). The inspector renders the harness event stream; **students don't build the UI.**
- **Notes:** VitePress.
- Libraries for durable execution, sandboxing, and state are introduced per lesson.

