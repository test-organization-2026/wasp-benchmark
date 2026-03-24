Handling large binary file uploads directly through a Node.js API can cause severe backend payload bottlenecks. The Open SaaS pattern within the Wasp ecosystem mitigates this by utilizing direct-to-cloud uploads.

You need to implement a server-side action that generates an S3 presigned URL in the Wasp backend. 

**Constraints:**
- The file payload itself must NOT pass through the Node.js server.
- The server action must only return the generated temporary upload URL and necessary AWS authentication headers.
- Ensure the action is authenticated so only logged-in users can request a presigned URL.