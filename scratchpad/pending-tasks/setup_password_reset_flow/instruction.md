Users currently have no way to recover their accounts if they forget their passwords, leading to permanent account lockouts.

You need to configure the `auth` section of `main.wasp` to enable password reset functionalities and set the authentication failure redirection route in the Wasp application configuration. 

**Constraints:**
- Rely entirely on Wasp's built-in Auth primitives within the `main.wasp` file.
- The `onAuthFailedRedirectTo` property MUST be explicitly set to `"/login"`.
- Do NOT implement a custom third-party authentication provider (e.g., Google or GitHub OAuth).