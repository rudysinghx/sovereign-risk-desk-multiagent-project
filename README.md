# Sovereign Risk Desk

Transparent four agent system for sovereign risk monitoring and IMF style country briefs.

Portfolio project inspired by official sector and banking risk workflows.  
This is not a replica of any proprietary IMF, World Bank, or bank internal model.  
This is not for investment or policy decisions.

**GitHub:** https://github.com/rudysinghx/sovereign-risk-desk

## Project summary

### What this is
A modular Python pipeline that:
1. Loads public IMF World Economic Outlook data
2. Computes clear sovereign risk scores with documented rules
3. Writes structured country briefs
4. Uses an independent Review step that must PASS before a brief is final

### The four agents
| Agent | Role | Uses LLM |
|-------|------|----------|
| Data Agent | Clean and validate WEO data into a CountryDataSnapshot | No |
| Risk Intelligence Agent | Component scores, regime label, simple forecasts | No |
| Research and Report Agent | Professional brief from structured numbers only | Optional, off by default |
| Review Agent | Checks consistency and grounding, returns PASS or FAIL | No |

An orchestrator runs the agents in order and retries only the failing step.

### Countries demonstrated
- Sri Lanka (LKA), 2022 external default episode
- Zambia (ZMB), 2020 external default episode
- India (IND), no distress event

### Key results
- Full pipeline runs end to end
- LKA, ZMB, and IND all received Review PASS
- Latest illustrative scores on a 0 to 100 scale:
  - Sri Lanka about 36.6
  - Zambia about 55.0
  - India about 39.0
- Walk forward evaluation showed scores rising into the documented default windows for Sri Lanka (2022) and Zambia (2020)

### Design principles
- Numbers never come from an LLM
- Agents communicate through typed Pydantic contracts
- Scoring rules live in YAML
- Point in time discipline in evaluation
- Clear limitations, no overclaiming

### Tech stack
Python, Pydantic, Pandas, PyYAML, Jinja2, structured logging

### Status
Working local prototype for portfolio demonstration and technical discussion.

## Quick start

Requirements: Python 3.11 or newer

```bash
git clone https://github.com/rudysinghx/sovereign-risk-desk.git
cd sovereign-risk-desk
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python scripts/run_pipeline.py
python scripts/run_evaluation.py
