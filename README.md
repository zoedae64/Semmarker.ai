# Semmark — Agentic AI Knowledge Graph Bookmarker

Save anything, turn it into permissioned graph cards, find trusted answers, and let AI agents act with your context.

## What is this?
Semmark is an AI bookmarker and knowledge graph for teams. A Chrome extension summarizes paragraphs and proposes “cards” (title, key points, tags, citation) before you bookmark. Each card becomes a node in a permissioned graph. Hybrid search (vector + BM25) and LLaMA-powered RAG deliver cited, permission-aware answers and drive agentic workflows across Slack/Jira/GitHub/Google/M365.

## Problem
Work knowledge is scattered across chats, docs, tickets, and files. People spend 20–30% of time searching, recreate prior work, and AI assistants underperform without a unified, secure context with permissions.

## Solution
- Capture from anywhere: URLs, PDFs/files, images (OCR), emails, Slack/Google/M365, Jira, GitHub.
- Cardization: Chrome extension summarizes per paragraph and suggests cards with tags/citations before saving.
- Graph organization: auto-link, dedupe, versioning; permission inheritance (RBAC/ABAC).
- Retrieval: hybrid vector + BM25 with graph neighborhood expansion and cross-encoder rerank; strict ACL filtering.
- Answer + act: LLaMA returns JSON {answer, citations[], actions[]} and agents execute tool calls with audit trails.
- Deploy securely: cloud, on‑prem, or air‑gapped; encryption, audit, retention/legal hold.

## Key Features
- Chrome “cardization” capture flow.
- Permissioned knowledge graph with nodes for cards/files/people/projects.
- Semantic search + keyword (BM25) + graph expansion; always cite sources.
- Agentic workflows and template marketplace (support runbooks, onboarding kits, project brief generator) with human-in-the-loop.
- Spaces and sharing, SSO/RBAC, audit logs, retention policies.
- Analytics/ROI dashboard (time saved, reuse rate, answer quality).

## Agentic Workflows — User Journey
1) Setup: connect SSO/integrations, choose templates, set approval policies, bind tools with scoped credentials.
2) Trigger: Chrome extension, chat mention, work-app sidebar, or event-based trigger.
3) Grounding: hybrid retrieval + graph expansion; ACL filters; trim context to token budget.
4) Plan: LLaMA proposes draft + citations and actions[]; risk scored.
5) Review: human approves/edits; auto-approve allowed by policy for low risk.
6) Execute: agent performs tool calls (Slack/Jira/GitHub/Email) with full audit.
7) Close loop: outcomes saved as cards; feedback improves templates and reranking.

## Tech Stack (proposed, aligned with Investor Proposal)
- Frontend: React (Next.js) + TypeScript, Tailwind; Chrome Extension (Manifest V3, TS).
- Backend: Node.js (Fastify/NestJS) or Python (FastAPI) API; workers (BullMQ/Celery); WebSocket events.
- Graph DB: ArangoDB for MVP (fast, easy), with a path to JanusGraph for 100B+ edge scale and horizontal growth.
- Datastores: PostgreSQL for accounts/billing; S3-compatible object store for files/artifacts.
- Retrieval/Search: vectors in pgvector; BM25/keyword in OpenSearch/Elasticsearch; hybrid blending with score normalization and cross-encoder rerank.
- AI: Llama 3.x (8B–70B) for RAG and planning; small quantized model in the extension; optional LoRA adapters.
- Integrations: Slack, Google Workspace, Microsoft 365, Jira, GitHub; OAuth2/SAML/OIDC; SCIM.
- Observability: OpenTelemetry, Prometheus/Grafana, structured logs.
- Deployment: Docker, Kubernetes (Helm), Terraform; cloud/on‑prem/air‑gapped.

## LLaMA Integration (Prompt + System)
- System prompt enforces: answer only from provided CONTEXT, respect permissions, always include citations, return JSON schema {answer, citations[], actions[]}.
- Context is built with hybrid retrieval (pgvector + BM25/OpenSearch) and 1–2 hop graph expansion from ArangoDB; all items carry source ids and ACL tags.
- Policy engine validates citations/ACLs; agent executor performs tool calls with audit logs.

## Security & Compliance
- RBAC/ABAC with per-object ACLs, least-privilege credentials for tools.
- Encryption in transit and at rest; audit trails; retention/legal hold; optional PII redaction for logs.

## Deployment Modes
- SaaS (default), customer VPC, on‑prem, or air‑gapped with quantized models.

## Getting Started 
- Planned structure:
  - /apps/extension — Chrome “cardization” extension
  - /services/api — API gateway
  - /services/worker — background jobs
  - /packages/shared — shared types/schemas
- Quickstart docs, Docker Compose for local, and Helm charts for Kubernetes deployment.

## Roadmap (engineering highlights)
- MVP: extension capture → graph storage → hybrid search → cited answers.
- Early workflows: support reply, onboarding kit, project brief generator via Marketplace/templates.
- Evaluations: faithfulness/citation coverage; latency/cost SLOs.
- Enterprise: SSO/SCIM, DLP/retention, private deployments.

## Related Documents
- Business Model Canvas: Semmark_Business_Model_Canvas.md
- Investor Proposal: Semmark_Investor_Proposal.md
- Backlog: Semmark_Backlog.md
- Market Validation Survey (EN/ID): Semmark_Market_Validation_Survey.md, Semmark_Market_Validation_Survey_ID.md

## License
Apache 2.0

## Contact
royadv32@gmail.com (Roy Adventus)
