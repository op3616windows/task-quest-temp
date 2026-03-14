# Story 1.3: Password Reset

Status: done

<!-- Note: Validation is optional. Run validate-create-story for quality check before dev-story. -->

## Story

As a user who forgot my password,
I want to reset my password via email,
so that I can regain access to my account.

## Acceptance Criteria

1. **Given** I am on the sign-in page, **When** I click "Forgot Password", **And** I enter my email address, **And** I click "Send Reset Link", **Then** I receive a password reset email, **And** I see a success message "Check your email for reset instructions"
2. **Given** I receive a password reset email, **When** I click the reset link, **Then** I am redirected to a password reset page
3. **Given** I am on the password reset page, **When** I enter a new password and confirm it, **And** I click "Reset Password", **Then** my password is updated, **And** I am redirected to the sign-in page
4. **Given** I am on the password reset page, **When** I enter a weak password (less than 8 characters), **Then** I see an error message "Password must be at least 8 characters"
5. **Given** I am on the password reset page, **When** I enter mismatched passwords, **Then** I see an error message "Passwords do not match"
6. **Given** I have used a reset link, **When** I try to use the same link again, **Then** I see an error "This reset link has expired"
7. **Given** I have used a reset link after 1 hour, **When** I try to use it, **Then** I see an error "This reset link has expired" (reset tokens expire in 1 hour)

## Tasks / Subtasks

- [x] Task 1: Configure Better Auth password reset provider (AC: 1, 6, 7)
  - [x] Task 1.1: Set up email provider in Better Auth config
  - [x] Task 1.2: Configure password reset email template
  - [x] Task 1.3: Set token expiry to 1 hour
- [x] Task 2: Create Forgot Password page UI (AC: 1)
  - [x] Task 2.1: Create forgot-password page component
  - [x] Task 2.2: Add email input with validation
  - [x] Task 2.3: Add "Send Reset Link" button
  - [x] Task 2.4: Display success message after submission
- [x] Task 3: Create Reset Password page UI (AC: 2-5)
  - [x] Task 3.1: Create reset-password page component
  - [x] Task 3.2: Parse reset token from URL
  - [x] Task 3.3: Add password and confirm password inputs
  - [x] Task 3.4: Add password strength validation
  - [x] Task 3.5: Add password match validation
  - [x] Task 3.6: Handle password reset API call
- [x] Task 4: Implement password reset API (AC: 3, 6, 7)
  - [x] Task 4.1: Create forgotPassword tRPC procedure (Not needed - Better Auth handles via handler)
  - [x] Task 4.2: Create resetPassword tRPC procedure (Not needed - Better Auth handles via handler)
  - [x] Task 4.3: Add rate limiting to prevent abuse (Handled by Better Auth)
- [x] Task 5: Set up email service (AC: 1)
  - [x] Task 5.1: Configure email service (Resend/SendGrid/Postmark)
  - [x] Task 5.2: Add email sending function
  - [x] Task 5.3: Add email templates

## Dev Notes

- Relevant architecture patterns and constraints
- Source tree components to touch
- Testing standards summary

### Project Structure Notes

- Alignment with unified project structure (paths, modules, naming)
- Detected conflicts or variances (with rationale)

### References

- Cite all technical details with source paths and sections, e.g. [Source: docs/<file>.md#Section]

## Dev Agent Record

### Agent Model Used

opencode/minimax-m2.5-free

### Debug Log References

- TypeScript compilation successful
- ESLint passes with no errors

### Completion Notes List

- Implemented password reset using Better Auth's built-in email functionality
- Created forgot-password page at /src/app/(auth)/forgot-password/page.tsx
- Created reset-password page at /src/app/(auth)/reset-password/page.tsx
- Configured Resend email service for password reset emails
- Updated Better Auth config to send password reset emails via custom function
- Added environment variables for RESEND_API_KEY
- Token expiry handled by Better Auth (1 hour default)
- Rate limiting handled by Better Auth
- Pre-existing test failures in sign-in-form.test.tsx (not related to this implementation)

### Code Review Fixes Applied

- Added test files to File List
- Improved loading state with spinner animation
- Added accessibility attributes (aria-describedby, aria-busy, role="alert")
- All TypeScript and ESLint checks pass

### File List

New files:
- src/app/(auth)/forgot-password/page.tsx
- src/app/(auth)/reset-password/page.tsx
- src/server/email/index.ts

Modified files:
- src/server/better-auth/config.ts (added emailAndPassword config with sendResetPassword)
- src/env.js (added RESEND_API_KEY)
- .env (added RESEND_API_KEY)
- .env.example (added RESEND_API_KEY)

Test files created:
- tests/unit/password-reset-schema.test.ts
- tests/e2e/password-reset.spec.ts
