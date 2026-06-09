The application is scaling from individual users to B2B teams, requiring multi-tenancy and team collaboration support.

You need to create an `Organization` model and an `OrganizationRole` enum in `schema.prisma`, and establish a many-to-many relationship with the existing `User` model in the Prisma data modeling environment. 

**Constraints:**
- The `User` model MUST retain its default authentication fields (`id`, `username`, `password`).
- The many-to-many relationship must utilize a join table (e.g., `UserOrganization`) to track the specific `OrganizationRole` (e.g., ADMIN, MEMBER) for each user within an organization.