# Story 1.2: OAuth Sign-In

Status: done

<!-- Note: Validation is optional. Run validate-create-story for quality check before dev-story. -->

## Story

As a user,
I want to sign in using Google or GitHub OAuth,
so that I can quickly access the platform without creating a new password.

## Acceptance Criteria

1. **Given** I am on the sign-in page
   **When** I click "Sign in with Google"
   **Then** I am redirected to Google OAuth
   **And** after authorization, I am returned to the dashboard

2. **Given** I am on the sign-in page
   **When** I click "Sign in with GitHub"
   **Then** I am redirected to GitHub OAuth
   **And** after authorization, I am returned to the dashboard

## Tasks / Subtasks

- [x] Task 1: Add OAuth providers to Better Auth config (AC: #1, #2)
  - [x] 1.1: Configure Google OAuth provider
  - [x] 1.2: Configure GitHub OAuth provider
  - [x] 1.3: Add OAuth environment variables documentation
- [x] Task 2: Create OAuth sign-in UI (AC: #1, #2)
  - [x] 2.1: Add OAuth buttons to sign-in page at src/app/(auth)/sign-in/page.tsx
  - [x] 2.2: Create OAuthButton component for provider buttons
  - [x] 2.3: Add OAuth button styling (matching registration page)
- [x] Task 3: Handle OAuth callback (AC: #1, #2)
  - [x] 3.1: Verify Better Auth OAuth callback handling
  - [x] 3.2: Handle successful OAuth sign-in and redirect to dashboard
  - [x] 3.3: Handle OAuth errors gracefully

## Dev Notes

- **Authentication**: Uses Better Auth OAuth for Google and GitHub
- **OAuth Providers**: Google OAuth 2.0, GitHub OAuth
- **Redirect**: After successful OAuth, redirect to dashboard
- **User Creation**: Better Auth automatically creates user on first OAuth sign-in
- **Account Linking**: Users can link multiple OAuth providers to same account (Better Auth feature)

### Project Structure Notes

- Sign-in page location: `src/app/(auth)/sign-in/page.tsx`
- Auth feature location: `src/features/auth/`
- Use shadcn/ui components from `src/shared/components/ui/`
- Feature-based organization required (per architecture)

### References

- [Source: planning-artifacts/epics.md#Story-1.2]
- [Source: planning-artifacts/architecture.md - Authentication & Security]
- [Source: planning-artifacts/architecture.md - Project Structure & Boundaries]

## Dev Agent Guardrails

### Technical Requirements

1. **Must use Better Auth** - Already configured in project from Story 1.0
2. **Must use tRPC** - All API calls must go through tRPC procedures
3. **Must use Drizzle** - Database operations via Drizzle ORM
4. **Must use feature-based structure** - Place auth components in `src/features/auth/`
5. **Must use React Hook Form + Zod** - For form handling and validation
6. **Must use TanStack Query** - For data fetching mutations

### Architecture Compliance

- Follow folder structure: `src/features/auth/components/`, `src/features/auth/server/`
- Use tRPC for API calls (no direct fetch)
- Use Drizzle camelCase plugin for DB conversion
- All database: snake_case, API: camelCase
- Multi-tenancy ready: prepare for team_id in future stories

### Library/Framework Requirements

| Layer | Technology | Version |
|-------|------------|---------|
| Framework | Next.js | 15.x |
| Language | TypeScript | Strict mode |
| Auth | Better Auth | Latest |
| OAuth Providers | Google, GitHub | Latest |
| ORM | Drizzle | Latest |
| API | tRPC | Latest |
| Forms | React Hook Form + Zod | Latest |
| State | TanStack Query | Latest |
| Styling | Tailwind CSS | Latest |
| UI Components | shadcn/ui | Latest |

### File Structure Requirements

```
src/
├── app/
│   └── (auth)/
│       └── sign-in/
│           └── page.tsx      # Sign-in page (update with OAuth buttons)
├── features/
│   └── auth/
│       ├── components/       # Auth UI components
│       │   ├── oauth-button.tsx
│       │   └── sign-in-form.tsx  # Update to include OAuth
│       ├── hooks/           # Auth hooks
│       │   └── use-oauth-sign-in.ts
│       └── server/
│           └── auth.ts      # Update with OAuth providers
└── shared/
    └── components/
        └── ui/              # shadcn/ui components
```

### Environment Variables Required

```env
# OAuth Providers (to be added)
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
GITHUB_CLIENT_ID=your-github-client-id
GITHUB_CLIENT_SECRET=your-github-client-secret

# Already configured from Story 1.0
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/taskquest
BETTER_AUTH_SECRET=your-secret-key
BETTER_AUTH_URL=http://localhost:3000
```

### Testing Requirements

- Unit tests for OAuth configuration
- Unit tests for OAuth callback handling
- Co-located tests: `*.test.ts` next to source files
- Use Vitest for unit tests
- Use Playwright for E2E tests (OAuth sign-in flow)

## Previous Story Intelligence

**From Story 1.1: User Registration**

- **Tech Stack Established**: Next.js 15 + tRPC + Drizzle + Better Auth + Tailwind
- **Auth Configured**: Better Auth email/password already working
- **Project Structure**: Feature-based folders in src/features/auth/
- **Pattern Established**: React Hook Form + Zod for forms, tRPC for API

**Key Learnings for OAuth Sign-In:**

- Better Auth is already set up - add OAuth providers to existing config
- Follow same patterns as Story 1.1 for UI components
- Use the existing sign-in page location: src/app/(auth)/sign-in/page.tsx
- OAuth buttons should match the styling of the registration page

**Files Already Created (Story 1.1):**

- `src/features/auth/components/sign-up-form.tsx` - Reference for form component structure
- `src/features/auth/hooks/use-sign-up.ts` - Reference for auth hook pattern
- `src/features/auth/server/auth.ts` - Update this with OAuth providers

**From Story 1.0: Project Setup - Initialize T3 Stack**

- **Better Auth Configured**: Already in src/server/better-auth/ or src/server/auth.ts
- **Auth Tables Created**: user, session, account, verification tables exist
- **Database Ready**: PostgreSQL on port 5432
- **Environment Variables**: BETTER_AUTH_SECRET, BETTER_AUTH_URL configured

## Git Intelligence Summary

Git repository exists with Story 1.1 implementation files.

Recent work patterns:
- T3 Stack project initialization
- PostgreSQL Docker container setup
- Database migrations
- Email/password authentication implementation
- React Hook Form + Zod integration
- tRPC procedure creation

## Latest Tech Information

### Better Auth OAuth (2026)

**OAuth Configuration:**
```typescript
import { betterAuth } from "better-auth"

const auth = betterAuth({
  emailAndPassword: {
    enabled: true
  },
  googleOAuth: {
    enabled: true,
    clientId: process.env.GOOGLE_CLIENT_ID,
    clientSecret: process.env.GOOGLE_CLIENT_SECRET
  },
  githubOAuth: {
    enabled: true,
    clientId: process.env.GITHUB_CLIENT_ID,
    clientSecret: process.env.GITHUB_CLIENT_SECRET
  }
})
```

**Client-side OAuth Sign-In:**
```typescript
import { authClient } from "@/features/auth/client"

// Google OAuth
await authClient.signIn.google()

// GitHub OAuth
await authClient.signIn.github()
```

**OAuth Callback:**
- Better Auth handles OAuth callback automatically
- After successful OAuth, user is created in database with account record
- Redirect to dashboard after successful authentication

### OAuth Provider Setup

**Google OAuth:**
1. Go to Google Cloud Console
2. Create OAuth 2.0 credentials
3. Set authorized redirect URI: `{BETTER_AUTH_URL}/api/auth/callback/google`
4. Copy client ID and secret to environment variables

**GitHub OAuth:**
1. Go to GitHub Developer Settings
2. Create OAuth App
3. Set callback URL: `{BETTER_AUTH_URL}/api/auth/callback/github`
4. Copy client ID and secret to environment variables

### UX Patterns

**OAuth Buttons:**
- Show OAuth providers as buttons with provider logos
- Use consistent styling with registration page
- Show loading state during OAuth redirect

**Error Handling:**
- Handle OAuth errors (user denied, account already exists with different provider)
- Show user-friendly error messages
- Allow retry on failure

## Project Context Reference

**Project**: team-management (TaskQuest)
**Tech Stack**: T3 Stack (Next.js 15 + tRPC + Drizzle + Better Auth + Tailwind)
**Database**: PostgreSQL (Neon for production, local Docker for dev)
**Architecture**: Feature-based folder structure with multi-tenancy support

**From PRD**:
- FR2: Users can sign in via OAuth (Google, GitHub)
- Security: JWT 7-day expiry, rate limiting 100 req/min

**From Architecture**:
- All API via tRPC
- Feature-based structure required
- Follow naming conventions: snake_case (DB), camelCase (API), PascalCase (Components)

## References

- [Source: planning-artifacts/epics.md#Story-1.2]
- [Source: planning-artifacts/architecture.md - Authentication & Security]
- [Source: planning-artifacts/architecture.md - Implementation Patterns & Consistency Rules]
- [Source: planning-artifacts/architecture.md - Project Structure & Boundaries]
- [Source: implementation-artifacts/1-1-user-registration.md]

## Dev Agent Record

### Agent Model Used

opencode/minimax-m2.5-free

### Debug Log References

### Completion Notes List

- Ultimate context engine analysis completed - comprehensive developer guide created
- Story file ready for dev-story execution
- Epic 1 already in-progress status (from Story 1.0)
- ✅ Added Google OAuth to Better Auth config (src/server/better-auth/config.ts)
- ✅ Added Google OAuth env vars to env.js
- ✅ Created OAuthButton component with Google and GitHub icons
- ✅ Created SignInForm component with email/password and OAuth buttons
- ✅ Created sign-in page at src/app/(auth)/sign-in/page.tsx
- ✅ Added OAuth buttons with loading states and error handling
- ✅ All lint and typecheck passes
- **Code Review Fixes Applied:**
  - ✅ Added user-facing error feedback to OAuthButton component
  - ✅ Fixed Google OAuth to only enable when credentials are provided
  - ✅ Fixed hardcoded redirect URI to use BETTER_AUTH_URL env variable
  - ✅ Added unit tests for OAuthButton and SignInForm components

### File List

**Created:**
- `src/features/auth/components/oauth-button.tsx` - OAuth button component with Google and GitHub icons
- `src/features/auth/components/sign-in-form.tsx` - Sign-in form with email/password and OAuth
- `src/app/(auth)/sign-in/page.tsx` - Sign-in page
- `tests/unit/oauth-button.test.tsx` - Unit tests for OAuthButton component
- `tests/unit/sign-in-form.test.tsx` - Unit tests for SignInForm component

**Modified:**
- `src/server/better-auth/config.ts` - Added Google OAuth provider with env-based config
- `src/env.js` - Added Google OAuth environment variables
- `.env` - Added Google OAuth placeholder variables

## Change Log

- 2026-03-13: Story 1.2 created - OAuth Sign-In comprehensive context prepared
  - Extracted acceptance criteria from epics.md
  - Included previous story learnings from Story 1.1
  - Documented Better Auth OAuth configuration
  - Provided OAuth provider setup instructions
  - Specified file structure following architecture patterns
- 2026-03-13: Implemented OAuth Sign-In feature
  - Added Google OAuth to Better Auth configuration
  - Created OAuth button component with Google and GitHub provider icons
  - Created sign-in form with email/password and OAuth buttons
  - Created sign-in page at src/app/(auth)/sign-in/page.tsx
  - Added Google OAuth environment variables
  - All lint and typecheck passes
- 2026-03-13: Code review fixes
  - Added user-facing error feedback to OAuthButton component
  - Fixed Google OAuth to only enable when credentials are provided
  - Fixed hardcoded redirect URI to use BETTER_AUTH_URL env variable
  - Added unit tests for OAuthButton and SignInForm components
