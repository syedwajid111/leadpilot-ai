# LeadPilot AI

An autonomous AI sales agent for service businesses (BSCS Final Year Project).

It chats with website visitors, finds out what they need, quotes real prices from the rate card,
scores the lead with an explainable BANT model (Hot / Warm / Cold) and books a discovery call.
The sales team gets a dashboard with every lead, the score with reasons, the full conversation
including the agent's tool calls, and an AI-written summary and follow-up email.

## Features
- AI chat agent with tool calling: `get_services`, `get_package_details`, `update_lead_profile`, `get_available_slots`, `book_meeting`
- English, Urdu and Roman Urdu conversations
- Explainable lead scoring (Budget 30, Need 20, Timeline 20, Authority 15, Contact 15)
- Meeting booking with double-booking protection
- Admin dashboard: KPIs, filters, lead detail, follow-up agent
- Works without an AI key (rule-based fallback) and without a database (in-memory fallback)

## Stack
Next.js 15 (App Router) · TypeScript · Google Gemini (OpenAI-compatible API, Groq as backup) · Neon Postgres · Vercel

## Run locally
```bash
npm install
cp .env.example .env.local   # add GEMINI_API_KEY, ADMIN_PASSWORD (DATABASE_URL optional)
npm run dev                  # http://localhost:3000   admin: /admin
```

## Environment variables
| Name | Required | Purpose |
|---|---|---|
| `GEMINI_API_KEY` | recommended | AI agent (free key from aistudio.google.com/apikey) |
| `ADMIN_PASSWORD` | yes for production | Password for `/admin` (default `leadpilot-demo`) |
| `DATABASE_URL` | recommended | Neon Postgres; set automatically by Vercel Storage → Neon |
| `GROQ_API_KEY` | optional | Backup AI provider |
| `GEMINI_MODEL` | optional | Comma-separated model list to override the default |

## Customise for another business
Edit `lib/knowledge.ts` (company name, services, packages, prices, FAQs). The agent sells from this file.

## Project structure
```
app/                 pages and API routes
  page.tsx           demo agency website with the live agent
  about/             project explanation for examiners
  admin/             dashboard, lead detail, login
  api/chat           agent endpoint
  api/admin/insights follow-up agent endpoint
components/          ChatWidget, Insights, site chrome
lib/agent.ts         agent loop, tools, rule-based fallback
lib/scoring.ts       lead scoring model
lib/slots.ts         meeting slots (Pakistan time)
lib/store.ts         Neon Postgres / in-memory data layer
lib/llm.ts           AI provider client
lib/knowledge.ts     business knowledge base
lib/insights.ts      summary + follow-up email agent
lib/demo.ts          sample leads for presentations
```
