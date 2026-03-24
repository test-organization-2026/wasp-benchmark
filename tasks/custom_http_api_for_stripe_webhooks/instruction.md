While Wasp's Remote Procedure Call (RPC) layer abstracts standard client-server communication, integrating third-party services like Stripe requires standard HTTP endpoints that can process raw request bodies for signature verification.

You need to declare a custom API endpoint and configure Express middleware in the Wasp backend framework. 

**Constraints:**
- You must use the `api` block in the `.wasp` file to define the route, not a `query` or `action` block.
- The endpoint must be configured to securely ingest raw request bodies, bypassing Wasp's default JSON parsing.
- You must manually configure Cross-Origin Resource Sharing (CORS) for this specific endpoint.