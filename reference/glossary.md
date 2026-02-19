# Glossary

### NimbleBrain

The company and hosted platform. What you sign up for and pay for. NimbleBrain runs Nira at scale for teams.

### MCP (Model Context Protocol)

An open protocol for connecting AI models to external tools and data sources. NimbleBrain uses MCP servers as its integration layer.

### MCP Server

A service that implements MCP to expose tools from an external service (Notion, HubSpot, Stripe, etc.) to AI agents.

### MCPB (MCP Bundle)

A packaged, portable MCP server. Contains the server code, dependencies, manifest, and configuration needed to run the server anywhere.

### mpak

The NimbleBrain package registry for MCP bundles and skills. Used to discover, install, and publish integrations.

### Skill

A composable unit of behavior for AI agents. Combines context, instructions, and tool orchestration into a reusable package. Published as `.skill` files to the mpak registry.

### Companion Skill

A skill packaged with an MCP server that composes that server's tools into a practical workflow. Each server ships with 2-3 companion skills.

### Operator

NimbleBrain's target user. Operations professionals (RevOps, Sales Ops, Marketing Ops, etc.) who own business processes and need to automate them without becoming developers.

### Playbook

An automated workflow in NimbleBrain. Defined through conversation with Nira, executed on schedules or triggers.

### Context as Code

Organizational context (business state, processes, conventions, knowledge) expressed as structured, version-controlled files that AI agents can traverse and act on.

### MTF (mpak Trust Framework)

Security scanning standard for MCPB bundles. Covers supply chain, code quality, artifact integrity, provenance, and capability declaration.
