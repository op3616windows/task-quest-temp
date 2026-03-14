# Story 1.5: View XP and Progress

Status: done

<!-- Note: Validation is optional. Run validate-create-story for quality check before dev-story. -->

## Story

As a user,
I want to view my XP, level, and achievement progress,
so that I can see my advancement in the platform.

## Acceptance Criteria

1. **Given** I am logged in, **When** I view my profile, **Then** I see my current XP total, **And** I see my current level, **And** I see my progress bar to the next level

2. **Given** I am logged in, **When** I have earned achievements, **Then** I see my achievement badges, **And** I see when each was earned

## Tasks / Subtasks

- [x] Task 1: Display XP and Level on profile (AC: 1)
  - [x] Task 1.1: Add XP and level fields to user schema (if not present)
  - [x] Task 1.2: Create XP display component with current XP, level, progress bar
  - [x] Task 1.3: Add XP display to profile page
  - [x] Task 1.4: Calculate and display XP needed for next level
- [x] Task 2: Display achievement badges (AC: 2)
  - [x] Task 2.1: Create badges component
  - [x] Task 2.2: Query user's earned badges
  - [x] Task 2.3: Display badge with earned date
  - [x] Task 2.4: Show locked badges (grayed out) if applicable

## Dev Notes

### Project Structure Notes

- **Feature Location**: `src/features/gamification/` for XP/levels, `src/features/users/` for profile integration
- **Profile Page**: Extend existing profile at `src/app/profile/page.tsx`
- **XP Components**: Create in `src/features/gamification/components/`
- **tRPC Router**: Add XP-related procedures to `src/features/gamification/server/xp.ts` or extend existing users router
- **Database Schema**: Check for XP/level fields in user table, badges table in `src/server/db/schema.ts`

### Previous Story Learnings

From Story 1.4 (Profile Management):
- Feature-based structure: `src/features/users/` contains user-related features
- Profile page exists at `/profile`
- Profile management uses React Hook Form + Zod for validation
- User data stored in `users` table with JSON preferences field
- tRPC procedures follow pattern in `src/features/users/server/users.ts`
- Avatar upload deferred to future - similar pattern may apply to badge images

### Architecture Compliance

- **Framework**: Next.js 15 with App Router
- **API Layer**: tRPC (no direct fetch)
- **Database**: Drizzle ORM with PostgreSQL
- **State**: TanStack Query for data fetching
- **Styling**: Tailwind CSS
- **Naming**: camelCase for API/TypeScript, snake_case for database columns
- **XP/Level System**: Follow architecture's `features/gamification/` pattern
- **Component Library**: shadcn/ui for UI components

### Technical Requirements

- XP stored as integer on user record (or separate XP history table)
- Level calculated from XP using level progression formula (see architecture)
- Progress bar shows percentage toward next level
- Badges earned stored in separate table with user_id, badge_id, earned_at
- XP display component should match UX design (gold/purple theme)
- Profile page should integrate XP display alongside existing profile info

### Library/Framework Requirements

- tRPC router pattern (existing in users.ts)
- React Hook Form + Zod for any form validation
- TanStack Query useQuery for fetching XP/level data
- Tailwind CSS for styling (match XP gold #F59E0B, purple #7C3AED from UX)
- Badge components from shadcn/ui or custom
- XP calculation utilities from `src/features/gamification/xp.ts`

### Testing Requirements

- Unit tests for XP calculation/level progression
- Unit tests for badge earned date formatting
- E2E tests for XP display on profile
- E2E tests for badge display

## References

- [Source: _bmad-output/planning-artifacts/epics.md#Story-1.5-View-XP-and-Progress]
- [Source: _bmad-output/planning-artifacts/architecture.md#Frontend-Architecture]
- [Source: _bmad-output/planning-artifacts/architecture.md#Project-Structure-Patterns]
- [Source: _bmad-output/planning-artifacts/architecture.md#Requirements-to-Structure-Mapping]
- [Source: _bmad-output/planning-artifacts/epics.md#Functional-Requirements]
- [Source: _bmad-output/planning-artifacts/epics.md#XP-Progression-System]
- [Source: _bmad-output/planning-artifacts/ux-design-specification.md#Design-System]

## Dev Agent Record

### Agent Model Used

opencode/minimax-m2.5-free

### Debug Log References

- TypeScript compilation successful (0 errors, 0 warnings in new code)
- ESLint passes with no errors
- All 73 unit tests pass

### Completion Notes List

- Implemented XP and level system following feature-based structure
- Added xp and level fields to user table in database schema
- Created badge and user_badge tables for achievement tracking
- Created XP calculation utilities with level progression formula (10% increase per level)
- Created gamification tRPC router with getXpAndLevel and getUserBadges procedures
- Created XpDisplay component with progress bar showing current XP, level, and progress to next level
- Created BadgesDisplay component showing earned and locked badges with earned dates
- Updated profile page to display XP and badges sections
- Added unit tests for XP calculations and tRPC procedures
- Added E2E tests for XP/badges display (requires authenticated user)
- Fixed existing tests to include xp and level fields in mock data

### File List

New files:
- src/features/gamification/xp.ts (XP calculation utilities)
- src/features/gamification/badges.ts (Badge definitions)
- src/features/gamification/server/gamification.ts (tRPC router)
- src/features/gamification/components/xp-display.tsx (XP display component)
- src/features/gamification/components/badges-display.tsx (Badges display component)
- tests/unit/xp.test.ts (XP utility tests)
- tests/unit/gamification-router.test.ts (tRPC procedure tests)
- tests/e2e/xp-badges.spec.ts (E2E tests for XP/badges display)
- drizzle/0001_add_xp_and_badges.sql (Database migration)

Modified files:
- src/server/db/schema.ts (added xp, level to user table; added badge, userBadge tables)
- src/server/api/root.ts (added gamification router)
- src/app/profile/page.tsx (added XP and badges display)
- tests/unit/user-router.test.ts (fixed mock data to include xp, level)
