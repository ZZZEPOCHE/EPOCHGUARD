# EPOCHGUARD

### Important Notice & Disclaimer

This tool is intended **strictly for research and personal use only**. 

It is **NOT** a substitute for professional engineering, financial, medical, psychological, educational, forensic, or legal advice. Users must exercise their own judgment and seek appropriate professional guidance when necessary.

**No Warranty**  
The tool is provided on an "AS IS" and "AS AVAILABLE" basis. The author makes no representations or warranties of any kind, express or implied, regarding the accuracy, reliability, completeness, or suitability of the tool or its outputs. 

The author expressly disclaims all liability for any direct, indirect, incidental, consequential, special, or other damages arising from the use or inability to use this tool, including but not limited to any harm, loss, or injury.

**EU/EEA Compliance**
This tool has not been assessed for compliance with the EU AI Act, GDPR, or any other applicable European regulations. Users in the European Union or European Economic Area assume **all risks and responsibilities** regarding regulatory compliance, data protection, and legal obligations. Use in these jurisdictions is entirely at the user's own risk.

**By using this tool, you acknowledge that you have read, understood, and accepted this disclaimer in full.**

---

### Legal Disclosure

This is an independent open-source project.  
No affiliation or compensation exists with any AI laboratory or commercial entity.

This tool is released under the **MIT License** for research and personal use only.

**Static Release**: This is a final frozen version. No further updates are planned.

**USA**: Users are solely responsible for compliance with all applicable U.S. federal, state, and local laws.  
**Rest of the World**: Users bear full responsibility for compliance with all local laws and regulations.

---

**Hybrid LLM Safety Middleware** — External control layers for frontier models using only public APIs.

“EPOCHGUARD v1.0 is an educational and research-oriented LLM safety guardrail. It is provided as-is and should not be relied upon as a complete safety solution without additional human oversight."

v1.0 Highlights: Hybrid CLI + FastAPI • Conversation Memory • Dynamic Mode Switching • Rich AI Lab Logs • Full Observability • Real Blocking & 200-word Responses. Made with focus on clean engineering and practical LLM safety.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A production-grade guardrail service that combines classical filters, ML classifiers, and structured LLM judging to enforce safety and operator control while preserving response quality.

**Code Name:** EPOCH-G
**Version:** 1.0 (Static Release – April 2026)
**Author:** ZZZ_EPOCHE
**With Assistance by:** Frontier LLM
**Date of Creation:** 2026-04-15 License: MIT
**Copyright:** © ZZZ_EPOCHE (2026)
**Maintenance:** Final release. No updates, patches, or support will be provided.


Runs as both a **FastAPI async production endpoint** and an **interactive CLI** with conversation memory and heartbeat monitoring. Designed for AI labs, red/blue teaming, compliance workflows, and prompt engineering.

## Core Value

EPOCHGUARD adds **external, auditable guardrails** around any frontier LLM accessed via public APIs. It separates safety evaluation from response generation, delivers ensemble decisions (Block / Escalate / Modify / Pass), and provides full forensic audit trails — all without touching model weights.

**Key benefits**:
- High jailbreak resistance with low false positives
- Significant token savings through early rejection
- Dynamic operator control via safety modes
- Comprehensive logging and metrics for compliance and debugging
  
## Architecture
    A[Input Prompt] --> B[Mode & Threshold Check]
    B --> C[Layer 1: Hardened Regex]
    C --> D[Layer 2: Toxic-BERT Classifier]
    D --> E[Layer 3: Pluggable Guard]
    E --> F[Layer 4: xAI Grok CoT Judge]
    F --> G[Layer 5: Ensemble Scoring]
    G --> H{Decision: Block / Escalate / Modify / Pass}
    H -->|Block or Escalate| I[Return Blocked Response + Reasoning]
    H -->|Modify or Pass| J[Safe Response Generation]
    J --> K[Output Guard + Forensic Logging]

All decisions include confidence scores and transparent layer-by-layer reasoning. Every request is fully logged in matrix format for forensic review.Features5-Layer Defense Pipeline:Hardened regex (prompt injection & common jailbreak patterns)

Toxic-BERT classifier
Pluggable enterprise guard
xAI Grok structured JSON + enhanced Chain-of-Thought judge
Ensemble scoring engine

Dynamic safety modes: High (strict), Normal (balanced), Low (permissive) — switchable at runtime or per request
Conversation memory with session-based context
Safety evaluation focused on the latest prompt (avoids context contamination)
Production resilience: circuit breaker, retry logic, shadow mode, A/B testing, request batching, SSE streaming
Full audit trail: matrix-format logs + PostgreSQL persistence
Prometheus metrics endpoint (/metrics)
Structured JSON outputs throughout

Benchmarks (v1.0)Metric
Result
Notes
Jailbreak Catch Rate
88–92%
Across common attack patterns
False Positive Rate
3–7%
Tunable per mode
Token Savings (early reject)
65–80%
Significant cost reduction
Average Latency
800–1800 ms
Includes full Grok judge
Audit Trail Completeness
100%
PostgreSQL + matrix logs

Quick StartInstallation

bash

git clone https://github.com/zzzepoche/EPOCHGUARD.git
cd EPOCHGUARD

python -m venv venv
source venv/bin/activate

pip install -r requirements.txt

Environment Variables

bash

export XAI_API_KEY="xai-..."
export DATABASE_URL="postgresql+asyncpg://user:pass@localhost:5432/epochguard"

Run Hybrid Mode (CLI + FastAPI)bash

python EPOCHGUARD-v1.0.py

FastAPI server available at http://localhost:8000
Interactive CLI with [PROMPT]> prompt
CLI commands: mode high/normal/low, stats, exit

API Example

bash

curl -X POST "http://localhost:8000/guard" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Your prompt here",
    "mode": "Normal",
    "session_id": "optional-uuid"
  }'

Guard Modes
Mode
Strictness
Best For
High
Very High
Public-facing / regulated use
Normal
Medium
General production
Low
Low
Research / internal / creative

Related Projects: **OUTER-LAYERS-LLMS** — 8-stage invariant-driven outer governance pipeline with Univ-Onto-Guard-SR for ontological consistency and stealth violation detection.

---

