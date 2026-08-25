# Operational CoPilot - Partner Intelligence Platform

A multi agent AI system built for restaurant and retail partners on a food delivery platform. It gives partners a single conversational interface for managing their store, understanding their performance, and getting proactive, data driven guidance, instead of navigating a traditional dashboard.

**Live demo:** https://giamarigkos-del.github.io/efood-intelligence/intelligence-login.html

## What This Repo Contains

This repository holds the frontend: the chat interface, widget rendering, and login flow that partners interact with. The system's intelligence lives in a multi agent backend built with n8n, Supabase, and the Claude API. That backend is not included here since it holds production credentials and business logic, but the architecture below describes how it works end to end.

## Architecture

A single orchestration workflow routes every incoming message to one of four specialized agents, each with its own memory and tool set.

- **Orchestrator** - classifies intent and routes each message to the right specialist agent, with logic to keep multi turn conversations on topic
- **Intelligence Agent** - reads and updates store data (products, pricing, availability, modifiers) and can escalate issues that need human follow up
- **Coaching Agent** - gives partners behavioral, evidence based recommendations, drawing on a knowledge graph of category specific strategies grounded in behavioral economics research (Kahneman and Tversky, Thaler and Sunstein, Deci and Ryan)
- **Prediction Agent** - forecasts demand shifts from weather and calendar events (holidays, religious observances, local events), with category aware reasoning about how each factor affects a given business type
- **Knowledge Base Agent** - semantic search over a support knowledge base using vector embeddings, for policy and how to questions

Each agent keeps its own isolated conversation memory while sharing a session context, so the system feels like one coherent assistant rather than four separate bots.

## Tech Stack

- **Orchestration:** n8n (visual workflow orchestration, one workflow with multiple AI agent nodes)
- **LLM:** Claude (Anthropic API)
- **Database:** Supabase / Postgres with pgvector for semantic search
- **Embeddings:** OpenAI text-embedding-3-small
- **External data:** Tavily (weather and event search)
- **Frontend:** HTML/CSS/JS, deployed on GitHub Pages

## Key Features

- Category aware demand forecasting that accounts for weather, weekday patterns, and a calendar of regional holidays and events, without naming specific products unless the underlying data supports it
- A behavioral coaching graph that gives store specific, evidence backed recommendations instead of generic advice
- Full bilingual support (Greek and English) across every agent, including semantic search and forecasting
- A 58 test automated regression suite covering all four agents, run before every production change

## Known Limitation

Store level access control is currently enforced at the tool and URL level rather than through a database level row security policy. This is a disclosed, intentional tradeoff for a proof of concept stage system and is documented as an open item for the next iteration.

## Status

Production stage internal deployment. Presented to senior engineering and business leadership as a proof of concept for company wide AI automation adoption.
