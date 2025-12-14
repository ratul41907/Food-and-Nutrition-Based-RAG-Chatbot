# CRAVEBOT
## Hybrid RAG Chatbot for Nutrition Intelligence
### Dataset-First Retrieval • Fuzzy Systems • Rule Engine • LLM-Augmented Generation

![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![AI](https://img.shields.io/badge/AI-Hybrid%20RAG%20System-green)
![RAG](https://img.shields.io/badge/Architecture-Dataset--First%20RAG-orange)
![UI](https://img.shields.io/badge/UI-Gradio-lightgrey)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## Executive Summary

CraveBot is an industrial-style hybrid AI system that answers nutrition and food-related
questions using a **dataset-first Retrieval-Augmented Generation (RAG) architecture**.
It combines **fuzzy retrieval**, **rule-based reasoning**, **fuzzy decision logic**,
and an **LLM generation layer** (simulated for local execution).

Unlike prompt-only chatbots, CraveBot prioritizes **auditable data retrieval** and
**deterministic reasoning**, with the LLM used strictly for response generation.

This repository is designed as a **portfolio-grade, recruiter-facing AI systems project**.

---

## Why This Project Matters (Recruiter Focus)

This project demonstrates the ability to:

- Design **hybrid AI systems**, not just call LLM APIs
- Implement **dataset-first RAG** instead of prompt-first guessing
- Handle **uncertainty and missing data** using fuzzy systems and imputation
- Combine **symbolic rules + statistical ML + generative models**
- Build **production-style reasoning pipelines** with explainability
- Ship an **interactive AI application** (Gradio)

---

## Core Architecture Philosophy

CraveBot follows a **Dataset → Retrieval → Reasoning → Generation** pipeline.

The LLM does **not** invent facts.
It only **rephrases verified, structured outputs**.

---

## High-Level System Architecture

Food Dataset (Parquet / Fallback Table)
        |
        v
Normalization & Preprocessing
        |
        v
Fuzzy Retrieval Engine
(RapidFuzz / difflib fallback)
        |
        v
Rule Engine & Fuzzy Reasoning
- Macro rules
- Calorie thresholds
- Meal balancing
- Imputation logic
        |
        v
RAG Context Construction
(Auditable factual output)
        |
        v
LLM Generation Layer (Simulated)
        |
        v
User-Facing Conversational Response
        |
        v
Gradio Web Interface

---

## Key Components

### 1. Dataset-First Retrieval (RAG)

- Uses a structured food dataset (Parquet preferred)
- Falls back to an internal curated dataset if unavailable
- Retrieval happens **before** any generation
- Every numeric output is traceable to:
  - Dataset row
  - Category median
  - Global median

---

### 2. Fuzzy Matching System

- Primary engine: RapidFuzz (WRatio)
- Automatic fallback: difflib
- Handles:
  - Misspellings
  - Partial names
  - Natural language food queries

Confidence levels:
- High: Direct row match
- Medium: Category median imputation
- Low: Global median imputation

---

### 3. Rule Engine & Fuzzy Reasoning

Implemented deterministic rules for:

- High-calorie detection
- Macro balance evaluation
- Meal composition advice
- Food pairing suggestions
- Healthier alternative retrieval
- Category-aware reasoning

Example conceptual rules:
```
IF energy_kcal_100g > 400 THEN mark as high_calorie
IF carb-heavy THEN suggest protein + vegetables
IF fat-heavy THEN recommend portion control
```

---

### 4. Imputation & Uncertainty Handling

When data is missing or invalid:

1. Attempt direct row retrieval
2. Fall back to category medians
3. Fall back to global medians
4. Clearly label confidence level

This prevents hallucination while maintaining usability.

---

### 5. RAG Context Construction

Before LLM involvement, the system builds a **structured, factual context** containing:

- Exact numeric values
- Data source
- Confidence level
- Explanatory notes
- Rule-based recommendations

This context is the **only input** to the LLM.

---

### 6. LLM Generation Layer (Simulated)

- LLM step is intentionally **simulated** for local execution
- Designed to be replaced with:
  - Phi-3
  - LLaMA
  - Gemma
  - Any production LLM API

LLM responsibilities:
- Read structured facts
- Improve readability
- Add conversational tone
- Never invent numbers

---

### 7. Interactive Application (Gradio)

- Real-time user queries
- Execution-time measurement
- Fuzzy engine status display
- Example prompts included
- Production-style UI layout

---

## Supported Query Types

- Nutrient lookup:
  - "How many calories in 150g chicken breast?"
- Comparisons:
  - "Compare protein in banana vs kiwi"
- Meal planning:
  - "I have rice and chicken for 500 kcal"
- Health advice:
  - "What should I pair with avocado?"
- General nutrition Q&A with retrieval guarantees

---

## Installation

Prerequisites:
- Python 3.8+
- pip

Install dependencies:
```bash
pip install pandas numpy gradio rapidfuzz pyarrow
```

Optional (for Parquet dataset):
```bash
pip install fastparquet
```

---

## Running the Application

```bash
python cravebot.py
```

The Gradio interface will launch in your browser.

---

## Configuration

```text
FOOD_DATA_PATH
FUZZY_CUTOFF_SCORE
```

- Dataset path can be replaced with any compatible Parquet file
- Fuzzy threshold controls strictness of retrieval

---

## Design Guarantees

- No hallucinated numeric values
- All outputs are explainable
- Deterministic reasoning layer
- LLM isolated from raw data
- Graceful degradation on missing data

---

## Limitations

- LLM generation is simulated in this environment
- Rules are heuristic-based (not learned)
- No vector database (yet)
- No persistent memory across sessions

---

## Future Enhancements

- Replace simulated LLM with production API
- Add vector embeddings for semantic retrieval
- Introduce learning-based fuzzy rule tuning
- Add user personalization
- Deploy via Docker and cloud services
- Add telemetry and monitoring

---

## Skills Demonstrated

- Hybrid AI system design
- Retrieval-Augmented Generation (RAG)
- Fuzzy logic and uncertainty handling
- Rule-based reasoning systems
- Data engineering with pandas
- Explainable AI principles
- LLM-safe architecture patterns
- Interactive AI application development

---

## Dependencies

```text
python >= 3.8
pandas
numpy
gradio
rapidfuzz (optional, auto-fallback)
pyarrow
```

---

## Contributors

```text
Arafat Zaman Ratul
```

---

## License

```text
MIT License

Copyright (c) 2025 Arafat Zaman Ratul

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
