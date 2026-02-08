# How We Work

## Feature Workflow

Every piece of work follows this exact sequence. No shortcuts, no exceptions.
This applies to everything. Features, docs, config, refactors. If it gets
committed, it starts with an issue.

### Step 1: GitHub Issue
Before writing any code or docs, create a GitHub issue using `gh issue create`. The issue must contain:
- **User story:** "As a [who], I want [what], so that [why]"
- **Acceptance criteria:** Numbered checklist of specific, testable behaviours
- **Out of scope:** What this feature intentionally does NOT do
All subsequent work references this issue. Commits and PRs link back to it.
Nothing gets committed without a linked issue.

### Step 2: Write E2E Tests First
Translate the acceptance criteria directly into e2e tests. Every acceptance
criterion becomes at least one test assertion. Run the tests. They must all
fail. If any pass before you've built anything, the tests aren't specific enough.

### Step 3: Build the Feature
Implement the minimum code to make the tests pass. Nothing more.

### Step 4: Tests Pass
Run the full test suite. All tests must pass. This is the automated validation.
No manual browser checking needed for functionality.

### Step 5: Visual Verification
After tests pass, open the feature in the browser tool at mobile viewport widths.
Screenshot and check the visual feel. Flag and fix anything that looks generic,
cold, or cluttered.

### Step 6: Commit and PR
Commit referencing the issue (`fixes #N`). Open a PR linking the issue.

The PR body must include a **How to test** section with specific instructions for
manually verifying the feature. Include the URL path to visit, any required setup
steps, and what the reviewer should see or interact with. Don't assume the reviewer
knows where to find the new work.

If the work included visual verification screenshots (Step 5), embed them in the
PR body. Save screenshots to a `screenshots/` directory, never the repo root.

## Code Conventions
- Use `function` declarations for components, arrow functions for handlers/utilities
- Name files in kebab-case: `study-timer.tsx`, `use-session.ts`
- Name components in PascalCase: `StudyTimer`, `SessionProvider`
- Colocate tests next to source files: `study-timer.test.tsx`
- Keep components small and focused. Extract early rather than letting files bloat.
- Prefer composition over prop drilling
- Use server components by default, add `'use client'` only when needed

## Frontend Design Principles
- Read the frontend-design skill file before any visual work.
- No generic AI aesthetics. Every project should have a distinctive visual identity.
- Avoid default system fonts (Inter, Roboto, Space Grotesk) unless deliberately chosen.
- Mobile-first. All touch targets 44px+.
- Support dark mode from day one, defaulting to system preference.
- Respect `prefers-reduced-motion` for all animations.

## Security Defaults
When building or reviewing API-facing code, verify:
1. API keys in environment variables only, never in client code or logs
2. User input passed as data, never interpolated into prompts or queries
3. Input validation: length limits, type checks, reject unexpected fields
4. Rate limiting on all API routes
5. Errors logged server-side only, generic responses to client
6. No PII logged or cached permanently

## Git Conventions
- **Never commit directly to main.** All changes go through a feature branch and PR. No exceptions.
- Commit messages: lowercase, imperative mood, reference issue (e.g. "add study timer component, fixes #3")
- Branch names: `feature/description`, `fix/description`
- Keep commits atomic. One logical change per commit.
- PRs always link back to their GitHub issue

## What to Avoid
- Heavy component libraries (Material UI, Chakra, etc.) unless the project specifically calls for one
- Complex state management (Redux, Zustand) until genuinely needed
- Over-engineering. Build the simplest thing that works, then iterate.
- Feature creep. Every feature must serve the core experience.