# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Common Commands

### Setup & Development
```bash
# Initial setup - fills in required .env files and installs dependencies
yarn setup

# Development - run all services concurrently
yarn dev:all

# Development - run services separately
yarn dev:server    # Start server (port 3001)
yarn dev:frontend  # Start frontend (port 3000)
yarn dev:collector # Start document collector (port 8888)

# Production builds
yarn prod:frontend  # Build frontend for production
yarn prod:server    # Start server in production mode
```

### Database Operations
```bash
# Prisma database operations
yarn prisma:generate  # Generate Prisma client
yarn prisma:migrate   # Run database migrations
yarn prisma:seed      # Seed database with initial data
yarn prisma:setup     # Complete setup (generate + migrate + seed)
yarn prisma:reset     # Reset database and re-migrate
```

### Testing & Quality
```bash
yarn test  # Run Jest tests
yarn lint  # Run ESLint across all projects (server, frontend, collector)
```

## Architecture Overview

AnythingLLM is a monorepo with six main components:

### Core Services
- **frontend/**: React + Vite application (UI layer)
- **server/**: Node.js Express server (API, LLM interactions, vector DB management)
- **collector/**: Node.js Express server (document processing and parsing)

### Additional Components
- **docker/**: Docker configuration and deployment files
- **embed/**: Submodule for embeddable chat widget
- **browser-extension/**: Submodule for Chrome extension

### Key Concepts
- **Workspaces**: Containerized document collections that function like threads
- **Multi-modal support**: Handles text, images, and various document types
- **Provider flexibility**: Supports multiple LLM providers, vector databases, and embedding models
- **Multi-user support**: Role-based access control (Docker version)

## Important Configuration

### Environment Files
After running `yarn setup`, configure these files:
- `server/.env.development` - **Critical**: Server configuration
- `frontend/.env` - Frontend environment variables
- `collector/.env` - Document collector configuration
- `docker/.env` - Docker deployment settings

### Database
- Uses Prisma ORM with SQLite by default
- Database file: `server/storage/anythingllm.db`
- Migrations in `server/prisma/migrations/`

## Key Directories

### Server Structure
- `server/models/` - Database models and business logic
- `server/utils/AiProviders/` - LLM provider integrations
- `server/utils/EmbeddingEngines/` - Embedding model integrations
- `server/utils/vectorDbProviders/` - Vector database integrations
- `server/endpoints/` - API route handlers
- `server/storage/` - File storage, models, and documents

### Frontend Structure
- `frontend/src/components/` - Reusable UI components
- `frontend/src/pages/` - Page components
- `frontend/src/models/` - API interaction models
- `frontend/src/utils/` - Utility functions and helpers

### Document Processing
- `collector/` - Handles document ingestion and processing
- `server/storage/documents/` - Document storage location
- Supports PDF, TXT, DOCX, audio, video, and more

## Development Notes

### Port Configuration
- Frontend: 3000
- Server: 3001  
- Collector: 8888

### Testing
- Uses Jest for unit testing
- Test files in `__tests__/` directories
- Run `yarn test` from root to execute all tests

### Linting
- ESLint configured for all projects
- Run `yarn lint` to check all code
- Each subproject has its own linting configuration