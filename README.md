# ClientOps AI

**MCP-powered agentic business operations — turn a plain-English client request into scheduled meetings, task records, approvals, and notifications in one shot.**

---

## What It Does

ClientOps AI connects an AI Agent to a suite of business tools via the Model Context Protocol (MCP). You send a natural-language request; the agent figures out what needs to happen and calls the right tools — no manual handoffs, no rigid form flows.

A single request can:
- Create a client record in Google Sheets
- Schedule a meeting on Google Calendar
- Raise an approval request and route it to a human reviewer
- Send a Gmail notification and a WhatsApp message on approval or rejection

---

## Architecture

```
Client Request
      │
   AI Agent  (OpenAI + n8n)
      │
  MCP Client
      │
  MCP Server
  ├── create_client_record     → Google Sheets
  ├── schedule_meeting         → Google Calendar
  ├── create_approval_request  → Human approval queue
  ├── send_notification        → Gmail + WhatsApp Cloud API
  └── generate_summary         → Structured output

Human Approval Queue
      │
  Approved / Rejected
      │
  Email & Messaging Workflows
```

---

## Tech Stack

| Layer | Tools |
|---|---|
| Workflow orchestration | n8n (Docker) |
| AI agent | OpenAI |
| Tool protocol | MCP (Model Context Protocol) |
| Data | Google Sheets |
| Calendar | Google Calendar |
| Notifications | Gmail, WhatsApp Cloud API |
| Infrastructure | Docker |

---

## Key Concepts Demonstrated

- **Agentic workflow design** — the agent decides tool execution order at runtime, not at design time
- **MCP client/server architecture** — clean separation between the agent's reasoning layer and the tools it can call
- **Human-in-the-loop** — approvals are a first-class step, not an afterthought
- **Event-driven automation** — downstream workflows trigger on approval/rejection events
- **AI tool calling** — structured outputs from unstructured natural-language input

---

## Getting Started

> Prerequisites: Docker, n8n, an OpenAI API key, Google OAuth credentials, WhatsApp Cloud API access.

```bash
# Clone the repo
git clone https://github.com/AbdullahUsman0/clientops-ai.git
cd clientops-ai

# Start n8n via Docker
docker compose up -d
```

Then import the workflow JSON into your n8n instance and configure the credential nodes for OpenAI, Google, and WhatsApp.

---

## Roadmap

- [ ] Custom Python MCP Server
- [ ] Multi-agent architecture
- [ ] Vector database + RAG-powered knowledge retrieval
- [ ] Slack and Microsoft Teams integrations
- [ ] Production deployment guide
