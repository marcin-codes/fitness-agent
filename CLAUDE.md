# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Claude Code plugin that provides the `fitness-science-advisor` agent - an evidence-based fitness guidance system with integrations for fitness tracking platforms (Hevy, Strava, Fitbit, Garmin, Under Armour).

## Architecture

```
.claude-plugin/plugin.json    # Plugin manifest (name, version, author, license)
agents/fitness-science-advisor.md   # Main agent definition with system prompt
skills/fitness/SKILL.md       # /fitness shortcut skill
.mcp.json.example             # MCP server config template for API integrations
```

**Key concepts:**
- **Agent** (`agents/`): Markdown file with YAML frontmatter defining the subagent behavior, tools, and model
- **Skill** (`skills/`): Markdown file creating the `/fitness` command shortcut
- **MCP Config**: Template using `${ENV_VAR}` placeholders for user credentials

## Plugin Testing

Test the plugin locally before publishing:
```bash
claude --plugin-dir /path/to/GIT_Fitness_Agent
```

## MCP Integration

The `.mcp.json.example` defines connections to fitness APIs. Users copy it to `.mcp.json` and set environment variables:
- `HEVY_API_KEY` - Requires Hevy Pro subscription
- `STRAVA_ACCESS_TOKEN` - OAuth tokens expire every 6 hours
- `FITBIT_ACCESS_TOKEN` - OAuth tokens expire in 8 hours
- `GARMIN_ACCESS_TOKEN` - Requires approved developer account
- `UA_ACCESS_TOKEN`, `UA_CLIENT_ID` - MapMyFitness/Under Armour

## License

CC BY-NC 4.0 - Free use with attribution to Marcin Konkel, no commercial use/reselling.
