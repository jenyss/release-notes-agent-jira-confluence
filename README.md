# Release Notes Agent - JIRA to Confluence

_Powered by Google ADK & Atlassian MCP_

**This agent automates release notes creation from JIRA user stories and publishes them to Confluence.**

![Watch on YouTube](https://img.shields.io/badge/Watch%20on-YouTube-red?logo=youtube&style=for-the-badge)(coming soon...)

If you have any questions or would like to collaborate, feel free to reach out to me on [LinkedIn](https://www.linkedin.com/in/jenya-stoeva-60477249/). You're more than welcome!

## How It Works:
**User**
1. Provides JQL parameter - "Affected Version"

**Agent**
1. Retrieves issues with affected_version="Jan-2026" from Jira using JQL query via Atlassian MCP
2. Extract data from issues - Name, Description, ID, Link, Project, ...
3. Generates release notes for each ticket and stores everything in tool_context
4. Publish to Confluence - Creates a formatted Markdown page via Atlassian MCP

## Architecture:
```
┌─────────────────────────────────────────────────────────────┐
│                    SequentialAgent                          │
│                  (ReleaseNotesWorkflow)                     │
├───────────────────────────┬─────────────────────────────────┤
│  TicketProcessorAgent     │   ConfluencePublisherAgent      │
│  ┌─────────────────────┐  │   ┌─────────────────────────┐   │
│  │ Atlassian MCP       │  │   │ format_confluence_conten│   │
│  │ store_ticket_in_ctx │  │   │ Atlassian MCP           │   │
│  └─────────────────────┘  │   └─────────────────────────┘   │
└───────────────────────────┴─────────────────────────────────┘
```

### Local Tools:
- store_ticket_in_context: Saves each processed ticket to tool_context
- format_confluence_content: Reads tickets from context and formats as Markdown

## How-to

### Prerequisites:
- Python 3.10+ with virtual environment
- Node.js 18+ - Required for MCP servers (npx)
- Atlassian Cloud Access - Browser authentication triggered on first run
- Environment Variables - GOOGLE_API_KEY in .env file

### Usage:
    await chat(affected_version="Jan-2026")

<h1 style="text-align: center;">Release Notes Agent - Jira to Confluence</h1>
<p style="text-align: center;"><em>Powered by Google ADK & Atlassian MCP</em></p>

This agent automates release notes creation from Jira work items and publishes them to Confluence.

### How It Works:
**User**
1. Provides JQL parameter - "Affected Version"

**Agent**
1. Retrieves issues with affected_version="Jan-2026" from Jira using JQL query via Atlassian MCP
2. Extract data from issues - Name, Description, ID, Link, Project, ...
3. Generates release notes for each ticket and stores everything in tool_context
4. Publish to Confluence - Creates a formatted Markdown page via Atlassian MCP

### Architecture:
```
┌─────────────────────────────────────────────────────────────┐
│                    SequentialAgent                          │
│                  (ReleaseNotesWorkflow)                     │
├───────────────────────────┬─────────────────────────────────┤
│  TicketProcessorAgent     │   ConfluencePublisherAgent      │
│  ┌─────────────────────┐  │   ┌─────────────────────────┐   │
│  │ Atlassian MCP       │  │   │ format_confluence_conten│   │
│  │ store_ticket_in_ctx │  │   │ Atlassian MCP           │   │
│  └─────────────────────┘  │   └─────────────────────────┘   │
└───────────────────────────┴─────────────────────────────────┘
```

### Local Tools:
- store_ticket_in_context: Saves each processed ticket to tool_context
- format_confluence_content: Reads tickets from context and formats as Markdown

### Prerequisites:
- Python 3.10+ with virtual environment
- Node.js 18+ - Required for MCP servers (npx)
- Atlassian Cloud Access - Browser authentication triggered on first run
- Environment Variables - GOOGLE_API_KEY in .env file

**How to get Confluence space and page IDs**
```
Use: https://<confluence-site>.atlassian.net/wiki/api/v2/spaces?keys=<space-key>
Example: https://marmind-knowledgebase.atlassian.net/wiki/api/v2/spaces?keys=KB
```

