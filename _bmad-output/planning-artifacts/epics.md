---
stepsCompleted: ['step-01-validate-prerequisites', 'step-02-design-epics', 'step-03-create-stories', 'step-04-final-validation']
inputDocuments: ['_bmad-output/planning-artifacts/prd.md', '_bmad-output/planning-artifacts/architecture.md', '_bmad-output/planning-artifacts/ux-design-specification.md']
---

# team-management - Epic Breakdown

## Overview

This document provides the complete epic and story breakdown for team-management, decomposing the requirements from the PRD, UX Design if it exists, and Architecture requirements into implementable stories.

## Requirements Inventory

### Functional Requirements

**User Authentication & Management:**
- FR1: Users can register with email/password
- FR2: Users can sign in via OAuth (Google, GitHub)
- FR3: Users can reset password via email
- FR4: Users can manage their profile (name, avatar, preferences)
- FR5: Users can view their XP, level, and achievement progress
- FR6: Sessions expire after 7 days of inactivity

**Quest Management:**
- FR7: Users can create a Quest from a template or blank
- FR8: Users can add Chapters to a Quest
- FR9: Users can add Tasks to a Chapter
- FR10: Users can assign Tasks to team members
- FR11: Users can mark Tasks as complete
- FR12: Quest progress updates automatically as Tasks complete
- FR13: Users can set Quest status (Active, Completed, Archived)

**XP & Progression System:**
- FR14: Users earn XP when completing Tasks
- FR15: Users gain levels as XP accumulates
- FR16: XP rules can be configured per team (Admin)
- FR17: Users can view their XP history and milestones

**Guild & Team Management:**
- FR18: Users can create a Guild (team)
- FR19: Users can invite members to a Guild
- FR20: Guild members can view shared team progress
- FR21: Guild Owners can manage member roles
- FR22: Guild Owners can configure Guild settings

**Activity & Notifications:**
- FR23: Users see real-time Activity Feed of team actions
- FR24: Users receive notifications for Quest completions
- FR25: Users can configure notification preferences

**Badge & Achievement System:**
- FR26: Users earn Badges for achieving milestones
- FR27: Teams can create custom Badges (Pro tier)
- FR28: Users can view their Badge collection
- FR29: Guilds can celebrate Badge achievements

**Project Analytics:**
- FR30: Users can view Quest completion rates
- FR31: Users can view Team XP trends
- FR32: Users can view individual contribution stats

**Import & Integration:**
- FR33: Users can import projects from Linear via OAuth
- FR34: Import maps Issues to Quests/Chapters/Tasks

**Settings & Administration:**
- FR35: Guild Owners can manage billing
- FR36: Guild Owners can manage integrations
- FR37: Guild Admins can manage Guild members

### NonFunctional Requirements

**Performance:**
- Page load time: <2 seconds (p95)
- API response time: <200ms (p95)
- Activity feed refresh: Every 30 seconds (polling)
- Time to "Aha!" moment: <7 days from signup

**Security:**
- All data encrypted in transit (TLS 1.3)
- Passwords hashed with bcrypt (cost factor 12)
- JWT tokens expire after 7 days
- Rate limiting: 100 requests/minute per team
- GDPR compliant: Data export/deletion for EU users

**Scalability:**
- MVP: Support 50 concurrent teams
- 12-month target: Support 500+ teams
- Database: PostgreSQL with connection pooling
- Horizontal scaling ready (stateless app servers)

**Accessibility:**
- WCAG 2.1 AA compliance target
- Keyboard navigation for all core actions
- Screen reader compatible
- Color contrast ratios meet AA standards

**Integration:**
- Linear OAuth integration
- RESTful API design for future integrations
- Webhook support for notifications (Post-MVP)

### Additional Requirements

**From Architecture:**
- Starter Template: T3 Stack (Next.js + tRPC + Drizzle + Better Auth + Tailwind) - Project initialization is the first implementation story
- PostgreSQL database via Neon
- Vercel hosting
- Feature-based folder structure
- Logical multi-tenancy via team_id foreign key
- RBAC: Owner, Admin, Member, Viewer roles
- Drizzle ORM with snake_case schema naming
- TanStack Query for client-side state
- GitHub Actions for CI/CD

**From UX Design:**
- Clean, minimal Linear-inspired base with progress-focused elements
- Purple (#7C3AED) for primary actions, Gold (#F59E0B) for XP/achievements
- XP Progress Bar always visible
- Quest Card component for display
- Badge Display component
- Celebration Overlay (confetti, badge reveal)
- Responsive breakpoints: Mobile (<768px), Tablet (768-1024px), Desktop (>1024px)
- Full keyboard navigation throughout
- Screen reader support with ARIA labels

### FR Coverage Map

| FR | Epic | Story |
|----|------|-------|
| FR1 | Epic 1 | Story 1.1 |
| FR2 | Epic 1 | Story 1.2 |
| FR3 | Epic 1 | Story 1.3 |
| FR4 | Epic 1 | Story 1.4 |
| FR5 | Epic 1 | Story 1.5 |
| FR6 | Epic 1 | Story 1.6 |
| FR7 | Epic 2 | Story 2.1 |
| FR8 | Epic 2 | Story 2.2 |
| FR9 | Epic 2 | Story 2.3 |
| FR10 | Epic 2 | Story 2.4 |
| FR11 | Epic 2 | Story 2.5 |
| FR12 | Epic 2 | Story 2.6 |
| FR13 | Epic 2 | Story 2.7 |
| FR14 | Epic 3 | Story 3.1 |
| FR15 | Epic 3 | Story 3.2 |
| FR16 | Epic 3 | Story 3.3 |
| FR17 | Epic 3 | Story 3.4 |
| FR18 | Epic 4 | Story 4.1 |
| FR19 | Epic 4 | Story 4.2 |
| FR20 | Epic 4 | Story 4.3 |
| FR21 | Epic 4 | Story 4.4 |
| FR22 | Epic 4 | Story 4.5 |
| FR23 | Epic 5 | Story 5.1 |
| FR24 | Epic 5 | Story 5.2 |
| FR25 | Epic 5 | Story 5.3 |
| FR26 | Epic 6 | Story 6.1 |
| FR27 | Epic 6 | Story 6.2 |
| FR28 | Epic 6 | Story 6.3 |
| FR29 | Epic 6 | Story 6.4 |
| FR30 | Epic 7 | Story 7.1 |
| FR31 | Epic 7 | Story 7.2 |
| FR32 | Epic 7 | Story 7.3 |
| FR33 | Epic 8 | Story 8.1 |
| FR34 | Epic 8 | Story 8.2 |
| FR35 | Epic 9 | Story 9.1 |
| FR36 | Epic 9 | Story 9.2 |
| FR37 | Epic 9 | Story 9.3 |

## Epic List

### Epic 1: User Authentication & Profile Management
Users can register, sign in, and manage their personal profiles.
**FRs covered:** FR1, FR2, FR3, FR4, FR5, FR6

### Epic 2: Quest Management
Users can create, organize, and complete quests with chapters and tasks.
**FRs covered:** FR7, FR8, FR9, FR10, FR11, FR12, FR13

### Epic 3: XP & Progression System
Users earn XP and level up by completing tasks.
**FRs covered:** FR14, FR15, FR16, FR17

### Epic 4: Guild & Team Management
Users can create teams, invite members, and manage team settings.
**FRs covered:** FR18, FR19, FR20, FR21, FR22

### Epic 5: Activity & Notifications
Users stay informed about team activity and quest progress.
**FRs covered:** FR23, FR24, FR25

### Epic 6: Badge & Achievement System
Users earn badges for achievements and milestones.
**FRs covered:** FR26, FR27, FR28, FR29

### Epic 7: Project Analytics & Reporting
Users can view quest completion rates, team XP trends, and contribution stats.
**FRs covered:** FR30, FR31, FR32

### Epic 8: Import & Integrations
Users can import projects from Linear via OAuth.
**FRs covered:** FR33, FR34

### Epic 9: Settings & Administration
Team owners can manage billing, integrations, and members.
**FRs covered:** FR35, FR36, FR37

---

## Epic 1: User Authentication & Profile Management

Users can register, sign in, and manage their personal profiles.

### Story 1.0: Project Setup - Initialize T3 Stack

As a developer,
I want to initialize the project using the T3 Stack starter template,
So that I have a ready-to-use development environment.

**Acceptance Criteria:**

**Given** I have Node.js and pnpm installed
**When** I run `pnpm create t3-app@latest taskquest`
**And** I select TypeScript, Tailwind, tRPC, Auth (Better Auth), Drizzle, PostgreSQL
**Then** the project is scaffolded
**And** dependencies are installed

**Given** the T3 app is created
**When** I configure the environment variables
**Then** the app connects to the database
**And** I can run the development server

**Given** the basic app is running
**When** I navigate to localhost:3000
**Then** the app loads without errors

### Story 1.1: User Registration

As a new user,
I want to register with my email and password,
So that I can create an account to access the platform.

**Acceptance Criteria:**

**Given** I am on the registration page
**When** I enter my email, password, and confirm password
**And** I click the "Register" button
**Then** my account is created
**And** I am redirected to the dashboard

**Given** I am on the registration page
**When** I enter an invalid email format
**Then** I see an error message "Please enter a valid email"

**Given** I am on the registration page
**When** I enter mismatched passwords
**Then** I see an error message "Passwords do not match"

**Given** I am on the registration page
**When** I enter a weak password (less than 8 characters)
**Then** I see an error message "Password must be at least 8 characters"

### Story 1.2: OAuth Sign-In

As a user,
I want to sign in using Google or GitHub OAuth,
So that I can quickly access the platform without creating a new password.

**Acceptance Criteria:**

**Given** I am on the sign-in page
**When** I click "Sign in with Google"
**Then** I am redirected to Google OAuth
**And** after authorization, I am returned to the dashboard

**Given** I am on the sign-in page
**When** I click "Sign in with GitHub"
**Then** I am redirected to GitHub OAuth
**And** after authorization, I am returned to the dashboard

### Story 1.3: Password Reset

As a user who forgot my password,
I want to reset my password via email,
So that I can regain access to my account.

**Given** I am on the sign-in page
**When** I click "Forgot Password"
**And** I enter my email address
**And** I click "Send Reset Link"
**Then** I receive a password reset email
**And** I see a success message "Check your email for reset instructions"

### Story 1.4: Profile Management

As a logged-in user,
I want to manage my profile (name, avatar, preferences),
So that I can customize my account.

**Acceptance Criteria:**

**Given** I am on the profile settings page
**When** I update my display name
**And** I click "Save Changes"
**Then** my display name is updated
**And** I see a success message "Profile updated"

**Given** I am on the profile settings page
**When** I upload an avatar image
**Then** my avatar is updated
**And** I see the new avatar displayed

**Given** I am on the profile settings page
**When** I change my preferences
**And** I click "Save Changes"
**Then** my preferences are saved
**And** I see a success message

### Story 1.5: View XP and Progress

As a user,
I want to view my XP, level, and achievement progress,
So that I can see my advancement in the platform.

**Acceptance Criteria:**

**Given** I am logged in
**When** I view my profile
**Then** I see my current XP total
**And** I see my current level
**And** I see my progress bar to the next level

**Given** I am logged in
**When** I have earned achievements
**Then** I see my achievement badges
**And** I see when each was earned

### Story 1.6: Session Management

As a user,
I want sessions to expire after 7 days of inactivity,
So that my account remains secure.

**Acceptance Criteria:**

**Given** I am logged in
**When** I am inactive for 7 days
**Then** my session expires
**And** I am redirected to the sign-in page

**Given** I am logged in
**When** I use the application within 7 days
**Then** my session is extended
**And** I remain logged in

---

## Epic 2: Quest Management

Users can create, organize, and complete quests with chapters and tasks.

### Story 2.1: Create Quest

As a user,
I want to create a new Quest from a template or blank,
So that I can start organizing my work.

**Acceptance Criteria:**

**Given** I am on the Quests page
**When** I click "New Quest"
**And** I enter a Quest title and description
**And** I select a template or blank
**And** I click "Create"
**Then** the Quest is created
**And** I am redirected to the Quest detail page

**Given** I am on the Quest creation page
**When** I select a template
**Then** I see pre-populated chapters and tasks

### Story 2.2: Add Chapters to Quest

As a user,
I want to add Chapters to a Quest,
So that I can break down the Quest into smaller phases.

**Acceptance Criteria:**

**Given** I am on a Quest detail page
**When** I click "Add Chapter"
**And** I enter a chapter title
**And** I click "Add"
**Then** the chapter is added to the Quest
**And** I can reorder chapters via drag-and-drop

### Story 2.3: Add Tasks to Chapter

As a user,
I want to add Tasks to a Chapter,
So that I can define specific work items.

**Acceptance Criteria:**

**Given** I am on a Chapter detail page
**When** I click "Add Task"
**And** I enter a task title
**And** I click "Add"
**Then** the task is added to the Chapter
**And** I can reorder tasks via drag-and-drop

### Story 2.4: Assign Tasks

As a user,
I want to assign Tasks to team members,
So that work is distributed appropriately.

**Acceptance Criteria:**

**Given** I am on a Task detail page
**When** I click "Assign"
**And** I select a team member
**Then** the task is assigned
**And** the assignee sees the task in their list

### Story 2.5: Complete Tasks

As a user,
I want to mark Tasks as complete,
So that I can track progress.

**Acceptance Criteria:**

**Given** I am on a Task list
**When** I click the checkbox on a task
**Then** the task is marked as complete
**And** the task shows a completed state
**And** XP is awarded to the assignee

**Given** I complete the last task in a Chapter
**Then** the Chapter shows as complete
**And** bonus XP is awarded

**Given** I complete the last Chapter in a Quest
**Then** the Quest shows as complete
**And** I receive loot (XP, badge if earned)
**And** a celebration animation plays

### Story 2.6: Auto-Update Quest Progress

As a user,
I want Quest progress to update automatically as Tasks complete,
So that I can see real-time progress.

**Acceptance Criteria:**

**Given** a Quest has multiple chapters and tasks
**When** tasks are completed
**Then** the Quest progress bar updates automatically
**And** the percentage reflects completed tasks

### Story 2.7: Quest Status Management

As a user,
I want to set Quest status (Active, Completed, Archived),
So that I can organize my Quests.

**Acceptance Criteria:**

**Given** I am on a Quest detail page
**When** I change the status to "Archived"
**Then** the Quest is moved to the archived list
**And** it no longer appears in active Quests

---

## Epic 3: XP & Progression System

Users earn XP and level up by completing tasks.

### Story 3.1: Earn XP on Task Completion

As a user,
I earn XP when completing Tasks,
So that I can progress through levels.

**Acceptance Criteria:**

**Given** I complete a task
**When** the task is marked complete
**Then** I receive XP (base amount: 50 XP)
**And** I see an XP animation "+50 XP!"

**Given** I complete a task
**When** there are bonus XP rules
**Then** I receive additional XP based on the rules

### Story 3.2: Level Progression

As a user,
I gain levels as XP accumulates,
So that I can see my advancement.

**Acceptance Criteria:**

**Given** I have earned enough XP to reach a new level
**Then** I level up
**And** I see a level-up celebration
**And** my progress bar resets for the next level

**Given** I am at max level
**Then** I continue to earn XP
**And** I receive bonus rewards instead

### Story 3.3: Configure XP Rules

As a Guild Admin,
I want to configure XP rules per team,
So that I can customize rewards.

**Acceptance Criteria:**

**Given** I am a Guild Admin
**When** I navigate to XP Rules settings
**Then** I can set base XP per task
**And** I can set bonus XP multipliers
**And** I can set bonus XP for chapter/quest completion

### Story 3.4: View XP History

As a user,
I want to view my XP history and milestones,
So that I can see my progress over time.

**Acceptance Criteria:**

**Given** I am on my profile
**When** I click "XP History"
**Then** I see a list of XP-earning activities
**And** I see timestamps for each

**Given** I am on my profile
**When** I reach a milestone
**Then** I see a milestone badge or indicator

---

## Epic 4: Guild & Team Management

Users can create teams, invite members, and manage team settings.

### Story 4.1: Create Guild

As a user,
I want to create a Guild (team),
So that I can start building my team.

**Acceptance Criteria:**

**Given** I am logged in
**When** I click "Create Guild"
**And** I enter a Guild name
**And** I click "Create"
**Then** the Guild is created
**And** I am the Owner
**And** I am redirected to the Guild dashboard

### Story 4.2: Invite Members

As a Guild Owner,
I want to invite members to a Guild,
So that I can grow my team.

**Acceptance Criteria:**

**Given** I am a Guild Owner
**When** I click "Invite Members"
**And** I enter email addresses
**And** I click "Send Invites"
**Then** invitation emails are sent
**And** I see a success message

**Given** I am a Guild Owner
**When** I generate an invite link
**Then** I can share the link
**And** users who click it can join the Guild

### Story 4.3: View Team Progress

As a Guild member,
I want to view shared team progress,
So that I can see how the team is doing.

**Acceptance Criteria:**

**Given** I am a Guild member
**When** I view the Guild dashboard
**Then** I see total team XP
**And** I see team level
**And** I see member contributions

### Story 4.4: Manage Member Roles

As a Guild Owner,
I want to manage member roles,
So that I can control permissions.

**Acceptance Criteria:**

**Given** I am a Guild Owner
**When** I view the member list
**Then** I can change a member's role (Admin, Member, Viewer)
**And** the new permissions take effect immediately

### Story 4.5: Configure Guild Settings

As a Guild Owner,
I want to configure Guild settings,
So that I can customize the team experience.

**Acceptance Criteria:**

**Given** I am a Guild Owner
**When** I navigate to Guild settings
**Then** I can change the Guild name
**And** I can change the Guild description
**And** I can upload a Guild avatar

---

## Epic 5: Activity & Notifications

Users stay informed about team activity and quest progress.

### Story 5.1: Activity Feed

As a user,
I want to see a real-time Activity Feed of team actions,
So that I can stay informed.

**Acceptance Criteria:**

**Given** I am on the dashboard
**When** I view the Activity Feed
**Then** I see recent team activities
**And** the feed refreshes every 30 seconds

**Given** another team member completes a quest
**Then** I see this in the Activity Feed
**And** I can click to view details

### Story 5.2: Quest Completion Notifications

As a user,
I want to receive notifications for Quest completions,
So that I know when milestones are reached.

**Acceptance Criteria:**

**Given** a team member completes a quest
**When** I have notifications enabled
**Then** I receive a notification
**And** the notification shows who completed what

### Story 5.3: Notification Preferences

As a user,
I want to configure notification preferences,
So that I control what I get notified about.

**Acceptance Criteria:**

**Given** I am on notification settings
**When** I toggle "Quest Completions"
**Then** I only receive quest completion notifications when enabled

**Given** I am on notification settings
**When** I toggle "Mentions"
**Then** I only receive mention notifications when enabled

---

## Epic 6: Badge & Achievement System

Users earn badges for achievements and milestones.

### Story 6.1: Earn Badges

As a user,
I earn Badges for achieving milestones,
So that I can showcase my accomplishments.

**Acceptance Criteria:**

**Given** I meet badge criteria
**When** the criteria are met
**Then** I earn the badge
**And** I see a badge unlock celebration

**Given** I earn a badge
**Then** it appears in my badge collection
**And** the team is notified in Activity Feed

### Story 6.2: Custom Badges (Pro)

As a Guild Admin (Pro tier),
I want to create custom Badges,
So that I can recognize team-specific achievements.

**Acceptance Criteria:**

**Given** I am a Guild Admin on Pro tier
**When** I navigate to Badge Management
**And** I create a custom badge
**Then** the badge is available to the team

### Story 6.3: View Badge Collection

As a user,
I want to view my Badge collection,
So that I can see all my achievements.

**Acceptance Criteria:**

**Given** I am on my profile
**When** I view Badges
**Then** I see all earned badges
**And** I see locked badges (greyed out)

### Story 6.4: Celebrate Badge Achievements

As a user,
I want to celebrate Badge achievements with my team,
So that we can acknowledge accomplishments.

**Acceptance Criteria:**

**Given** a team member earns a badge
**When** I view the Activity Feed
**Then** I see the badge celebration
**And** I can react with an emoji

---

## Epic 7: Project Analytics & Reporting

Users can view quest completion rates, team XP trends, and contribution stats.

### Story 7.1: Quest Completion Rates

As a user,
I want to view Quest completion rates,
So that I can measure team productivity.

**Acceptance Criteria:**

**Given** I am on the Analytics page
**When** I view Quest Completion
**Then** I see the percentage of quests completed
**And** I see trends over time

### Story 7.2: Team XP Trends

As a user,
I want to view Team XP trends,
So that I can see team engagement over time.

**Acceptance Criteria:**

**Given** I am on the Analytics page
**When** I view XP Trends
**Then** I see a chart of team XP over time
**And** I can filter by date range

### Story 7.3: Individual Contribution Stats

As a user,
I want to view individual contribution stats,
So that I can see how each member is contributing.

**Acceptance Criteria:**

**Given** I am on the Analytics page
**When** I view Individual Contributions
**Then** I see each member's XP
**And** I see each member's tasks completed

---

## Epic 8: Import & Integrations

Users can import projects from Linear via OAuth.

### Story 8.1: Import from Linear

As a user,
I want to import projects from Linear via OAuth,
So that I can migrate my existing work.

**Acceptance Criteria:**

**Given** I am on the Import page
**When** I click "Import from Linear"
**Then** I am redirected to Linear OAuth
**And** after authorization, I see my Linear projects

**Given** I have authorized Linear
**When** I select a project to import
**Then** the project is imported
**And** issues are mapped to Quests/Chapters/Tasks

### Story 8.2: Map Issues to Quest Structure

As a user,
I want issues mapped to Quests/Chapters/Tasks,
So that my work is organized correctly.

**Given** I am importing from Linear
**When** issues are imported
**Then** Linear issues become Quests
**And** Linear issue lists become Chapters
**And** Linear issues become Tasks

---

## Epic 9: Settings & Administration

Team owners can manage billing, integrations, and members.

### Story 9.1: Manage Billing

As a Guild Owner,
I want to manage billing,
So that I can control my subscription.

**Acceptance Criteria:**

**Given** I am a Guild Owner
**When** I navigate to Billing
**Then** I see my current plan
**And** I can upgrade or downgrade

**Given** I am on the billing page
**When** I update payment method
**Then** my payment method is saved

### Story 9.2: Manage Integrations

As a Guild Owner,
I want to manage integrations,
So that I can connect external tools.

**Acceptance Criteria:**

**Given** I am a Guild Owner
**When** I navigate to Integrations
**Then** I see available integrations
**And** I can enable/disable them

### Story 9.3: Manage Guild Members

As a Guild Admin,
I want to manage Guild members,
So that I can control team access.

**Acceptance Criteria:**

**Given** I am a Guild Admin
**When** I view the member list
**Then** I can remove members
**And** I can view member details
