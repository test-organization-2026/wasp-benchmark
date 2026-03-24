Wasp drastically reduces backend boilerplate by combining Prisma models with its proprietary Domain-Specific Language (DSL). The Automatic CRUD feature leverages this to generate standard database operations automatically.

You need to define a `Task` entity in `schema.prisma` and configure an automatic `crud` block in `main.wasp`. 

**Constraints:**
- Do NOT manually write the Node.js functions for the CRUD operations.
- The `crud` block must explicitly declare `getAll`, `get`, `create`, and `update` operations.
- You must override the `create` operation to import a custom function from `@src/tasks`.