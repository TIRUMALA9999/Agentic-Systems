# Agentic-Systems — Agentic AI Workflows (CrewAI • Flows • Memory • Tools • Knowledge)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![CrewAI](https://img.shields.io/badge/CrewAI-Agents%20%26%20Flows-black)
![Notebook](https://img.shields.io/badge/Jupyter-Notebooks-orange)



This portfolio repository demonstrates practical **agentic system design** using **CrewAI** and **CrewAI Flows**: multi-agent orchestration, tool use (web search), memory behavior, and grounding via a custom knowledge source.

---

## Key highlights 

- Built a **3-agent research pipeline** (Research → Summarize → Fact-check) using **CrewAI** to improve reliability and reduce hallucinations.
- Implemented **Flow-based orchestration** using `Flow` with `@start`/`@listen` patterns (event-driven, stateful workflows).
- Explored **agent memory** (short-term, long-term, entity memory) to understand persistence and recall in multi-step tasks.
- Added a **custom knowledge source** (weather API) to ground agent outputs with real external data.

**Keywords:** Agentic AI, LLM agents, multi-agent systems, workflow orchestration, tool calling, grounding, memory, CrewAI, OpenAI API, Ollama, YAML configuration, Python.

---

## Repository map

```
Agentic-Systems-main/
├─ 1.ipynb                          # LlamaIndex OpenAI call + early CrewAI examples
├─ 2.ipynb                          # Multi-agent research/summarize/fact-check (inline)
├─ 3.ipynb                          # Config-driven version using config.yaml
├─ config.yaml                       # Template-style agent/task config
├─ output.md                         # Example generated output (artifact)
│
├─ project/
│  ├─ research_crew.py               # CrewBase class for research pipeline
│  ├─ research_crew.ipynb            # Run the ResearchCrew end-to-end
│  └─ config/
│     ├─ agents.yaml                 # Agent roles/goals/backstories
│     └─ tasks.yaml                  # Task descriptions + expected outputs
│
├─ Flows/
│  ├─ AI-Agents-crash-course-Part-3.ipynb  # Flow patterns + OpenAI + Ollama + routing
│  ├─ practice.ipynb                 # Empty placeholder in this snapshot
│  ├─ test_flow/                     # `crewai create flow` scaffold + PoemCrew example
│  └─ social_media_content_writer/   # Planner configs + style assets + draft output
│
├─ Memory_Demo/
│  └─ memory.ipynb                   # Inspect CrewAI memory objects + search behavior
│
└─ custom_knowledge_source/
   └─ weather_knowledge_source.ipynb # Knowledge source pattern (Open-Meteo API)
```

---

## How it works

### 1) Research Crew (multi-agent pipeline)
**Goal:** Produce a verified research summary for a topic.

1. **Research Agent** pulls sources via web search tooling  
2. **Summarization Agent** converts sources into a structured summary  
3. **Fact Checker Agent** verifies claims / reduces hallucinations  

This design matches real production stacks where responsibilities are separated for reliability and maintainability.

### 2) Orchestration with CrewAI Flows
**Goal:** Model workflows as event-driven graphs instead of a single prompt chain.

- `Flow` with `@start()` entrypoints and `@listen()` chaining
- Routing example (ticket triage)
- Cloud + local model concepts (OpenAI + Ollama example)

### 3) Memory + Knowledge grounding
- Memory notebook shows how short/long-term/entity memory can support continuity.
- Custom knowledge source notebook grounds responses with external API data.

---

## Quickstart (run locally)

### 1) Clone
```bash
git clone https://github.com/TIRUMALA9999/Agentic-Systems.git
cd Agentic-Systems
```

### 2) Create environment
```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate
```

### 3) Install dependencies
This repo includes a root `requirements.txt` (added for reproducibility):

```bash
pip install -r requirements.txt
```

### 4) Configure environment variables
Copy `.env.example` → `.env` and add your keys:

```bash
cp .env.example .env
```

---

## Run the demo

### A) ResearchCrew (config-driven, end-to-end)
1. Open `project/research_crew.ipynb`
2. Run all cells
3. It loads `project/config/agents.yaml` and `project/config/tasks.yaml`
4. Executes **sequential** Research → Summarize → Fact-check

### B) Flow orchestration demo
Open `Flows/AI-Agents-crash-course-Part-3.ipynb` to see:
- Flow patterns (`@start`, `@listen`)
- Routing/triage example
- OpenAI + Ollama usage patterns

### C) CLI scaffold (Flow template)
```bash
cd Flows/test_flow
python -m test_flow.main
```

---

## Outputs / artifacts

- `output.md` — example agent-produced output
- `Flows/social_media_content_writer/output/draft.json` — sample content draft artifact

---

## Points

- “I split the pipeline into research, summarization, and fact-checking to reduce hallucinations and make responsibilities clear.”
- “I used tool-augmented agents (web search) so the system can fetch up-to-date sources rather than relying on static training knowledge.”
- “I implemented flow-based orchestration to represent agent workflows as event-driven graphs, which is closer to production orchestration.”
- “I explored memory objects to understand how state and recall can improve continuity across steps.”
- “I grounded responses with a custom knowledge source so outputs can be tied to external data.”


---

## Author

**Tirumala Teja Yegineni**  
GitHub: https://github.com/TIRUMALA9999
