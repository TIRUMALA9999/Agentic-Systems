# Agentic-Systems (Portfolio) — Agentic AI Workflows with CrewAI (Flows • Memory • Tools • Knowledge)

**Target audience:** Recruiters • Hiring managers  
**Positioning:** Interview‑explainable, ATS‑friendly portfolio repo demonstrating **agentic system design** using **CrewAI**, **CrewAI Flows**, **tool/knowledge integration**, and **memory** patterns.

---

## 1) What this repo demonstrates (resume-focused)

This repository contains a set of practical, hands-on experiments that showcase how to build **LLM-powered agents** and **multi-step workflows** with:

- **Multi-agent orchestration** (Research → Summarize → Fact-check) using **CrewAI**
- **Flow-based execution** using **CrewAI Flow** (`@start`, `@listen`, branching with `or_`)
- **Agent memory** inspection (short-term, long-term, entity memory)
- **Custom knowledge source** pattern (fetching external data and grounding agent responses)
- **Tooling integration** (web search via **SerperDevTool**, content extraction via **Firecrawl**, local inference via **Ollama**)
- **Config-driven agent/task definitions** via YAML

**ATS keywords:** Agentic AI, LLM agents, multi-agent systems, workflow orchestration, tool calling, retrieval/grounding, memory, CrewAI, LlamaIndex, OpenAI API, Ollama, YAML configuration, Python, notebooks.

---

## 2) High-level architecture (how to explain in an interview)

### A) Research Crew (multi-agent pipeline)
**Goal:** Produce a verified research summary for a topic.

**Flow (sequential):**
1. **Research Agent** → gathers sources using web search tool  
2. **Summarization Agent** → distills findings into structured summary  
3. **Fact Checker Agent** → verifies claims and reduces hallucinations

This pattern mirrors production agent stacks where **tool-augmented research** is separated from **synthesis** and **verification**.

### B) Flow Orchestration (CrewAI Flow)
**Goal:** Show how to build stateful, event-driven workflows.

- Uses `Flow` with `@start()` entrypoints and `@listen()` to chain steps.
- Demonstrates branching / routing patterns (e.g., ticket routing).
- Includes an example of **OpenAI + Ollama** in a single flow (cloud + local fallback concept).

### C) Memory & Knowledge
- **Memory_Demo** explores how CrewAI stores and retrieves:
  - short-term memory
  - long-term memory
  - entity memory
- **custom_knowledge_source** shows how to inject external data into the agent context via a `BaseKnowledgeSource` implementation.

---

## 3) Repository map

```
Agentic-Systems-main/
├─ 1.ipynb                          # LlamaIndex OpenAI call + early CrewAI examples
├─ 2.ipynb                          # Multi-agent research/summarize/fact-check (inline)
├─ 3.ipynb                          # Config-driven version using config.yaml
├─ config.yaml                       # Agent/task definitions (template-style)
├─ output.md                         # Example generated output (agent-produced content)
│
├─ project/
│  ├─ research_crew.py               # CrewBase class for research pipeline
│  ├─ research_crew.ipynb            # Run the ResearchCrew end-to-end
│  └─ config/
│     ├─ agents.yaml                 # Agent roles/goals/backstories
│     └─ tasks.yaml                  # Task descriptions + expected outputs
│
├─ Flows/
│  ├─ AI-Agents-crash-course-Part-3.ipynb  # Flow patterns + OpenAI + Ollama + CLI scaffold
│  ├─ practice.ipynb                 # (Empty placeholder in this snapshot)
│  ├─ test_flow/                     # `crewai create flow` scaffold + PoemCrew example
│  │  ├─ README.md
│  │  ├─ pyproject.toml
│  │  └─ src/test_flow/
│  │     ├─ main.py                  # Flow kickoff scaffold (template sections)
│  │     ├─ crews/poem_crew/          # CrewBase for poem writing (config-driven)
│  │     └─ tools/custom_tool.py      # Example CrewAI BaseTool implementation
│  │
│  └─ social_media_content_writer/   # Planner-style agent configs + assets + sample output
│     ├─ config/ (planner_agents.yaml, planner_tasks.yaml)
│     ├─ assets/ (sample LinkedIn + Threads writing styles, source markdown)
│     └─ output/draft.json
│
├─ Memory_Demo/
│  └─ memory.ipynb                   # Inspect CrewAI memory objects + searches
│
└─ custom_knowledge_source/
   └─ weather_knowledge_source.ipynb # Knowledge source pattern (Open-Meteo API)
```

> **Note:** Some YAML/Python/notebook files contain literal `...` placeholders (template sections). The `project/config/*.yaml` files are complete and runnable; some other configs are intended as partially-filled examples.

---

## 4) Tech stack

- **Python**
- **CrewAI** (agents, crews, tasks, sequential process)
- **CrewAI Flow** (workflow orchestration)
- **crewai-tools**
  - `SerperDevTool` (web search)
- **LlamaIndex** (`llama_index.llms.openai`) for LLM calls
- **OpenAI API** (example uses `gpt-5-mini` in notebooks)
- **Ollama** (local model example: `llama3.2:1b`)
- **Firecrawl** (content extraction; used in social media writer setup notes)
- **requests** (external API calls)
- **YAML** configs for agent/task definitions
- **Jupyter Notebooks** for reproducible experiments

---

## 5) Setup (run it locally)

### A) Create environment
```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate
```

### B) Install dependencies
There is no single pinned `requirements.txt` in this snapshot. Install the core packages used across notebooks:

```bash
pip install crewai crewai-tools llama-index openai python-dotenv pyyaml requests nest-asyncio ollama firecrawl-py html2text
```

> If you want this repo to look **production-ready to recruiters**, add a `requirements.txt` (or `pyproject.toml`) at the root with pinned versions.

### C) Environment variables
Create a `.env` file in the repo root:

```env
OPENAI_API_KEY=...
SERPER_API_KEY=...
FIRECRAWL_API_KEY=...
```

- `SERPER_API_KEY` is required for `SerperDevTool`
- `FIRECRAWL_API_KEY` is used by the social-media content workflow (if you run it)

---

## 6) How to run the demos

### A) Run the ResearchCrew (most recruiter-relevant demo)
1. Open `project/research_crew.ipynb`
2. Run all cells
3. It loads `project/config/agents.yaml` and `project/config/tasks.yaml`
4. Executes a **sequential** research → summarize → fact-check pipeline.

### B) Run the flow crash-course notebook
Open:
- `Flows/AI-Agents-crash-course-Part-3.ipynb`

It demonstrates:
- `Flow` patterns (`@start`, `@listen`)
- OpenAI + Ollama usage in a flow
- Routing example (ticket triage)
- Creating a flow scaffold via CLI (`crewai create flow test_flow`)

### C) Run the `test_flow` scaffold (CLI-style)
```bash
cd Flows/test_flow
python -m test_flow.main
```

This folder includes:
- a config-driven `PoemCrew`
- a sample custom tool (`MyCustomTool`)

### D) Memory demo
Open:
- `Memory_Demo/memory.ipynb`

This notebook shows how to:
- create a `Crew`
- run a task
- inspect `crew._short_term_memory`, `crew._long_term_memory`, and entity memory search behavior

### E) Custom knowledge source demo
Open:
- `custom_knowledge_source/weather_knowledge_source.ipynb`

Demonstrates a `BaseKnowledgeSource` implementation that fetches weather data from **Open-Meteo** and uses it to ground the agent’s output.

---

## 7) Results / artifacts

- `output.md` contains sample generated content (agent-produced summary about agentic systems).
- `Flows/social_media_content_writer/output/draft.json` shows a sample draft artifact produced by the content workflow.

---

## 8) Interview talking points (use these verbatim)

- “I separated the pipeline into **research**, **summarization**, and **fact-checking** to reduce hallucinations and make responsibilities clear.”
- “I used **tool-augmented agents** (Serper web search) so the system can fetch **up-to-date sources** instead of relying on static training knowledge.”
- “I explored **CrewAI Flows** to model workflows as **event-driven graphs**, which is closer to production orchestration than a single prompt chain.”
- “I inspected memory objects to understand how **state and recall** can improve agent continuity across turns and tasks.”
- “I implemented a **custom knowledge source** so agents can be grounded in external APIs/data feeds.”

---

## 9) Roadmap (to make it even more recruiter-ready)

- [ ] Add **root** `requirements.txt` with pinned versions
- [ ] Add `.env.example` (no secrets) + setup instructions
- [ ] Replace template `...` placeholders with complete configs or remove them
- [ ] Add a small CLI entrypoint, e.g. `python -m project.run --topic "..." `
- [ ] Add tests for knowledge source + task wiring
- [ ] Add GitHub Actions for linting and a notebook smoke test

---

## Author

**Tirumala Teja Yegineni**  
GitHub: https://github.com/TIRUMALA9999
