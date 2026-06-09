Certain premium features in the application should be restricted exclusively to paying customers with active Stripe subscriptions.

You need to implement an authorization check inside a Wasp action (`createPremiumTask`) that verifies the user's subscription status and blocks unauthorized access in the Node.js operations layer. 

**Constraints:**
- You must verify `context.user.hasActiveSubscription` inside the action implementation.
- If the user does not have an active subscription, you MUST throw an `HttpError(403)` imported from `wasp/server`.
- Assume the `hasActiveSubscription` boolean already exists on the user context; do NOT alter the Prisma schema for this task.