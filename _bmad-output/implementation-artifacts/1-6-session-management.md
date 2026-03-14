# Story 1.6: Session Management

Status: done

<!-- Note: Validation is optional. Run validate-create-story for quality check before dev-story. -->

## Story

As a user,
I want sessions to expire after 7 days of inactivity,
so that my account remains secure.

## Acceptance Criteria

1. **Given** I am logged in, **When** I am inactive for 7 days, **Then** my session expires, **And** I am redirected to the sign-in page

2. **Given** I am logged in, **When** I use the application within 7 days, **Then** my session is extended, **And** I remain logged in

## Tasks / Subtasks

- [x] Task 1: Implement session expiry after 7 days of inactivity (AC: 1)
  - [x] Task 1.1: Configure Better Auth session expiry to 7 days
  - [x] Task 1.2: Implement session refresh on user activity
  - [x] Task 1.3: Add redirect to sign-in page when session expires
- [x] Task 2: Implement session extension on activity (AC: 2)
  - [x] Task 2.1: Track last activity timestamp
  - [x] Task 2.2: Extend session on API calls/user actions
  - [x] Task 2.3: Verify session persistence across page navigation

## Dev Notes

### Project Structure Notes

- **Auth Configuration**: `src/features/auth/` - Better Auth configuration
- **Session Storage**: Uses Better Auth's built-in session management (PostgreSQL)
- **Middleware**: Session validation handled in Next.js middleware or Better Auth hooks
- **Sign-in Page**: `src/app/(auth)/sign-in/page.tsx`
- **tRPC Context**: Session available in tRPC context for protected procedures

### Architecture Compliance

- **Framework**: Next.js 15 with App Router
- **API Layer**: tRPC (no direct fetch)
- **Database**: Drizzle ORM with PostgreSQL
- **Authentication**: Better Auth with JWT sessions
- **Security**: JWT 7-day expiry (PRD requirement), bcrypt cost 12
- **State**: TanStack Query for data fetching
- **Styling**: Tailwind CSS
- **Naming**: camelCase for API/TypeScript, snake_case for database columns

### Technical Requirements

- Configure Better Auth session expiry to 7 days (604800 seconds)
- Track last activity timestamp or rely on Better Auth's built-in session management
- Session should automatically refresh on any authenticated API call
- Handle session expiry gracefully - redirect to sign-in with message
- Ensure session extension works across browser sessions (consider "remember me" functionality)
- Test session expiry edge cases: exactly 7 days, after 7 days, before 7 days
- Consider refresh token rotation if using long-lived sessions

### Library/Framework Requirements

- Better Auth for authentication and session management
- tRPC protected procedures automatically validate sessions
- React Context for auth state (as per architecture)
- TanStack Query for any session-related queries (if needed)
- Tailwind CSS for styling

### Testing Requirements

- Unit tests for session expiry configuration
- Unit tests for session refresh logic
- E2E tests for session expiry flow (mock time or use test accounts)
- E2E tests for session extension on activity

### Previous Story Learnings

From Story 1.5 (View XP and Progress):
- Feature-based structure: `src/features/gamification/` for XP/levels
- Profile page at `src/app/profile/page.tsx`
- Feature folders contain components, hooks, and tRPC routers
- Auth uses Better Auth, configured in `src/features/auth/`
- Test patterns: unit tests for utilities, E2E for user flows

From Story 1.4 (Profile Management):
- User data stored in `users` table
- Profile management uses React Hook Form + Zod for validation
- Avatar upload was deferred - similar approach may apply for session settings
- tRPC procedures follow pattern in `src/features/users/server/users.ts`

### Security Considerations

- JWT tokens expire after 7 days (per PRD requirement)
- Rate limiting: 100 requests/minute per team
- CSRF protection via Next.js CSRF tokens
- HTTPS only (TLS 1.3)

## References

- [Source: _bmad-output/planning-artifacts/epics.md#Story-1.6-Session-Management]
- [Source: _bmad-output/planning-artifacts/architecture.md#Authentication-Security]
- [Source: _bmad-output/planning-artifacts/architecture.md#Starter-Template-Evaluation]
- [Source: _bmad-output/planning-artifacts/architecture.md#Project-Structure-Patterns]
- [Source: _bmad-output/planning-artifacts/epics.md#Functional-Requirements]
- [Source: _bmad-output/planning-artifacts/prd.md#Security]
- [Source: _bmad-output/planning-artifacts/architecture.md#Requirements-to-Structure-Mapping]

## Dev Agent Record

### Agent Model Used

opencode/minimax-m2.5-free

### Debug Log References

- TypeScript compilation successful (0 errors in new code)
- All 92 unit tests pass
- Pre-existing TypeScript errors in sign-in-form.test.tsx (unrelated to this story)

### Completion Notes List

- Implemented session expiry configuration in Better Auth with 7-day idle timeout
- Created session utilities for expiry checking, time calculation, and formatting
- Implemented client-side session manager hook that:
  - Checks session status every minute
  - Refreshes session when user is active (mousedown, keydown, touchstart)
  - Redirects to sign-in with "session_expired" reason when session expires
- Created API endpoints:
  - GET /api/auth/get-session - returns current session status
  - POST /api/auth/refresh-session - extends session expiry by 7 days
- Created SessionProvider component that wraps the app
- Updated root layout to include SessionProvider
- Added unit tests for session utility functions
- **Post-review fixes applied:**
  - Removed auto-refresh logic (only refresh on user activity)
  - Added 5-second debounce to prevent API spam on activity
  - Removed scroll from activity events to reduce unnecessary refresh calls
  - Added session-manager logic tests

### File List

New files:
- src/features/auth/server/session-utils.ts (pure session utility functions)
- src/features/auth/server/session.ts (session management with DB)
- src/features/auth/hooks/use-session-manager.ts (client-side session management hook)
- src/features/auth/components/session-provider.tsx (React context provider)
- src/app/_components/client-providers.tsx (combines TRPC and Session providers)
- src/app/api/auth/get-session/route.ts (GET endpoint to check session)
- src/app/api/auth/refresh-session/route.ts (POST endpoint to refresh session)
- tests/unit/session.test.ts (unit tests for session utilities)
- tests/unit/session-manager.test.ts (unit tests for session manager logic)

Modified files:
- src/server/better-auth/config.ts (added sessionExpiresIn configuration)
- src/app/layout.tsx (added ClientProviders wrapper)

## Change Log

- 2026-03-14: Initial implementation of session management feature
