A basic Wasp Todo app currently lists tasks without any specific order, lacking a way for users to prioritize them.

You need to add an Integer `priority` field (defaulting to 1) to the `Task` model in `schema.prisma`, and update the `getTasks` query implementation in `src/server/tasks.ts` to sort tasks by priority in descending order in the Wasp backend environment. 

**Constraints:**
- Use standard Prisma schema syntax for the entity update.
- Do NOT modify the frontend React components; only update the data model and the backend TypeScript query logic.
- Ensure the query retains the filter for the currently authenticated user (`context.user.id`).