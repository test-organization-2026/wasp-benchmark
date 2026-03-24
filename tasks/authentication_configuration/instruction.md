Wasp handles authentication natively by generating the necessary server-side session management and client-side UI components based on a few lines of declarative code.

You need to configure the `auth` block for a user entity in the `main.wasp` configuration file. 

**Constraints:**
- The authentication block must map to an existing `User` entity.
- You must enable both `email` and `google` authentication methods.
- Do NOT use third-party vendor libraries (like Auth0 or Clerk) to fulfill this task.