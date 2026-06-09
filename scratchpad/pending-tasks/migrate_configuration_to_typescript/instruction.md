Wasp is modernizing its configuration by moving away from its custom DSL towards standard TypeScript configuration files to improve developer experience and IDE support.

You need to manually translate a legacy `main.wasp` file (which contains basic app metadata, email/password auth config, and one query definition) into the new `main.wasp.ts` syntax in the project's root environment. 

**Constraints:**
- Do NOT use or suggest the `wasp ts-setup` CLI command; strictly output the contents of the final `main.wasp.ts` file.
- Ensure all original settings (title, version, auth methods, and operations) are preserved identically in the new TypeScript object format.