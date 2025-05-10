## Chronologue Python SDK 

Chronologue is a memory-centric agent runtime built around integrating time as core to orchestrating and scheduling agentic behavior.

We treat the calendar not just as a tool for scheduling—but as a **control surface** for directing agents to take actions at specified times, location, and duration. With Chronologue, users and developers can program and coordinate agent behavior, steer execution with memory, and audit agent performance with structured profiling.


Chronologue enables: 

- Structured agent planning (`agent_planning`)
- Composable, taggable memory (`memory_tagging`)
- Temporal execution and profiling (`executed_at`, `deviation_ms`)
- Feedback-driven improvement (`feedback_score`)
- Portable context for LLMs, agents, and teams

### Core Concepts 


#### Memory Traces 

Every agent action, user reflection, or event is stored as a `memory_trace`, with metadata such as:
- `type`: goal, reflection, observation, calendar_event, agent_plan
- `timestamp`, `content`, `tags`
- Optional: `profiling` object

#### Tempo Tokens

Time-anchored tokens (e.g., `<tempo:SundayEvening>`) help cluster and align agent behavior to user intent.

#### Memory Tags

Semantic and time-based labels (`#deep_work`, `#q2_review`, `#5-8_notes`, `#July_travel_itenary`) used for:

- Prompt filtering
- Memory clustering
- Multi-agent sharing

#### Profiling 

Execution traces include:
- `executed_at`, `duration_ms`, `deviation_ms`
- `tempo_alignment`, `feedback_score`

#### Retrieval Augmented Planning 

Use memory traces filtered by tags or tempo tokens to shape agent behavior in planning and scheduling.

Agents propose actions as structured plans:
- `action_type`, `scheduled_for`, `status`, `origin`
- Routed through the planner, executor, and profiler

---

## Getting Started 

1. Clone the repository: 

```
git clone https://github.com/dr2633/chronologue-sdk.git
cd chronologue-sdk
```


2. Install backend dependencies:

```
pip install -r requirements.txt
```

3. Start the API Server: 

```
uvicorn api.main:app --reload
```

4. Launch frontend: 

```
cd frontend
npm install 
npm run dev
```

---

### Tagging System 


- All traces support a `tags` field (`List[str]`)
- Tags can be added manually or suggested by agents
- Chat prompts can include `#hashtags` to filter memory
- API endpoints:
  - `GET /tags`
  - `POST /memory/:id/tags`
  - `GET /memory?tags=deep_work+q1_review`

--- 

### Agent Runtime 

The Chronologue runtime consists of: 

- **Planner**: receives validated `agent_plan` input
- **Scheduler**: places tasks into time-aware queues
- **Executor**: performs the action, updates `status`, logs execution
- **Profiler**: records latency, alignment, feedback

Execution flow:

1. User or LLM proposes plan
2. Plan enters planner queue
3. On scheduled time, executor runs task
4. Profiling metadata is stored
5. Feedback is attached as memory

### Memory API 

- `POST /memory` — Create trace
- `GET /memory` — Filter by tags, type, range
- `PATCH /memory/:id/tags` — Add or update tags
- `GET /memory/export` — Download traces as JSON, Markdown, or ICS

### Frontend 


Implemented in React + Tailwind:

- **AgentQueuePanel** — Review and approve plans
- **TagAutocomplete** — `#`-triggered input completion
- **FeedbackModal** — Post-execution review
- **ProfilerTimeline** — Visualize execution behavior over time


### Datasets and Evaluation 

The `datasets/` directory contains:
- Synthetic planning traces
- Profiling examples (aligned, misaligned, feedback-tagged)
- Templates for exporting and testing context injection

You can generate your own datasets by:
- Simulating agent runs
- Logging execution to memory
- Exporting via `/memory/export`

--- 

### Extending and Building with Chronologue 

Chronologue is built to scale:

- Add new agent `action_type`s
- Extend tempo token grammar
- Build team memory scopes and tag namespaces
- Integrate with external LLMs via planning APIs

Future directions:
- Vector store integration
- Reinforcement feedback modeling
- Multi-agent simulation via shared memory and calendar

--- 

### Guidelines:
- Use Pydantic for all schemas
- Use FastAPI for backend endpoints
- Keep memory trace mutations versioned
- Add tests for trace resolution and prompt parsing


---

## 📄 License

Apache License © 2025 Chronologue

---

Chronologue turns time, memory, and intent into structured and sharable infrastructure — for users, agents, and systems that need to reason and act with precision. Build with it. Schedule with it. Collaborate and share. 

