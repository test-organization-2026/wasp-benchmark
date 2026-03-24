Wasp does not feature a native multi-tenancy keyword, meaning data isolation for Software as a Service (SaaS) applications must be strictly enforced at the database and operations layer to prevent cross-tenant data leaks.

You need to write a secure Node.js server action enforcing data isolation in a multi-tenant Wasp application. 

**Constraints:**
- The action must extract the tenant identifier strictly via the `context.user` object.
- The database write operation must fail entirely if `context.user` is undefined or lacks a valid `tenantId`.
- Do NOT utilize external authorization middleware; rely only on Wasp's native context and Prisma's filtering capabilities.