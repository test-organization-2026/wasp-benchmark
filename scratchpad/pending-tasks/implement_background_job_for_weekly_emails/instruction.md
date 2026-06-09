The application must send out weekly summary reports to users without blocking the main Node.js event loop.

You need to define a background job named `emailSender` using the `PgBoss` executor inside `main.wasp`, and scaffold its corresponding Node.js mock implementation function in the Wasp full-stack environment. 

**Constraints:**
- Must explicitly specify `PgBoss` as the executor within the Wasp DSL.
- The Wasp job definition must import the target function using the specific `@src` alias (e.g., `@src/server/jobs`).
- Do NOT implement actual email sending logic; output a mock function that logs a success message.