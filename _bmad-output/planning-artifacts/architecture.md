---
stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8]
inputDocuments:
  - "/_bmad-output/planning-artifacts/prd.md"
  - "/_bmad-output/planning-artifacts/product-brief-team-management-2026-03-12.md"
  - "/_bmad-output/planning-artifacts/ux-design-specification.md"
workflowType: 'architecture'
project_name: 'team-management'
user_name: 'op3616'
date: '2026-03-13'
lastStep: 8
status: 'complete'
completedAt: '2026-03-13'
---

# Architecture Decision Document

_This document builds collaboratively through step-by-step discovery. Sections are appended as we work through each architectural decision together._

## Project Context Analysis

### Requirements Overview

**Functional Requirements:**
37 FRs covering user authentication, quest/chapter/task management, XP/progression system, guild/team management, activity feed, badge system, analytics, Linear import, and administration. Core value: gamified team task management.

**Non-Functional Requirements:**
- Performance: <2s page load (p95), <200ms API response (p95)
- Security: TLS 1.3, bcrypt (cost 12), JWT 7-day expiry, rate limiting (100 req/min)
- Scalability: MVP 50 teams → 12-month 500+ teams
- Accessibility: WCAG 2.1 AA, keyboard navigation

**Scale & Complexity:**
- Primary domain: Full-stack SaaS Web Application
- Complexity level: Medium (gamification engine + multi-tenancy)
- Estimated architectural components: 8-12 core modules

### Technical Constraints & Dependencies

- PostgreSQL with connection pooling
- RESTful API (v1, rate limited)
- JWT + OAuth (Google, GitHub) authentication
- Linear OAuth integration for import
- Greenfield project (no legacy constraints)

### Cross-Cutting Concerns Identified

1. **Multi-tenancy**: Logical separation per team (team_id)
2. **Authentication**: JWT with refresh tokens, OAuth providers
3. **RBAC**: Owner, Admin, Member, Viewer roles
4. **Real-time**: Activity feed (polling-based MVP, WebSocket post-MVP)
5. **Gamification Engine**: XP rules, badge criteria, level progression

## Starter Template Evaluation

### Primary Technology Domain

Full-stack SaaS Web Application based on project requirements analysis

### Starter Options Considered

- **T3 Stack (create-t3-app)**: Next.js + tRPC + Drizzle + Better Auth + Tailwind - Industry standard
- **Chust3r/next-better-stack**: Next.js + Better Auth + Drizzle + tRPC + TanStack Query

### Selected Starter: T3 Stack

**Rationale for Selection:**
Industry-standard, well-maintained CLI scaffold with end-to-end type safety. Supports Next.js + tRPC + Drizzle + Better Auth + Tailwind.

**Initialization Command:**

```bash
pnpm create t3-app@latest taskquest
# Select: TypeScript, Tailwind, tRPC, Better Auth, Drizzle, PostgreSQL
```

**Or with CLI flags:**
```bash
pnpm dlx create-t3-app@latest --CI --trpc --tailwind --auth --drizzle --dbProvider postgres --appRouter
```

**Note:** T3 Stack uses NextAuth by default. To use Better Auth instead, run:
```bash
pnpm add better-auth
# Then configure in src/server/auth.ts
```

**Environment Variables:**
```env
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/taskquest
BETTER_AUTH_SECRET=your-secret-key
BETTER_AUTH_URL=http://localhost:3000
```

**Architectural Decisions Provided by Starter:**

| Layer | Technology | Decision |
|-------|------------|----------|
| Framework | Next.js 15 | App Router, Server Components |
| Language | TypeScript | Strict mode |
| Auth | Better Auth | JWT sessions, OAuth (Google, GitHub) |
| ORM | Drizzle | PostgreSQL, type-safe queries |
| API | tRPC | Type-safe client-server communication |
| State | TanStack Query | Client-side caching, mutations |
| Styling | Tailwind CSS | Utility-first |
| UI | shadcn/ui-ready | Radix primitives, accessible |

**Docker Services for Local Development:**
- PostgreSQL (database)
- (Optional) Redis for session caching

**Project Structure:**
```
├── src/                    # T3 Stack structure
│   ├── app/               # Next.js App Router
│   ├── server/             # tRPC router & API
│   │   ├── api/           # tRPC procedures
│   │   └── auth.ts        # Better Auth config
│   ├── db/                # Drizzle schema
│   ├── components/        # React components
│   └── utils/             # Utilities
├── database/              # Drizzle migrations
└── ...
```

**Note:** Project initialization using this command should be the first implementation story.

## Core Architectural Decisions

### Decision Priority Analysis

**Critical Decisions (Block Implementation):**
- Stack selection (T3 Stack: Next.js 15 + Drizzle + tRPC + Better Auth)
- Database (PostgreSQL via Neon)
- Hosting (Vercel)

**Important Decisions (Shape Architecture):**
- Caching strategy (PostgreSQL → Redis for scale)
- Component organization (feature-based)
- API layer (tRPC)

**Deferred Decisions (Post-MVP):**
- WebSocket for real-time (polling for MVP)
- Redis session caching (add when scaling)
- REST API for Linear integration (add during OAuth implementation)

### Data Architecture

| Decision | Choice | Rationale |
|----------|--------|-----------|
| ORM | Drizzle | Type-safe, lightweight, PostgreSQL-native |
| Validation | Zod | Built into tRPC, excellent DX |
| Caching | PostgreSQL (MVP) | Simplicity, can add Redis at scale |
| Migrations | Drizzle Kit | Declarative, schema-as-source |

**Database Schema Approach:**
- Logical multi-tenancy via `team_id` foreign key
- Row-level security policies for data isolation
- UUID primary keys for distributed systems

### Authentication & Security

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Auth | Better Auth | JWT sessions, OAuth providers, RBAC-ready |
| Session Storage | PostgreSQL | Simpler MVP, swap to Redis at scale |
| Rate Limiting | Next.js Middleware | Built-in, effective for MVP |
| Password Hashing | bcrypt (cost 12) | PRD requirement |

**Security Implementation:**
- JWT 7-day expiry (per PRD)
- CSRF protection via Next.js CSRF tokens
- HTTPS only (TLS 1.3)
- Rate limit: 100 req/min per team

### API & Communication Patterns

| Decision | Choice | Rationale |
|----------|--------|-----------|
| API Layer | tRPC | Type-safe, Zod validation, integrated |
| Documentation | tRPC Panel | Built-in, auto-generated |
| REST | Minimal (Linear OAuth) | Only for external integrations |
| Error Handling | tRPC Error Codes | Standardized, type-safe |

**API Architecture:**
- tRPC routers organized by feature
- Protected procedures for authenticated routes
- Team-scoped procedures with `teamId` context

### Frontend Architecture

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Organization | Feature-based | Best for AI agent consistency |
| State | TanStack Query | Integrated in starter |
| Routing | Next.js App Router | Server Components, nested layouts |
| Forms | React Hook Form + Zod | Type-safe, accessible |

**Component Structure:**
```
src/
├── features/
│   ├── quests/
│   │   ├── components/
│   │   ├── hooks/
│   │   └── server/
│   ├── guilds/
│   ├── users/
│   └── auth/
├── shared/
│   ├── components/
│   ├── hooks/
│   └── lib/
└── app/
```

### Infrastructure & Deployment

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Hosting | Vercel | Best Next.js DX, auto-scaling |
| Database | Neon (PostgreSQL) | Serverless, Drizzle-native, free tier |
| CI/CD | GitHub Actions | Free for repos, native Next.js support |
| Container | Docker Compose | Local dev (app + postgres) |

**Docker Compose (Local):**
```yaml
services:
  app:
    build: .
    ports:
      - "3000:3000"
  postgres:
    image: postgres:16
    environment:
      POSTGRES_DB: taskquest
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
    volumes:
      - postgres_data:/var/lib/postgresql/data
```

### Decision Impact Analysis

**Implementation Sequence:**
1. Initialize project with T3 Stack
2. Configure Neon database and run migrations
3. Swap NextAuth for Better Auth
4. Implement feature-based folder structure
5. Build core domain models (Quest, Guild, User)
6. Add RBAC middleware
7. Deploy to Vercel

**Cross-Component Dependencies:**
- Feature-based structure requires clear domain boundaries
- tRPC procedures need consistent team context extraction
- Multi-tenancy requires `teamId` on all domain queries

## Implementation Patterns & Consistency Rules

### Pattern Categories Defined

**Critical Conflict Points Identified:** 8 areas where AI agents could make different choices

### Naming Patterns

**Database Naming Conventions:**
- Tables: snake_case, plural (users, quest_chapters, guild_members)
- Columns: snake_case (user_id, created_at, xp_amount)
- Foreign keys: snake_case with _id suffix (team_id, user_id)
- Indexes: idx_{table}_{columns} (idx_quests_team_id)

**API Naming Conventions (tRPC):**
- Routers: kebab-case (quests, guilds, users)
- Procedures: camelCase (getQuest, createQuest, updateQuestProgress)
- Input/Output: PascalCase with suffix (QuestInput, QuestOutput)

**Code Naming Conventions:**
- Components: PascalCase (QuestCard, GuildBadge, XpProgressBar)
- Files: kebab-case (quest-card.tsx, auth-provider.tsx)
- Hooks: camelCase with use prefix (useQuest, useGuild)
- Utilities: camelCase (formatXp, calculateLevel)
- Constants: UPPER_SNAKE_CASE (MAX_XP_PER_TASK, QUEST_STATUS)

### Structure Patterns

**Project Organization:**
```
src/
├── features/           # Feature-based (recommended)
│   ├── quests/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── server/    # tRPC router
│   │   └── quests.test.ts
│   └── guilds/
├── shared/
│   ├── components/    # Reusable UI
│   ├── lib/          # Utilities
│   └── db/           # Database config
└── app/              # Next.js pages
```

**Tests:** Co-located with source files (*.test.ts, *.spec.ts)

### Format Patterns

**API Response Formats:**
- tRPC handles this automatically
- Errors: throw tRPC errors with ZodError for validation

**Data Exchange (JSON):**
- API/Client: camelCase (JavaScript standard)
- Database: snake_case (PostgreSQL standard)
- Use Drizzle camelCase plugin for automatic conversion

**Date/Time:**
- Database: TIMESTAMP WITH TIME ZONE
- API: ISO 8601 strings
- Display: Format in UI layer

### Communication Patterns

**State Management:**
- TanStack Query for server state
- React Context for auth state only
- Avoid global state for domain data

**Events:**
- Not used in MVP (polling-based activity feed)
- Future: Use event emitter with namespaced events

### Process Patterns

**Error Handling:**
- tRPC errors for API errors
- Error boundaries for React errors
- Zod for validation errors
- Never expose internal errors to users

**Loading States:**
- TanStack Query useQuery isLoading
- Skeleton screens for initial loads
- Optimistic updates for mutations

### Enforcement Guidelines

**All AI Agents MUST:**
1. Follow Drizzle snake_case schema naming
2. Use tRPC for all API calls (no direct fetch)
3. Place tests co-located with source files
4. Use feature-based folder structure
5. Convert between camelCase (API) and snake_case (DB)

**Pattern Enforcement:**
- ESLint rules for naming
- Prettier for code formatting
- Drizzle camelCase plugin for DB conversion
- Shared types for tRPC procedures

## Project Structure & Boundaries

### Complete Project Directory Structure

```
taskquest/
├── README.md
├── package.json
├── pnpm-lock.yaml
├── tsconfig.json
├── next.config.js / next.config.mjs
├── tailwind.config.ts
├── postcss.config.mjs
├── drizzle.config.ts
├── .env.local
├── .env.example
├── .gitignore
├── .github/
│   └── workflows/
│       └── ci.yml
├── docker-compose.yml
├── vercel.json
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── globals.css
│   │   ├── (auth)/            # Auth routes (grouped)
│   │   │   ├── sign-in/
│   │   │   └── sign-up/
│   │   ├── (dashboard)/       # Protected routes
│   │   │   ├── layout.tsx
│   │   │   ├── quests/
│   │   │   ├── guilds/
│   │   │   └── profile/
│   │   └── api/
│   │       └── trpc/
│   │           └── [trpc]/
│   │               └── route.ts
│   ├── features/               # Feature-based organization
│   │   ├── quests/
│   │   │   ├── components/     # QuestCard, QuestBoard, QuestForm
│   │   │   ├── hooks/         # useQuest, useQuests
│   │   │   ├── server/        # tRPC router
│   │   │   │   ├── quests.ts  # router
│   │   │   │   └── quests.test.ts
│   │   │   ├── schema.ts      # Drizzle schema
│   │   │   └── types.ts       # TypeScript types
│   │   ├── chapters/
│   │   │   ├── components/
│   │   │   ├── hooks/
│   │   │   └── server/
│   │   ├── tasks/
│   │   │   ├── components/
│   │   │   ├── hooks/
│   │   │   └── server/
│   │   ├── guilds/
│   │   │   ├── components/     # GuildCard, GuildMembers, GuildSettings
│   │   │   ├── hooks/
│   │   │   ├── server/
│   │   │   └── schema.ts
│   │   ├── users/
│   │   │   ├── components/
│   │   │   ├── hooks/
│   │   │   ├── server/
│   │   │   └── schema.ts
│   │   ├── auth/               # Better Auth
│   │   │   ├── client.ts       # Auth client config
│   │   │   ├── server.ts       # Auth server config
│   │   │   └── components/     # SignInButton, UserButton
│   │   ├── gamification/
│   │   │   ├── xp.ts           # XP calculations
│   │   │   ├── levels.ts       # Level progression
│   │   │   └── rules.ts        # XP rules engine
│   │   ├── badges/
│   │   │   ├── components/
│   │   │   ├── server/
│   │   │   └── schema.ts
│   │   ├── activity/
│   │   │   ├── components/     # ActivityFeed
│   │   │   ├── hooks/          # useActivity
│   │   │   ├── server/
│   │   │   └── schema.ts
│   │   └── analytics/
│   │       ├── components/
│   │       └── server/
│   ├── shared/                  # Shared code
│   │   ├── components/         # shadcn/ui components
│   │   │   ├── ui/            # button, card, input, etc.
│   │   │   └── forms/
│   │   ├── hooks/              # useDebounce, useMediaQuery
│   │   ├── lib/                # utils, helpers
│   │   │   ├── utils.ts
│   │   │   └── cn.ts           # classnames helper
│   │   ├── db/                 # Database
│   │   │   ├── index.ts        # Drizzle client
│   │   │   ├── schema.ts       # Main schema
│   │   │   └── migrations/     # Drizzle migrations
│   │   └── types/              # Shared types
│   │       └── index.ts
│   ├── server/                  # tRPC setup
│   │   ├── index.ts            # tRPC initialization
│   │   ├── context.ts          # Context (auth, db)
│   │   └── routers/            # Root routers
│   │       ├── index.ts
│   │       └── root.ts
│   └── middleware.ts           # Next.js middleware
├── database/                   # Drizzle
│   ├── schema.ts               # All schemas
│   └── migrations/             # SQL migrations
├── tests/                      # E2E tests
│   └── ...
└── public/                     # Static assets
    └── ...
```

### Architectural Boundaries

**API Boundaries:**
- tRPC: All internal API via `src/server/routers/`
- REST: Only for Linear OAuth callback (`/api/auth/linear/callback`)
- Webhooks: For future integrations

**Component Boundaries:**
- Features own their components, hooks, and tRPC routers
- Shared UI in `src/shared/components/ui/`
- No cross-feature imports without explicit exports

**Service Boundaries:**
- tRPC routers = service layer
- Database access only through tRPC procedures
- No direct DB access from components

**Data Boundaries:**
- Drizzle schema = single source of truth
- camelCase in API, snake_case in DB (via Drizzle plugin)
- Multi-tenancy: all queries filter by `teamId`

### Requirements to Structure Mapping

| FR Category | Feature | Key Files |
|-------------|---------|-----------|
| User Auth | `features/auth/` | auth/server.ts, auth/client.ts |
| Quest Management | `features/quests/` | quests/server/quests.ts |
| XP System | `features/gamification/` | gamification/xp.ts, levels.ts |
| Guild/Team | `features/guilds/` | guilds/server/, schema.ts |
| Activity Feed | `features/activity/` | activity/server/, hooks/useActivity |
| Badges | `features/badges/` | badges/server/, schema.ts |
| Analytics | `features/analytics/` | analytics/server/ |

### Integration Points

**Internal Communication:**
- tRPC for client-server communication
- TanStack Query hooks for data fetching
- React Context for auth state only

**External Integrations:**
- Linear OAuth: `/api/auth/linear/*`
- Google/GitHub OAuth: via Better Auth
- Future: Webhooks for notifications

**Data Flow:**
```
UI Components → tRPC Hooks → tRPC Router → Drizzle → PostgreSQL
                    ↓
            Better Auth (session)
```

### File Organization Patterns

**Configuration:** Root directory (next.config, drizzle.config, etc.)  
**Source:** `src/` with feature-based organization  
**Tests:** Co-located (`*.test.ts` next to source)  
**Database:** `database/migrations/` for Drizzle  

### Development Workflow Integration

**Dev:** `pnpm dev` runs Next.js + connects to local Postgres  
**Build:** `pnpm build` runs typecheck, lint, then Next.js build  
**Deploy:** Vercel auto-deploys from main branch  

## Architecture Validation Results

### Coherence Validation ✅

**Decision Compatibility:**
All technology choices are compatible: Next.js 15 (App Router) + Drizzle ORM + Better Auth + tRPC + TanStack Query + Tailwind CSS + shadcn/ui. All packages work together without version conflicts. Type-safe stack ensures consistent development.

**Pattern Consistency:**
Implementation patterns fully align with technology choices:
- Drizzle snake_case schema matches PostgreSQL conventions
- tRPC procedures follow consistent naming
- Feature-based structure matches TanStack Query patterns

**Structure Alignment:**
Project structure supports all architectural decisions:
- Feature folders contain components, hooks, and tRPC routers
- Shared code separated for reusability
- Database migrations in dedicated folder

### Requirements Coverage Validation ✅

**Functional Requirements Coverage:**
All 37 FRs architecturally supported:
- Auth: features/auth/ with Better Auth
- Quests: features/quests/ with full CRUD
- XP System: features/gamification/ with XP and levels
- Guilds: features/guilds/ for team management
- Badges: features/badges/ for achievements
- Activity: features/activity/ for feed

**Non-Functional Requirements Coverage:**
- Performance: Vercel edge network + Neon serverless DB
- Security: JWT 7-day expiry, bcrypt cost 12, rate limiting
- Scalability: Logical multi-tenancy, horizontal scaling ready
- Accessibility: shadcn/ui WCAG-compliant components

### Implementation Readiness Validation ✅

**Decision Completeness:**
All critical decisions documented with versions and rationale. Technology stack fully specified.

**Structure Completeness:**
Complete directory structure with all key files defined. Integration points clearly mapped.

**Pattern Completeness:**
8 pattern categories covering naming, structure, format, communication, and process patterns.

### Gap Analysis Results

No critical gaps identified. Architecture is complete and ready for implementation.

### Validation Issues Addressed

No issues found during validation.

### Architecture Completeness Checklist

**✅ Requirements Analysis**
- [x] Project context thoroughly analyzed
- [x] Scale and complexity assessed
- [x] Technical constraints identified
- [x] Cross-cutting concerns mapped

**✅ Architectural Decisions**
- [x] Critical decisions documented with versions
- [x] Technology stack fully specified
- [x] Integration patterns defined
- [x] Performance considerations addressed

**✅ Implementation Patterns**
- [x] Naming conventions established
- [x] Structure patterns defined
- [x] Communication patterns specified
- [x] Process patterns documented

**✅ Project Structure**
- [x] Complete directory structure defined
- [x] Component boundaries established
- [x] Integration points mapped
- [x] Requirements to structure mapping complete

### Architecture Readiness Assessment

**Overall Status:** READY FOR IMPLEMENTATION

**Confidence Level:** HIGH

**Key Strengths:**
- Type-safe end-to-end (TypeScript + tRPC + Drizzle + Zod)
- Feature-based architecture for AI agent consistency
- Multi-tenancy built-in from the start
- Clear component boundaries and integration points
- Comprehensive patterns prevent implementation conflicts

**Areas for Future Enhancement:**
- Real-time activity feed (WebSocket post-MVP)
- Session caching (Redis at scale)
- Additional analytics features

### Implementation Handoff

**AI Agent Guidelines:**
- Follow all architectural decisions exactly as documented
- Use implementation patterns consistently across all components
- Respect project structure and boundaries
- Refer to this document for all architectural questions

**First Implementation Priority:**
```bash
pnpm create t3-app@latest taskquest
# Select: TypeScript, Tailwind, tRPC, Auth, Drizzle, PostgreSQL

cd taskquest
pnpm add better-auth
# Configure Better Auth in src/server/auth.ts
```
