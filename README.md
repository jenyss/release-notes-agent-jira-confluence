# Release Notes Agent - JIRA to Confluence

_Powered by Google ADK & Atlassian MCP_

**This agent automates release notes creation from JIRA user stories and publishes them to Confluence.**

![Watch on YouTube](https://img.shields.io/badge/Watch%20on-YouTube-red?logo=youtube&style=for-the-badge)(_coming soon..._)

If you have any questions or would like to collaborate, feel free to reach out to me on [LinkedIn](https://www.linkedin.com/in/jenya-stoeva-60477249/). You're more than welcome!

### How It Works: _release-notes-agent-jira-confluence_
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

### Usage:
    await chat(affected_version="Jan-2026")

**How to get Confluence space and page IDs**
```
Use: https://<confluence-site>.atlassian.net/wiki/api/v2/spaces?keys=<space-key>
Example: https://jenys.atlassian.net/wiki/api/v2/spaces?keys=Jeny
```
```
{
  "results": [
    {
      "spaceOwnerId": "6019b68b3b1af00069d7ee60",
      "homepageId": "98306",
      "createdAt": "2022-02-25T07:43:26.965Z",
      "authorId": "6019b68b3b1af00069d7ee60",
      "description": null,
      "icon": null,
      "status": "current",
      "name": "Jeny",
      "key": "JENY",
      "id": "98305",
      "type": "global",
      "_links": {
        "webui": "/spaces/JENY"
      },
      "currentActiveAlias": "JENY"
    }
  ],
  "_links": {
    "base": "https://jenys.atlassian.net/wiki"
  }
}
```
Parent pageID is displayed the URL.

