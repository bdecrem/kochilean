# Kochi.to - SMS-Based AI Agent Platform

Welcome to the kochi.to codebase! This repository contains the core functionality for our SMS-based AI agent assistant platform.

## What is Kochi.to?

Kochi.to is a personal AI agent assistant accessible via SMS. It provides:

- **AI Agents**: Crypto research, YouTube search, stock tracking, arXiv research, daily insights
- **Personal Assistant**: Information retrieval, task automation over SMS
- **Conversational AI**: Multi-turn conversations with specialized agents
- **Daily Reports**: Automated daily briefings (crypto, AI news, academic papers, etc.)
- **SMS Interface**: All interactions happen via text message

## Repository Structure

This is a minimal clone containing the essential components:

```
kochilean/
├── sms-bot/              # Core SMS processing engine
│   ├── src/             # Main application code
│   ├── lib/             # Shared libraries and utilities
│   ├── commands/        # SMS command handlers
│   ├── agents/          # AI agent implementations
│   ├── content/         # Content templates
│   ├── migrations/      # Database migrations
│   ├── api/             # API endpoints
│   └── documentation/   # Technical documentation
│
├── web/                  # Web interface (minimal)
│   ├── app/
│   │   ├── report-viewer/  # View generated reports
│   │   └── music-player/   # Audio player
│   ├── components/      # React components
│   └── lib/             # Web utilities
│
├── CLAUDE.md            # Development guidelines and architecture
├── AGENTS.md            # Agent system overview
└── README.md            # This file
```

## Key Technologies

- **Backend**: TypeScript, Node.js
- **SMS**: Twilio
- **Database**: Supabase (PostgreSQL)
- **AI**: Anthropic Claude API, Claude Agent SDK
- **Deployment**: Railway (production)
- **Agent Framework**: Custom agent pipeline with autonomous and scripted agents

## Getting Started

### Prerequisites

- Node.js 24+
- npm or yarn
- Access to:
  - Twilio account (for SMS)
  - Supabase project (for database)
  - Anthropic API key (for AI agents)

### Installation

```bash
# Install dependencies
npm install

# Set up environment variables
cp .env.local.example .env.local
# Edit .env.local with your credentials

# Build the project
cd sms-bot && npm run build

# Start the SMS listener (development)
node dist/src/index.js
```

### Configuration

Create `.env.local` files with the required credentials:

**Required Environment Variables:**
- `ANTHROPIC_API_KEY` - Claude API key
- `TWILIO_ACCOUNT_SID` - Twilio account identifier
- `TWILIO_AUTH_TOKEN` - Twilio authentication
- `TWILIO_PHONE_NUMBER` - Your Twilio phone number
- `SUPABASE_URL` - Supabase project URL
- `SUPABASE_SERVICE_KEY` - Supabase service role key

See `.env.local.example` for complete list.

## Architecture Overview

### SMS Processing Flow

```
Incoming SMS → Twilio Webhook → sms-bot/src/index.ts
    ↓
Controller (orchestration)
    ↓
Command Dispatcher → Agent/Command Handler
    ↓
AI Processing (Claude API or Agent SDK)
    ↓
Response Generation → Twilio (outgoing SMS)
```

### Agent Types

1. **Autonomous Agents** (using claude-agent-sdk)
   - Crypto research agent
   - arXiv research agent
   - Knowledge graph query agent
   - Fully autonomous with tool use

2. **Scripted Workflow Agents**
   - YouTube search agent
   - Stock news agent
   - Medical daily briefings
   - Ticketmaster events
   - Predefined workflows with AI enhancements

### Key Modules

- **controller.ts**: Request routing and orchestration
- **storage-manager.ts**: All database operations
- **notification-client.ts**: SMS/email sending
- **commands/**: All SMS command handlers
- **agents/**: AI agent implementations

## Development Guidelines

- Read `CLAUDE.md` for complete development guidelines
- Read `AGENTS.md` for agent system overview
- Read `sms-bot/documentation/AGENT-PIPELINE.md` for agent patterns
- Follow the strict module boundaries defined in architecture
- Never hardcode credentials - always use environment variables
- All database operations go through storage-manager.ts

## Agent Development

To create a new agent:

1. Create handler in `sms-bot/commands/`
2. Implement agent in `sms-bot/agents/`
3. Choose: Autonomous (claude-agent-sdk) or Scripted workflow
4. Follow patterns in existing agents
5. Register in command index

See `sms-bot/documentation/AGENT-PIPELINE.md` for detailed instructions.

## Testing

```bash
# Run SMS bot tests
cd sms-bot
npm test

# Test specific agent
npm run test:agent <agent-name>
```

## Documentation

Key documentation files:

- `CLAUDE.md` - Complete development guidelines
- `AGENTS.md` - Agent system overview
- `sms-bot/documentation/AGENT-PIPELINE.md` - Agent development patterns
- `sms-bot/documentation/DEV_SETUP.md` - Development setup guide
- `sms-bot/documentation/security_practices.md` - Security guidelines
- `sms-bot/documentation/ZAD-API-REFERENCE.md` - ZAD system reference

## Deployment

The production system runs on Railway:

1. Push to `main` branch
2. Railway auto-deploys
3. Environment variables configured in Railway dashboard
4. SMS listener runs as persistent service

## What's Not Included

This is a minimal clone for candidate review. The following are excluded:

- Discord bot integration
- Webtoys OS (community desktop)
- Most web app pages (kept only report-viewer and music-player)
- Build artifacts (dist/, .next/, node_modules/)
- Data files and logs
- Development machine specific configurations
- Test scripts and experimental code

## Questions?

For questions about the codebase, see:
- Architecture details in `CLAUDE.md`
- Agent system in `AGENTS.md`
- Technical docs in `sms-bot/documentation/`

---

**This is a candidate review copy of the kochi.to codebase.**
The full production system includes additional components not present in this repository.
