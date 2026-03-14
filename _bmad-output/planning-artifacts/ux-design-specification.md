---
stepsCompleted: ['step-01-init', 'step-02-discovery', 'step-03-core-experience', 'step-04-emotional-response', 'step-05-inspiration', 'step-06-design-system', 'step-07-defining-experience', 'step-08-visual-foundation', 'step-09-design-directions', 'step-10-user-journeys', 'step-11-component-strategy', 'step-12-ux-patterns', 'step-13-responsive-accessibility', 'step-14-complete']
workflow_complete: true
inputDocuments: ['_bmad-output/planning-artifacts/prd.md', '_bmad-output/planning-artifacts/product-brief-team-management-2026-03-12.md']
---

# UX Design Specification team-management

**Author:** op3616
**Date:** 2026-03-13

---

<!-- UX design content will be appended sequentially through collaborative workflow steps -->

## Executive Summary

### Project Vision

TaskQuest is a SaaS team task management platform that transforms mundane tasks into meaningful adventures. By combining powerful productivity features with gamification and team identity systems, TaskQuest solves the "invisible progress" problem that causes team disengagement and turnover.

The product occupies a unique position: "the fun alternative to Linear" - combining serious productivity tooling with emotional engagement.

### Target Users

1. **The Disengaged Developer (Alex)** - Backend engineer feeling like a ticket-completing machine. Needs to feel accomplished and seen.

2. **The Burned-Out PM (Jordan)** - Product manager struggling to show real progress to stakeholders. Needs visibility and morale tools.

3. **The New Team Lead (Casey)** - First-time manager wanting to build team culture. Needs framework for acknowledgment.

4. **Admin/Operations (Taylor)** - Operations lead managing team settings and integrations. Needs visibility and controls.

### Key Design Challenges

1. **Gamification without childishness** - Balance fun progress visualization with professional aesthetic
2. **Information density vs. delight** - Show XP, badges, progress without overwhelming users
3. **Dual-mode experience** - Support both quick task completion (power users) and exploratory progress tracking

### Design Opportunities

1. **Delightful micro-animations** - Celebratory moments when completing quests (confetti, badge reveals)
2. **Progress as storytelling** - Quest boards that read like adventure narratives
3. **Linear-import UX** - Make migration from Linear frictionless and impressive

## Core User Experience

### Defining Experience

**Core Action:** Completing tasks and seeing progress - the quest completion loop. Users mark tasks complete and watch XP/progress increase. This is the primary value delivery moment.

**Value Proposition:** Transform mundane task completion into meaningful progress that users can see, feel, and celebrate.

### Platform Strategy

- **Primary Platform:** Web application (MVP)
- **Input Method:** Keyboard-driven for power users, mouse-friendly
- **Responsive:** Adapts to various screen sizes
- **Offline:** Not required for MVP

### Effortless Interactions

1. **Task Completion** - One click or keystroke to complete a task
2. **Progress Visibility** - Always visible XP bar and current level
3. **Quest Creation** - Simple creation flow from templates

### Critical Success Moments

1. **First Quest Completion** - The "Aha!" moment where XP animation plays and badge may be earned
2. **Linear Import** - Frictionless migration from Linear determines adoption
3. **Quest Progress Visualization** - Seeing chapters complete and "boss battles" defeated

### Experience Principles

1. **Progress should be visible, never hidden** - XP, levels, badges always accessible
2. **Keyboard-first, mouse-friendly** - Power users can fly, mouse users aren't forgotten
3. **Celebrate small wins** - Every task completion has micro-celebration
4. **Professional gamification** - Clean, modern aesthetic, never cartoonish

## Desired Emotional Response

### Primary Emotional Goals

- **Accomplished** - Users feel their work matters and is recognized
- **Excited** - Delighted by progress visualization and celebrations
- **Connected** - Part of a team (Guild) with shared purpose

### Emotional Journey Mapping

1. **First Use** → Curious and hopeful
2. **First Quest Completion** → Surprised by delight (XP animation!)
3. **Regular Use** → Motivated by visible progress
4. **Team Achievement** → Proud belonging to Guild

### Micro-Emotions

- **Accomplishment vs. Frustration** - Key tension to manage
- **Excitement vs. Apathy** - Combat disengagement
- **Belonging vs. Isolation** - Guild system addresses this

### Design Implications

- Celebratory animations on completion (excitement)
- Progress bars always visible (accomplishment)
- Team activity feed (belonging)
- Clean, professional aesthetic (trust)

### Emotional Design Principles

- Celebrations should feel earned, not childish
- Progress visualization is core, not cosmetic
- Team belonging is supported, not forced
- Delight is in the details, not the interface

## UX Pattern Analysis & Inspiration

### Inspiring Products Analysis

1. **Linear** - Primary competitor and inspiration
   - Clean, minimal interface with excellent whitespace
   - Keyboard-driven workflows (cmd+k command palette)
   - Exceptional import UX from other tools

2. **Notion** - Flexible workspace
   - Great onboarding flow that teaches by doing
   - Blocks-based content creation pattern

3. **Habitica** - Gamification pioneer
   - Individual task gamification (lessons for team adaptation)
   - Avatar and progression system design

4. **GitHub** - Developer tools reference
   - Activity feed design and patterns
   - Contribution graphs as progress visualization template

### Transferable UX Patterns

- **Command Palette (Linear)** → TaskQuest keyboard navigation with cmd+k
- **Contribution Graph (GitHub)** → XP progress bars and visualization
- **Clean List Views (Linear)** → Quest and Task list layouts
- **Block Creation (Notion)** → Quest/Chapter/Task creation flow

### Anti-Patterns to Avoid

- **Cluttered gamification** - Keep progress elements clean and professional
- **Overwhelming first-time experience** - Linear excels here, don't complicate
- **Rigid workflows** - Flexibility for different team styles matters

### Design Inspiration Strategy

**What to Adopt:**
- Linear's keyboard-first navigation
- GitHub's progress visualization
- Clean whitespace and minimal design

**What to Adapt:**
- Habitica's gamification for team context
- Notion's onboarding for task management

**What to Avoid:**
- Cartoonish gamification visuals
- Feature-heavy first screens
- Complex initial setup flows

## Design System Foundation

### Design System Choice

**Tailwind CSS + shadcn/ui**

A powerful combination of utility-first CSS framework with a collection of accessible, reusable components.

### Rationale for Selection

1. **Speed** - Tailwind provides rapid UI development
2. **Accessibility** - shadcn/ui provides WCAG-compliant components out of the box
3. **Customization** - Both are fully customizable for TaskQuest's unique gamification needs
4. **Developer Experience** - Easy to maintain, extend, and customize
5. **Modern Aesthetic** - Matches the clean, professional look we need

### Implementation Approach

- **Tailwind CSS** - Core utility classes for layout, spacing, typography, colors
- **shadcn/ui** - Base components (buttons, forms, dialogs, dropdowns, cards)
- **Custom Components** - Build on top for: Quest cards, XP bars, Badge displays, Progress visualizations, Celebration animations

### Customization Strategy

- Extend shadcn/ui theme tokens for TaskQuest brand colors
- Create custom "progress" component library
- Build "celebration" layer for animations and micro-interactions
- Maintain Linear-like minimal aesthetic for productivity surfaces
- Add gamification visual elements as overlay/wrapper layer

## 2. Core User Experience

### Defining Experience

**Completing a Quest** - The core action: completing tasks in a Quest and watching progress unfold.

### User Mental Model

- Users think of work as "tasks to complete"
- Quest metaphor adds adventure layer without changing behavior
- Progress should feel like advancing in a game, not filling spreadsheets

### Success Criteria

- One click/keystroke to complete a task
- Immediate visual feedback (XP animation, progress bar update)
- Clear sense of advancement
- Celebration on quest completion (confetti, badge reveal)

### Novel UX Patterns

- Task completion = established pattern (users know this)
- Quest/Chapters/Boss Battles = novel gamification layer
- Need to teach metaphor without being confusing

### Experience Mechanics

1. **Initiation:** User sees Quest board with tasks
2. **Interaction:** Click task or press key to complete
3. **Feedback:** XP animation (+50 XP!), progress bar moves, sound optional
4. **Completion:** Quest complete → Celebration → Badge if earned

## Visual Design Foundation

### Color System

**Primary Palette:** Clean, minimal base (Linear-inspired)
- Background: Pure white (#FFFFFF) / Dark: Near-black (#0D0D0D)
- Surface: Light gray (#F9FAFB) / Dark: Dark gray (#1A1A1A)
- Border: Subtle gray (#E5E7EB) / Dark: (#2D2D2D)
- Text Primary: Near-black (#111827) / Dark: (#F9FAFB)
- Text Secondary: Gray (#6B7280)

**Accent Colors:** Gamification layer
- Primary Action: Deep purple (#7C3AED) - Progress, advancement
- XP/Gold: Warm gold (#F59E0B) - Achievement, rewards
- Success: Emerald (#10B981) - Quest completion
- Celebration: Gradient gold-to-purple for special moments

**Semantic Colors:**
- Success: Emerald (#10B981)
- Warning: Amber (#F59E0B)
- Error: Rose (#EF4444)
- Info: Sky blue (#0EA5E9)

### Typography System

**Font Stack:**
- Primary: Inter (clean, modern, excellent readability)
- Monospace: JetBrains Mono (for code/technical content)

**Type Scale:**
- H1: 32px / Bold
- H2: 24px / Semibold
- H3: 18px / Semibold
- Body: 14px / Regular
- Small: 12px / Regular
- Caption: 11px / Medium

### Spacing & Layout Foundation

**Base Unit:** 4px (Tailwind default)

**Spacing Scale:**
- xs: 4px
- sm: 8px
- md: 16px
- lg: 24px
- xl: 32px
- 2xl: 48px

**Layout Principles:**
- Dense enough for productivity (like Linear)
- Airy enough for progress visualization
- 12-column grid for complex layouts
- Sidebar navigation (240px) + content area

### Accessibility Considerations

- WCAG 2.1 AA compliance target
- Minimum contrast ratio: 4.5:1 for text
- Focus indicators on all interactive elements
- Keyboard navigation throughout
- Screen reader friendly (ARIA labels)

## Design Direction Decision

### Design Directions Explored

1. **Linear-Inspired Minimal** - Clean, sparse, focus on content
2. **Progress-Focused** - Gamification prominent with visible XP bars
3. **Dark Mode Primary** - Developer-friendly dark aesthetic
4. **Card-Based Exploration** - Quest-centric visual layout

### Chosen Direction

**Linear-Inspired Minimal with Progress-Focused Elements**

Combines Linear's clean productivity aesthetic with strategic gamification:
- Clean white backgrounds, minimal borders (Linear baseline)
- Visible but not overwhelming progress indicators
- Purple/gold accents for achievements and XP
- Card-based Quest display for visual engagement

### Design Rationale

- Matches "fun alternative to Linear" positioning
- Professional enough for enterprise, delightful enough for engagement
- Progress visible but not cluttered
- Scalable visual language

### Implementation Approach

- Start with Linear-like minimal base
- Layer in progress components (XP bars, badge displays)
- Quest cards as primary content containers
- Gradual gamification introduction in UI

## User Journey Flows

### Journey 1: Completing a Quest

**User:** Alex (Disengaged Developer)
**Goal:** Complete tasks and see progress

**Flow:**
1. User views Quest board with task list
2. User clicks task or presses key to complete
3. System shows XP animation (+50 XP!)
4. Progress bar updates
5. If Quest complete → Celebration → Badge earned (optional)

**Key Interactions:**
- Single click/key to complete
- Immediate visual feedback
- Sound optional

### Journey 2: Creating a Quest

**User:** Jordan (PM)
**Goal:** Create a new quest for team

**Flow:**
1. User clicks "New Quest" button
2. User enters Quest title and description
3. User adds Chapters (optional)
4. User adds Tasks to Quest
5. User assigns Tasks to team members
6. User sets Quest status to "Active"
7. Quest appears on team board

**Key Interactions:**
- Progressive disclosure for complexity
- Template selection for speed
- Assignee selection for team tasks

### Journey 3: Onboarding to Guild

**User:** Casey (New Team Lead)
**Goal:** Set up team with Guild

**Flow:**
1. User creates Guild (team)
2. User invites team members via email/link
3. User creates first badge criteria
4. User configures XP rules
5. Team begins using Quests

**Key Interactions:**
- Simple Guild creation wizard
- Easy invite flow
- Badge criteria templates

### Journey Patterns

**Navigation:**
- Sidebar navigation for main sections
- Breadcrumbs for nested content
- Cmd+K command palette for quick actions

**Feedback:**
- Immediate XP animations on completion
- Progress bars always visible
- Toast notifications for actions
- Loading states for async operations

**Decision Points:**
- Clear CTAs for primary actions
- Secondary actions in dropdowns
- Destructive actions require confirmation

### Flow Optimization Principles

1. **Minimize steps to value** - Get users to completion quickly
2. **Reduce cognitive load** - Show only what's needed at each step
3. **Clear progress indicators** - Users always know where they are
4. **Delight moments** - Celebrate achievements visibly
5. **Graceful error handling** - Clear recovery paths

## Component Strategy

### Design System Components

**From shadcn/ui:**
- Button, Input, Select, Dropdown
- Card, Dialog, Sheet (sidebar)
- Form, Label, Checkbox
- Toast (notifications)
- Avatar, Badge
- Table, Tabs

### Custom Components

**1. Quest Card**
- Purpose: Display quest with progress
- States: active, completed, archived
- Contains: title, progress bar, chapter count, XP display

**2. XP Progress Bar**
- Purpose: Show user progress to next level
- States: normal, leveling-up, celebration
- Animations: fill animation, glow on level up

**3. Badge Display**
- Purpose: Show earned achievements
- States: locked, unlocked, celebrating
- Contains: icon, name, earn date

**4. Chapter Progress**
- Purpose: Show quest chapter completion
- States: pending, in-progress, boss-battle, completed
- Visual: task count, boss indicator

**5. Celebration Overlay**
- Purpose: Reward moment on quest completion
- Contains: confetti, badge reveal, XP gain notification
- Triggers: quest complete, badge earned, level up

### Component Implementation Strategy

- Build custom components using Tailwind + shadcn/ui patterns
- Use design tokens for consistent theming
- Follow shadcn/ui accessibility patterns
- Create React components for reusability

### Implementation Roadmap

**Phase 1 (Core - MVP):**
- Quest Card, Task Item, XP Progress Bar

**Phase 2 (Gamification):**
- Badge Display, Chapter Progress

**Phase 3 (Delight):**
- Celebration Overlay, animation system

## UX Consistency Patterns

### Button Hierarchy

- **Primary**: Purple (#7C3AED) - Main CTAs
- **Secondary**: Gray outline - Secondary actions
- **Ghost**: Text only - Tertiary actions
- **Destructive**: Red (#EF4444) - Delete, remove

### Feedback Patterns

- **Success**: Green toast + checkmark
- **Error**: Red toast + message  
- **Warning**: Amber toast
- **Loading**: Skeleton screens, spinners
- **Info**: Blue toast

### Form Patterns

- Labels above inputs
- Inline validation on blur
- Error messages below fields
- Required field indicator (*)
- Placeholder text for examples

### Navigation Patterns

- Sidebar: Main navigation (240px fixed)
- Breadcrumbs: Path navigation
- Cmd+K: Command palette (global search)
- Tabs: Content organization

### Empty States

- Illustration + message + CTA
- Guide users to first action

### Loading States

- Skeleton screens for content
- Spinners for actions
- Progress indicators for uploads

## Responsive Design & Accessibility

### Responsive Strategy

- **Desktop**: Full sidebar (240px), multi-column layouts, keyboard-first
- **Tablet**: Collapsible sidebar, touch-optimized interactions
- **Mobile**: Bottom navigation, simplified views, essential features only

### Breakpoint Strategy

- **Mobile**: < 768px
- **Tablet**: 768px - 1024px  
- **Desktop**: > 1024px

### Accessibility Strategy

- **Target**: WCAG 2.1 AA compliance
- **Keyboard**: Full keyboard navigation throughout
- **Contrast**: 4.5:1 minimum for text
- **Focus**: Visible focus indicators on all interactive elements
- **Screen Reader**: ARIA labels on custom components

### Testing Strategy

- Device testing on actual phones/tablets
- Screen reader testing (VoiceOver, NVDA)
- Keyboard-only navigation testing
- Color blindness simulation

### Implementation Guidelines

- Use relative units (rem, %)
- Mobile-first media queries
- Semantic HTML structure
- Focus management for modals
