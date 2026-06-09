# Evaluation Dataset Research: Wasp (wasp-lang.dev)

### 1. Library Overview

*   **Description**: Wasp is a full-stack, open-source web framework that uses a domain-specific language (DSL) to manage the boilerplate of connecting React (frontend), Node.js (backend), and Prisma (database). It provides built-in solutions for authentication, background jobs, email sending, and deployment.
*   **Ecosystem Role**: Wasp acts as a "glue" or "orchestrator" for the modern TypeScript stack. It competes with frameworks like Next.js or Remix but takes a more opinionated, declarative approach to infrastructure and full-stack integration through its compiler.
*   **Project Setup**:
    1.  **Install Wasp CLI**: `curl -sSL https://get.wasp.sh/installer.sh | sh`
    2.  **Initialize Project**: `wasp new my-app` (select template: `basic`, `minimal`, or `saas`)
    3.  **Setup Database**: `wasp db migrate-dev` (starts a managed dev database or applies Prisma migrations)
    4.  **Run App**: `wasp start`

### 2. Core Primitives & APIs

*   **App Configuration (`main.wasp`)**: The central manifest where you define the app's metadata, auth, and global settings.
    ```wasp
    app myApp {
      wasp: { version: "^0.15.0" },
      title: "My App",
      auth: {
        userEntity: User,
        methods: { usernameAndPassword: {} },
        onAuthFailedRedirectTo: "/login"
      }
    }
    ```
    *   [App Config Docs](https://wasp.sh/docs/language/app)

*   **Entities (`schema.prisma`)**: Wasp uses standard Prisma for data modeling.
    ```prisma
    model User {
      id       Int    @id @default(autoincrement())
      username String @unique
      password String
      tasks    Task[]
    }
    ```
    *   [Data Model Docs](https://wasp.sh/docs/data-model/entities)

*   **Operations (Queries & Actions)**: Declarative RPC layer.
    *   **Definition (`main.wasp`)**:
        ```wasp
        query getTasks {
          fn: import { getTasks } from "@src/server/tasks",
          entities: [Task]
        }
        action createTask {
          fn: import { createTask } from "@src/server/tasks",
          entities: [Task]
        }
        ```
    *   **Implementation (`src/server/tasks.ts`)**:
        ```typescript
        import { type GetTasks } from "wasp/server/operations";
        export const getTasks: GetTasks<void, Task[]> = async (args, context) => {
          if (!context.user) throw new HttpError(401);
          return context.entities.Task.findMany({ where: { userId: context.user.id } });
        };
        ```
    *   [Operations Docs](https://wasp.sh/docs/data-model/operations/overview)

*   **Jobs (Background Tasks)**: Managed background processing using `PgBoss`.
    ```wasp
    job emailSender {
      executor: PgBoss,
      perform: { fn: import { sendEmail } from "@src/server/jobs" }
    }
    ```
    *   [Jobs Docs](https://wasp.sh/docs/advanced/jobs)

### 3. Real-World Use Cases & Templates

*   **Open SaaS (Official Template)**: A comprehensive SaaS boilerplate including Stripe/Polar payments, Shadcn UI, S3 file uploads, and admin dashboards.
    *   [Open SaaS Repository](https://github.com/wasp-lang/open-saas)
    *   [Open SaaS Docs](https://docs.opensaas.sh/)
*   **Waspello**: A Trello clone demonstrating complex entity relationships and real-time updates via Wasp's automatic cache invalidation.
    *   [Waspello Example](https://github.com/wasp-lang/wasp/tree/main/examples/waspello)

### 4. Developer Friction Points

*   **DSL Context Switching**: Developers often forget that changes to `main.wasp` require the compiler to re-run, and syntax errors in the DSL can sometimes produce cryptic error messages compared to standard TypeScript errors.
*   **Import Aliases**: Wasp uses specific aliases like `@src`, `@server`, and `@client`. Misconfiguring these in a non-standard IDE or manually editing `tsconfig.json` can break the build process.
*   **Migration from `main.wasp` to `main.wasp.ts`**: The framework is transitioning to a TypeScript-based configuration. Setting this up requires `wasp ts-setup`, which modifies the project structure in a way that can be confusing for beginners. [Discussion on TS Config](https://wasp.sh/docs/general/wasp-ts-config).

### 5. Evaluation Ideas

*   **Simple**: Add a "Priority" field to a Todo entity and update the frontend to sort by it.
*   **Intermediate**: Implement a "Forgot Password" flow using Wasp's built-in Email and Auth primitives.
*   **Intermediate**: Create a background job that generates a weekly PDF report for a user and stores it in S3.
*   **Complex**: Implement multi-tenancy (Organizations) where users can belong to multiple Orgs with different roles.
*   **Complex**: Add a Stripe subscription check middleware to a set of protected Wasp Actions.
*   **Complex**: Migrate a project from `main.wasp` to the new `main.wasp.ts` configuration format.

### 6. Sources

1.  [Official Wasp Documentation](https://wasp.sh/docs): Core framework documentation.
2.  [Wasp llms-full.txt](https://wasp.sh/llms-full.txt): Comprehensive LLM-optimized documentation.
3.  [Open SaaS Website](https://opensaas.sh): Details on the flagship Wasp template.
4.  [Wasp GitHub Repository](https://github.com/wasp-lang/wasp): Source code and example projects.
5.  [LogRocket Blog: Leveraging Wasp](https://blog.logrocket.com/leveraging-wasp-full-stack-development/): Third-party tutorial and overview.
6.  [Wasp CLI Reference](https://wasp.sh/docs/general/cli): Documentation for CLI commands.