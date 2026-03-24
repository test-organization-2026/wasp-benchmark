Wasp relies on PgBoss to handle background processing and cron scheduling. However, modifying scheduled jobs can leave stale records in the database, resulting in memory bloat and overlapping executions.

You need to define a scheduled cron job and write a SQL cleanup command in the Wasp backend environment. 

**Constraints:**
- The job defined in `main.wasp` must be named `sentimentAnalysisJob` and execute every 5 minutes using standard Unix cron syntax.
- You must provide the exact SQL command to manually delete an old job named `oldSentimentJob` specifically from the `pgboss.schedule` table.