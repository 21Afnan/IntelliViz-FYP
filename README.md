<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:4A0D2E,50:C2185B,100:FF8FC7&height=220&section=header&text=IntelliViz&fontSize=58&fontColor=FFFFFF&fontAlignY=36&desc=Agentic%20analytics%20for%20predictive%20maintenance%20%C2%B7%20Final%20Year%20Project&descSize=16&descAlignY=58" width="100%" alt="IntelliViz"/>

<p>
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI"/>
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="PyTorch"/>
  <img src="https://img.shields.io/badge/LangGraph-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white" alt="LangGraph"/>
  <img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white" alt="Next.js"/>
  <img src="https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white" alt="Supabase"/>
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"/>
</p>

**Project showcase.** The source code is private; this page explains what we built and how it works.

</div>

---

## Why this project exists

Factories lose a great deal of money to machines that stop without warning. The usual answers are either to fix a machine after it breaks, which is slow and costly, or to service it on a fixed calendar, which wastes healthy parts and still misses some failures. The sensor data that could have warned the team is usually sitting in a database that the people on the floor cannot easily question.

**IntelliViz** reads that data continuously, predicts which machines are heading for trouble, schedules maintenance before the failure, and lets plant staff ask questions about their machines in everyday language.

Our guiding rule: **language models plan and explain, code computes and checks.** No number on screen comes from a model's guess.

| | |
|---|---|
| **Domain** | Industrial predictive maintenance: CNC machines, pumps, compressors, robotic arms |
| **Users** | Plant managers, maintenance engineers, operators, production analysts |
| **Outcome** | Less unplanned downtime, maintenance planned ahead, plant data anyone can query |

---

## What it does

**Live monitoring.** Vibration, motor temperature, current, pressure and RPM for every machine, streamed to the dashboard in real time, with health bands, stale-data warnings and per-category sensor limits.

**Failure prediction.** A multi-task LSTM looks at a short window of recent readings and estimates, for each machine, its remaining useful life in hours, the chance it fails in the next 24 hours, and the most likely failure type (bearing, hydraulic, electrical or motor overheat). A background worker scores new readings as they arrive.

**Maintenance workflow.** Work orders, scheduling and maintenance history in one place, so predictions turn into planned jobs.

**Energy tracking.** Consumption per machine and per period to spot waste.

**Orion AI, the analytics assistant.** Staff type a question such as *"Which compressors are most likely to fail this week?"* and get an answer backed by real computation.

---

## How Orion AI stays honest (research focus)

This is the research question at the heart of our FYP:

> Does checking an agent's numeric claims with deterministic code reduce unsupported claims more than letting the LLM review its own answer?

- **Agents with narrow jobs.** An Orchestrator, Analyst, Visualizer and Validator coordinate through LangGraph. The LLM decides *what* to analyse and *how* to explain it.
- **Code does the maths.** Fixed pandas tools produce every figure. The model never calculates.
- **A code-based Validator.** Each number in the final answer is traced back to the tool call that produced it. Anything that cannot be traced is shown to the user as **unverified** instead of being stated as fact.
- **Evaluation.** Ground-truth questions over more than 20,000 telemetry records, measuring answer accuracy, the unsupported-claim rate, and the cost of escalating hard questions from a small model to a larger one.

---

## Prediction model at a glance

| | |
|---|---|
| Data | About 24,000 time-stamped readings from 20 machines of four types |
| Inputs | Vibration, motor temperature, current, pressure, RPM, operating mode, hours since maintenance, ambient temperature |
| Model | Two-layer LSTM (128 hidden units, dropout 0.3) over the last 10 readings, with three output heads |
| Outputs | Remaining useful life (regression), failure within 24 h (binary), failure type (5 classes) |

We also retrained the model under stricter, leakage-free splits (future readings of known machines, and machines the model has never seen) and compared it with a gradient-boosting baseline, so that the reported numbers reflect realistic conditions rather than a lucky split.

---

## Architecture

```
Machine sensors (simulated IoT)
        |
   Supabase (PostgreSQL)  <---  Prediction worker (LSTM)
        |
   FastAPI backend: repository -> services -> REST + live streams
        |                              |
   Next.js dashboard              Orion AI (LangGraph agents + pandas tools + Validator)
```

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | Next.js, React, Tailwind CSS, shadcn/ui, React Query, Recharts |
| Backend | FastAPI, Pydantic, Uvicorn |
| Data | Supabase (PostgreSQL) |
| ML | PyTorch (LSTM), scikit-learn, pandas |
| Agents | LangChain, LangGraph, Gemini |
| Ops | Docker, Docker Compose |

---

## Team

| Member | Roll No. |
|---|---|
| **Afnan Shoukat** | BSAI-207 |
| Usama Shahid | BSAI-180 |
| Dur-e-Adan Noor | BSAI-211 |

**Supervisor:** Dr. Hina Ali, Department of Computer Science, National University of Modern Languages (NUML), Islamabad.

---

## Source code and contact

The full code (frontend, backend, prediction worker, analytics agents, trained models and data) is private as part of our Final Year Project. For a live demo, a technical walkthrough or collaboration, please get in touch.

<div align="center">

<a href="mailto:afnanshoukat35@gmail.com?subject=IntelliViz%20demo%20request">
  <img src="https://img.shields.io/badge/Email-afnanshoukat35%40gmail.com-FF4FA3?style=for-the-badge&logo=gmail&logoColor=white&labelColor=4A0D2E" alt="Email"/>
</a>
<a href="https://www.linkedin.com/in/afnanshoukat">
  <img src="https://img.shields.io/badge/LinkedIn-Afnan%20Shoukat-FF4FA3?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=4A0D2E" alt="LinkedIn"/>
</a>
<a href="https://github.com/21Afnan">
  <img src="https://img.shields.io/badge/GitHub-21Afnan-FF4FA3?style=for-the-badge&logo=github&logoColor=white&labelColor=4A0D2E" alt="GitHub"/>
</a>

<br/><br/>

© 2026 Afnan Shoukat, Usama Shahid and Dur-e-Adan Noor, NUML Islamabad. All rights reserved. This repository is a showcase; the source code is private.

</div>

