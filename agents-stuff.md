

![](agent-design.png)

```
# Global Agent Rules 
## Git Workflow
When making code changes ALWAYS follow this process:

1. Ensure current branch is committed if not do not continue until the user has committed and pushed the changes.

2. Create a new branch before editing:
   git checkout -b agent/<short-task-name>

3. Never commit directly to main or master.

4. Use clear commit messages:
   feat: ...
   fix: ...
   refactor: ...

5. After finishing changes:
   - run tests
   - run linters
   - ensure project builds


## Session Handling

After each agent run or session :

1. Export the session for traceability:
   opencode export

2. Save a summary in:
   docs/agent-sessions/<date>-session.md

3. Include:
   - goal
   - files changed
   - commands run

## Mandatory Rules

These rules must always be followed:
- NEVER make changes unless the current branch is committed.
- ALWAYS create a git branch before editing code.
- NEVER modify protected branches.
- ALWAYS run tests before committing.
- ALWAYS export the session on each completed agent run
```

## Creating an AGENTS.md File

For best results, create an `AGENTS.md` file in your project root. This helps OpenCode understand:

- Your project structure
- Coding conventions
- Preferred patterns
- Technology stack

Example:

```markdown
## Project: My SaaS App

## Tech Stack
- Next.js 14 with App Router
- TypeScript
- Tailwind CSS
- PostgreSQL with Prisma

## Conventions
- Use functional components
- Prefer server components when possible
- Follow REST API naming conventions
- Write tests for all new features

## Structure
- /app - Next.js app router pages
- /components - Reusable UI components
- /lib - Utility functions and helpers
- /prisma - Database schema and migrations
```
