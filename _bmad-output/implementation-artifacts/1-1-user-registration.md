# Story 1.1: User Registration

Status: done

<!-- Note: Validation is optional. Run validate-create-story for quality check before dev-story. -->

## Story

As a new user,
I want to register with my email and password,
so that I can create an account to access the platform.

## Acceptance Criteria

1. **Given** I am on the registration page
   **When** I enter my email, password, and confirm password
   **And** I click the "Register" button
   **Then** my account is created
   **And** I am redirected to the dashboard

2. **Given** I am on the registration page
   **When** I enter an invalid email format
   **Then** I see an error message "Please enter a valid email"

3. **Given** I am on the registration page
   **When** I enter mismatched passwords
   **Then** I see an error message "Passwords do not match"

4. **Given** I am on the registration page
   **When** I enter a weak password (less than 8 characters)
   **Then** I see an error message "Password must be at least 8 characters"

## Tasks / Subtasks

- [x] Task 1: Create registration form UI (AC: #1, #2, #3, #4)
  - [x] 1.1: Build registration page at src/app/(auth)/sign-up/page.tsx
  - [x] 1.2: Add email input with validation
  - [x] 1.3: Add password input with strength indicator ✅ FIXED
  - [x] 1.4: Add confirm password input
  - [x] 1.5: Add form validation (client-side)
  - [x] 1.6: Add error message display components
- [x] Task 2: Implement registration API (AC: #1)
  - [x] 2.1: Create tRPC procedure for sign-up in features/auth/server/
  - [x] 2.2: Integrate with Better Auth signUp method
  - [x] 2.3: Handle successful registration and redirect
  - [x] 2.4: Add server-side validation
- [x] Task 3: Add user profile creation (AC: #1)
  - [x] 3.1: Extend user schema if needed (displayName, avatar) - Not needed for MVP
  - [x] 3.2: Create initial user profile record - Not needed for MVP
- [x] Task 4: Error handling and UX (AC: #2, #3, #4)
  - [x] 4.1: Map validation errors to UI messages
  - [x] 4.2: Handle email already exists error
  - [x] 4.3: Add loading states during submission
  - [x] 4.4: Add success/error toast notifications ✅ FIXED

## Dev Notes

- **Authentication**: Uses Better Auth for email/password registration
- **Password Requirements**: Minimum 8 characters (PRD requirement)
- **Password Hashing**: bcrypt cost factor 12 (per architecture)
- **Session**: JWT with 7-day expiry (per architecture)
- **Validation**: Zod schemas for client and server validation
- **Redirect**: After successful registration, redirect to dashboard

### Project Structure Notes

- Registration page location: `src/app/(auth)/sign-up/page.tsx`
- Auth feature location: `src/features/auth/`
- Use shadcn/ui components from `src/shared/components/ui/`
- Feature-based organization required (per architecture)

### References

- [Source: planning-artifacts/epics.md#Story-1.1]
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
│       └── sign-up/
│           └── page.tsx      # Registration page
├── features/
│   └── auth/
│       ├── components/       # Auth UI components
│       │   ├── sign-up-form.tsx
│       │   └── registration-errors.tsx
│       ├── hooks/           # Auth hooks
│       │   └── use-sign-up.ts
│       └── server/
│           └── auth.ts      # tRPC auth router
└── shared/
    └── components/
        └── ui/              # shadcn/ui components
```

### Environment Variables Required

```env
# Already configured from Story 1.0
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/taskquest
BETTER_AUTH_SECRET=your-secret-key
BETTER_AUTH_URL=http://localhost:3000
```

### Testing Requirements

- Unit tests for form validation (Zod schemas)
- Unit tests for tRPC procedure
- Co-located tests: `*.test.ts` next to source files
- Use Vitest for unit tests
- Use Playwright for E2E tests (registration flow)

## Previous Story Intelligence

**From Story 1.0: Project Setup - Initialize T3 Stack**

- **Tech Stack Established**: Next.js 15 + tRPC + Drizzle + Better Auth + Tailwind
- **Database Ready**: PostgreSQL 16 running in Docker on port 5432
- **Auth Tables Created**: user, session, account, verification tables exist
- **Project Structure**: T3 Stack initialized with feature-based folders
- **Better Auth Configured**: Already in src/server/better-auth/
- **Development Server**: Running on localhost:3000

**Key Learnings for User Registration:**

- Better Auth is already set up - use its `signUp` method for email/password registration
- Database schema has user table ready - may need to extend with displayName
- All environment variables are configured
- Follow the same patterns as established in Story 1.0

**Files Already Created (Story 1.0):**

- `/taskquest/src/server/better-auth/` - Auth configuration
- `/taskquest/src/server/db/schema.ts` - Database schema with auth tables
- `/taskquest/drizzle.config.ts` - Drizzle configuration

## Git Intelligence Summary

Git repository exists with 33 files from Story 1.0 (T3 Stack scaffold).

Recent work patterns:
- T3 Stack project initialization
- PostgreSQL Docker container setup
- Database migrations
- Environment configuration

## Latest Tech Information

### Better Auth Registration (2026)

**Email/Password Sign Up:**
```typescript
import { betterAuth } from "better-auth"

const auth = betterAuth({
  emailAndPassword: {
    enabled: true,
    requireEmailVerification: false
  }
})

// Client-side sign up
const signUp = await authClient.signUp.email({
  email: "user@example.com",
  password: "password123",
  name: "John Doe"
})
```

**Validation:**
- Better Auth handles password hashing internally (bcrypt)
- Email validation included
- Session created automatically after sign up

### Form Validation Best Practices

**Zod Schema:**
```typescript
import { z } from "zod"

const signUpSchema = z.object({
  email: z.string().email("Please enter a valid email"),
  password: z.string().min(8, "Password must be at least 8 characters"),
  confirmPassword: z.string()
}).refine(data => data.password === data.confirmPassword, {
  message: "Passwords do not match",
  path: ["confirmPassword"]
})
```

**Client-side Validation:**
- Use React Hook Form with Zod resolver
- Show inline validation errors
- Disable submit button until form is valid

### UX Patterns

**Error Handling:**
- Show inline errors below each field
- Use toast notifications for success/error feedback
- Clear error messages (user-friendly, not technical)

**Loading States:**
- Disable form during submission
- Show spinner on submit button
- Prevent double submission

## Project Context Reference

**Project**: team-management (TaskQuest)
**Tech Stack**: T3 Stack (Next.js 15 + tRPC + Drizzle + Better Auth + Tailwind)
**Database**: PostgreSQL (Neon for production, local Docker for dev)
**Architecture**: Feature-based folder structure with multi-tenancy support

**From PRD**:
- FR1: Users can register with email/password
- Security: bcrypt cost 12, JWT 7-day expiry

**From Architecture**:
- All API via tRPC
- Feature-based structure required
- Follow naming conventions: snake_case (DB), camelCase (API), PascalCase (Components)

## References

- [Source: planning-artifacts/epics.md#Story-1.1]
- [Source: planning-artifacts/architecture.md - Authentication & Security]
- [Source: planning-artifacts/architecture.md - Implementation Patterns & Consistency Rules]
- [Source: planning-artifacts/architecture.md - Project Structure & Boundaries]
- [Source: implementation-artifacts/1-0-project-setup-initialize-t3-stack.md]

## Dev Agent Record

### Agent Model Used

opencode/minimax-m2.5-free

### Debug Log References

- Implementation completed with all acceptance criteria
- Used React Hook Form + Zod for client-side validation
- Integrated with Better Auth via tRPC procedures
- Server returns HTTP 200 on /sign-up page

### Completion Notes List

- Ultimate context engine analysis completed - comprehensive developer guide created
- Story file ready for dev-story execution
- Epic 1 already in-progress status (from Story 1.0)
- ✅ Created registration page at src/app/(auth)/sign-up/page.tsx
- ✅ Created sign-up form component at src/features/auth/components/sign-up-form.tsx
- ✅ Created use-sign-up hook at src/features/auth/hooks/use-sign-up.ts
- ✅ Created tRPC auth router at src/features/auth/server/auth.ts
- ✅ Added auth router to app router in src/server/api/root.ts
- ✅ Installed react-hook-form and @hookform/resolvers dependencies
- ✅ All lint and typecheck passes
- ✅ Development server runs successfully (HTTP 200 on /sign-up)
- ✅ Client-side validation for email, password match, and password length (min 8)
- ✅ Server-side validation via Zod and tRPC
- ✅ Error handling for duplicate email (USER_ALREADY_EXISTS)
- ✅ Loading states during form submission
- ✅ Redirect to dashboard after successful registration
- ✅ Code review fixes applied: password strength indicator, toast notifications
- ✅ Added password strength indicator UI
- ✅ Added success/error toast notifications
- ✅ Added E2E tests for password strength and form submission

### File List

**Created:**
- `src/app/(auth)/sign-up/page.tsx` - Registration page
- `src/features/auth/components/sign-up-form.tsx` - Registration form component (with password strength & toast)
- `src/features/auth/hooks/use-sign-up.ts` - Sign-up mutation hook
- `src/features/auth/server/auth.ts` - tRPC auth router

**Modified:**
- `src/server/api/root.ts` - Added auth router
- `package.json` - Added react-hook-form and @hookform/resolvers dependencies

**Test Files Created:**
- `tests/unit/auth-schema.test.ts` - Zod validation schema tests (11 tests)
- `tests/e2e/registration.spec.ts` - E2E registration tests (5 tests)
- `vitest.config.ts` - Vitest configuration
- `playwright.config.ts` - Playwright configuration
- `tests/setup.ts` - Test setup

## Change Log

- 2026-03-13: Implemented user registration feature with email/password sign-up
  - Created registration page, form component, tRPC router
  - Integrated with Better Auth for email/password authentication
  - Added client-side and server-side validation
  - Added error handling and loading states
- 2026-03-13: Code review fixes
  - Added password strength indicator UI with color-coded bar
  - Added success/error toast notifications
  - Updated test coverage with additional E2E tests
  - Updated File List with test files
