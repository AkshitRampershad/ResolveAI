# ResolveAI — Evidence-Driven Banking Dispute Resolution

> An AI-powered payment investigation copilot that reconstructs transaction timelines, reconciles payment events, identifies missing evidence, and prepares auditable resolution recommendations.

**Built for:** Banking AI Hackathon  
**Project category:** Agentic AI · Financial Services · Intelligent Automation · Responsible AI  
**Status:** Hackathon prototype in development

---

## Overview

Payment disputes and transaction errors can require investigators to piece together information from transaction records, payment processor events, customer reports, and operating procedures.

ResolveAI aims to reduce this investigative burden through an evidence-driven AI workflow.

Instead of simply answering questions about a payment, ResolveAI investigates a case by retrieving transaction records, reconstructing event timelines, identifying inconsistencies, retrieving relevant procedures, and preparing a structured recommendation for human review.

The system distinguishes verified facts from hypotheses and explicitly identifies missing evidence. When transaction status is uncertain, it recommends further investigation rather than inventing a resolution.

**The goal:** Reduce investigation time, improve evidence traceability, and support safer, more consistent dispute resolution.

## The Problem

Investigating a payment issue can involve several challenges:

- Fragmented transaction and processor records.
- Incomplete or contradictory payment-status information.
- Manual reconciliation of multiple payment attempts.
- Time-consuming retrieval of relevant procedures.
- Inconsistent investigation documentation.
- Difficulty tracing recommendations back to supporting evidence.
- Risk of premature action when the final payment status is unknown.

These challenges create opportunities to improve operational efficiency without removing human accountability.

## The Solution

ResolveAI combines deterministic transaction processing with LLM-based reasoning and policy retrieval.

### Core capabilities

**1. Payment timeline reconstruction**

Organizes transaction events chronologically and identifies missing, duplicated, or contradictory events.

**2. Transaction reconciliation**

Compares payment attempts, ledger entries, reversals, and processor events to identify discrepancies requiring investigation.

**3. Evidence-grounded investigation**

Uses an LLM to interpret structured evidence and produce a concise investigation summary. Material findings must reference their supporting records.

**4. Policy-aware recommendations**

Retrieves relevant, versioned operating procedures and identifies the next permitted investigation step.

**5. Uncertainty and escalation management**

Separates confirmed facts from hypotheses, flags insufficient evidence, and routes ambiguous or high-impact cases for human review.

**6. Auditable case documentation**

Generates a structured case report containing findings, evidence references, missing information, recommended actions, and reviewer decisions.

**7. Evaluation and performance measurement**

Compares AI-assisted investigations against a baseline using investigation time, evidence accuracy, recommendation quality, unsupported claims, and escalation performance.

## Example Use Case

A customer reports that an $850 payment was debited from their account, but the merchant says the payment was not received.

ResolveAI:

1. Retrieves the available transaction and processor events.
2. Reconstructs the payment timeline.
3. Identifies a processor timeout and a second payment attempt.
4. Checks whether the authoritative settlement status is available.
5. Retrieves the applicable investigation procedure.
6. Identifies missing evidence and possible duplicate-payment risk.
7. Recommends reconciliation and prepares a case summary for an authorized investigator.

If settlement cannot be verified, ResolveAI does not claim that the payment failed or issue an automatic refund. It records the uncertainty and recommends the appropriate next step.

*This scenario uses synthetic data and does not represent an actual customer case.*

## System Architecture

```text
                  Synthetic Banking Data
                           |
          +----------------+----------------+
          |                |                |
     Transactions     Processor Events   Policies
          |                |                |
          +----------------+----------------+
                           |
                 Evidence Normalization
                           |
                 Transaction Reconciliation
                           |
                +----------+----------+
                |                     |
          Investigation Agent    Policy Retrieval
                |                     |
                +----------+----------+
                           |
                  Decision and Control
                           |
          +----------------+----------------+
          |                |                |
      Case Report     Missing Evidence   Audit Log
          |                |                |
          +----------------+----------------+
                           |
                 Investigator Dashboard
```

### Architectural principles

- Deterministic code handles transaction calculations, event ordering, and reconciliation rules.
- The LLM interprets evidence, develops hypotheses, and generates structured summaries.
- Retrieval grounds procedural recommendations in approved documentation.
- The control layer validates output, checks permissions, and enforces approval requirements.
- Audit records capture evidence references, recommendations, and reviewer decisions.

## Technology Stack

| Layer | Technology |
|---|---|
| Frontend | Next.js, React, TypeScript |
| Backend | Python, FastAPI |
| Data storage | PostgreSQL |
| Policy retrieval | pgvector or Qdrant |
| AI reasoning | LLM with structured output and tool calling |
| Data validation | Pydantic |
| Testing | Pytest |
| Deployment | Docker |
| Monitoring | Structured logging and evaluation metrics |

The final implementation may vary depending on the hackathon environment, available model providers, and infrastructure constraints.

## Data Strategy

The prototype uses synthetic banking records rather than real customer information.

Example entities include:

- `transactions`: transaction identifiers, amounts, timestamps, and statuses.
- `payment_events`: processor requests, acknowledgments, timeouts, reversals, and settlement events.
- `disputes`: case identifiers, reported issues, and investigation status.
- `policies`: approved procedures, versions, effective dates, and source references.
- `investigation_findings`: conclusions, evidence references, confidence, and missing information.
- `audit_events`: tool calls, validation outcomes, reviewer actions, and timestamps.

Synthetic scenarios should include:

- Delayed payment processing.
- Duplicate payment attempts.
- Duplicate debit risk.
- Reversed transactions.
- Settled transactions reported as missing.
- Unauthorized transaction reports.
- Incomplete or contradictory evidence.

Each evaluation case should have a predefined expected outcome so that the system can be tested reproducibly.

## Evaluation Framework

ResolveAI should be evaluated against a baseline investigation workflow using the same test cases.

| Metric | Evaluation method |
|---|---|
| Investigation time | Median elapsed time per case |
| Evidence accuracy | Percentage of material findings supported by the correct records |
| Root-cause accuracy | Percentage of cases with the correct primary finding |
| Unsupported claims | Number of claims without adequate evidence |
| Recommendation quality | Percentage of recommendations consistent with the test-case answer key |
| Escalation accuracy | Percentage of uncertain or high-impact cases correctly escalated |
| Deadline accuracy | Correctness against the applicable rule and case facts |
| Cost per case | AI, retrieval, infrastructure, and human-review costs |

Performance targets will be established after measuring the baseline. No efficiency or accuracy improvement should be reported as achieved until supported by test results.

## Responsible AI and Security

Financial workflows require more than plausible model outputs.

ResolveAI is designed around the following controls:

- **Evidence traceability:** Findings reference the records that support them.
- **Uncertainty handling:** Missing or contradictory evidence triggers additional investigation or escalation.
- **Deterministic validation:** Financial calculations, transaction comparisons, and deadline calculations are not delegated solely to an LLM.
- **Human oversight:** Consequential actions require the appropriate authorization.
- **Least-privilege access:** Tools expose only the operations necessary for the investigation.
- **Prompt-injection defenses:** Retrieved documents and customer-provided text are treated as untrusted data.
- **Data minimization:** The prototype uses synthetic data and avoids unnecessary sensitive information.
- **Auditability:** Recommendations and reviewer actions are recorded for later examination.

ResolveAI is a decision-support prototype, not a production banking system, legal determination engine, or autonomous payment-processing service.

## Getting Started

### Prerequisites

- Python 3.11+
- Node.js 20+
- PostgreSQL
- An LLM provider API key, if using a hosted model
- Git and Docker (recommended)

### Installation

Clone the repository:

```bash
git clone <YOUR_REPOSITORY_URL>
cd resolveai
```

Create and activate a Python virtual environment:

```bash
python -m venv .venv
```

Activate it on macOS or Linux:

```bash
source .venv/bin/activate
```

On Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Install backend dependencies after the project dependency file has been created:

```bash
pip install -r requirements.txt
```

Configure the environment:

```bash
cp .env.example .env
```

Populate the required configuration values locally. Never commit API keys or credentials.

Start the backend using the configured application entry point:

```bash
uvicorn app.main:app --reload
```

The command assumes the backend entry point is located at `app/main.py`; adjust it if the repository uses a different structure.

Start the frontend from its directory:

```bash
cd frontend
npm install
npm run dev
```

The frontend command assumes a Next.js application exists in `frontend/`.

**Note:** These commands describe the intended setup. They should be updated to match the actual repository structure and dependencies before the first public release.

## Roadmap - WIP

### Phase 1 — Core investigation workflow
- [ ] Define transaction, event, and dispute schemas.
- [ ] Generate synthetic investigation cases.
- [ ] Implement transaction lookup and timeline reconstruction.
- [ ] Add deterministic reconciliation rules.
- [ ] Produce a structured investigation report.

### Phase 2 — Evidence-grounded AI
- [ ] Integrate an LLM with structured output.
- [ ] Add policy retrieval and source references.
- [ ] Implement missing-evidence detection.
- [ ] Validate findings against underlying records.
- [ ] Add uncertainty-aware escalation.

### Phase 3 — Investigator experience
- [ ] Build the case dashboard.
- [ ] Display transaction timelines and evidence.
- [ ] Show recommendations and unresolved questions.
- [ ] Add reviewer approval and audit history.

### Phase 4 — Evaluation and hardening
- [ ] Create a labeled evaluation dataset.
- [ ] Implement baseline comparisons.
- [ ] Test duplicate payments and contradictory events.
- [ ] Test unsupported claims and prompt injection.
- [ ] Measure latency, cost, accuracy, and safe escalation.
- [ ] Document limitations and evaluation results.

## Business Impact

ResolveAI targets three measurable outcomes:

1. **Operational efficiency:** Reduce the time employees spend gathering and reconciling evidence.
2. **Decision quality:** Improve the consistency and traceability of investigation findings.
3. **Risk control:** Reduce unsupported conclusions and inappropriate actions when evidence is incomplete.

The business case will be quantified through controlled evaluation rather than assumed savings.

## Project Status

ResolveAI is a proposed hackathon prototype. Features, metrics, integrations, and performance claims should be updated as implementation and testing progress.

The project is not affiliated with, endorsed by, or integrated with Bank of America unless explicitly authorized.

## References

- [Bank of America — How to dispute a charge and check claim status](https://www.bankofamerica.com/help/how-to-dispute-a-charge/)
- [Bank of America — Credit card dispute FAQs](https://www.bankofamerica.com/credit-cards/credit-card-disputes-faq/)
- [NIST — AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)

These references provide public context for dispute workflows and responsible AI development; they do not imply access to internal bank procedures.

---

**ResolveAI — Investigate with evidence. Recommend with confidence. Resolve with control.**
