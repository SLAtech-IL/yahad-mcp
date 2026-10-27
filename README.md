<img src="icon.png" alt="Yahad" width="96" align="right">

# Yahad MCP server

Remote [Model Context Protocol](https://modelcontextprotocol.io) server for
[Yahad](https://www.yahad.ai/) (yahad.ai), a service for group greeting cards
in Hebrew (ברכה משותפת). Friends, family or colleagues each add a greeting, a
photo or a voice message, and the card opens for the recipient on a set date.

With this server an AI assistant can start such a card in the middle of a
conversation and give back the link to send to the group.

```
https://api.yahad.ai/mcp
```

Streamable HTTP. No account, no API key, no sign-in.

This repository holds the description of the server, not its code. The server
itself runs at the address above.

## Tools

| Tool | What it does | Changes data |
|---|---|---|
| `list_occasions` | Lists the supported occasions (birthday, enlistment, release from the army, bar and bat mitzvah, a teacher at the end of the year and others) with the value to pass on | no |
| `suggest_prompts` | Suggests ready questions that help participants write, for an occasion, optionally with the recipient's name filled in | no |
| `create_board` | Creates the card and returns the invite link for participants | yes |
| `board_status` | Shows how many people have signed, when collection closes and when the card opens | no |
| `gift_budget` | How much each person gives toward a group gift, in shekels, rounded down to 10; the organiser adds the rest. Or the budget from a per-person amount | no |
| `occasion_date` | Next two dates of a Jewish holiday, with Israeli postponements, computed from the calendar rule; says when greetings are not customary | no |

`create_board` requires the organiser's email address: the links for managing
the card are sent there. The assistant is told to ask for it and never to
invent one. It also accepts the recipient's gender, which Hebrew grammar needs.

## Try it

```
תכין ברכה משותפת לדנה ליום הולדת ב-1 במרץ, הדוא״ל שלי you@example.com
```
```
אילו שאלות כדאי לשאול את החברים לברכת גיוס?
```
```
איך הולכת הברכה? הנה הקישור: https://www.yahad.ai/m/...
```

## Connect

**Claude** (claude.ai or the desktop app): Settings, Connectors, Add custom
connector, then paste `https://api.yahad.ai/mcp`.

**Claude Code**

```
claude mcp add --transport http yahad https://api.yahad.ai/mcp
```

**Cursor** (`~/.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "yahad": { "url": "https://api.yahad.ai/mcp" }
  }
}
```

**VS Code** (`.vscode/mcp.json`)

```json
{
  "servers": {
    "yahad": { "type": "http", "url": "https://api.yahad.ai/mcp" }
  }
}
```

Any other client that speaks streamable HTTP takes the same address.

## Data

The server stores the recipient's name and the organiser's email. Email is
sent through Amazon SES. No payment data, no credentials. Nothing is sent to
the card's recipient by the server.

- For assistants: https://www.yahad.ai/leozrim/
- Privacy: https://www.yahad.ai/privacy/
- Terms: https://www.yahad.ai/terms/
- Support: https://www.yahad.ai/tmicha/

## Registry

Published in the official MCP Registry as `ai.yahad/yahad`; `server.json` here
is the manifest sent there. The Russian sister service is
[darim-mcp](https://github.com/SLAtech-IL/darim-mcp).

Made by SLATECH LTD.
