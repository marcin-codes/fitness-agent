# Fitness Science Advisor

An evidence-based fitness guidance agent for Claude Code with integrations for popular fitness tracking platforms.

> **Disclaimer:** This agent, like any AI, can be wrong. It does not substitute professional health support and does not provide professional health or medical advice. Always consult a qualified healthcare or fitness professional before making decisions about your health, training, or nutrition.
>
> This software is provided "as is", without warranty of any kind, express or implied. The author makes no representations or warranties regarding the accuracy, completeness, or suitability of any information provided. To the fullest extent permitted by law, the author shall not be liable for any damages, losses, or harm of any kind arising from or in connection with the use of this software or the information it provides.

**Author:** [Marcin Konkel](https://marcinkonkel.com)

---

## Features

- **Evidence-Based Guidance**: Workout programming, nutrition science, body composition, and exercise physiology based on peer-reviewed research with citations and links
- **Platform Integrations**: Connect to Hevy, Strava, Fitbit, Garmin, and Under Armour/MapMyFitness
- **`/fitness` Shortcut**: Quick access to the fitness advisor from anywhere in Claude Code
- **Myth Busting**: Scientific analysis of fitness trends and claims with quotations, researcher names, and links
- **Personalized Context**: Remembers your goals, training history, and preferences across sessions
- **Body Composition Tracking**: Reads measurements from Tanita, InBody, or manual entries
- **Personal Records Tracking**: Log and track PRs over time with the `pr` command
- **Event Logging**: Track injuries, illness, and life events that affect training with the `event` command
- **Timeline**: Visual PR and event timeline with weight progression comparison table via the `timeline` command
- **Self-Updating**: Pull the latest version from GitHub with the `update-agent` command

---

## User Data Folder

On first startup, the agent automatically creates a folder structure in your home directory:

```
~/fitness-advisor/
├── context.md          # Your personal context (goals, history, preferences, PRs, events)
├── data/               # Body composition measurements
│   ├── inbody-2024-01-15.pdf
│   ├── tanita-scan.jpg
│   └── measurements.txt
└── knowledge/          # Saved articles and debunked myths
    ├── debunked-cardio-kills-gains.md
    └── debunked-meal-timing.md
```

| Folder/File | Purpose |
|-------------|---------|
| `context.md` | Stores your training history, goals, preferences, body composition trends, personal records, and logged events. Updated automatically as you chat. |
| `data/` | Place your body composition reports here (PDFs, images, or text files). The agent reads these to track your progress. |
| `knowledge/` | When you ask about fitness myths, the agent offers to save the debunking as a reference file here. |

**Supported measurement formats:** PDF reports from InBody, Tanita, or similar bioimpedance analyzers; images (photos or screenshots); text files with manually entered data.

---

## First Start Setup

On your first interaction (or when you type `setup`), the agent runs an initial setup:

1. **Welcomes you** and explains all available commands
2. **Asks about your goals** — muscle building, fat loss, strength, endurance, recomposition, etc.
3. **Asks for body stats** — weight, height, and age for tailored advice
4. **Checks for API keys** — detects which fitness platforms you have configured
5. **Asks which platforms to link** — select one or more to sync your workout data
6. **Offers to download history** — fetches your last 2 months of fitness data to establish a baseline

All settings are saved to `context.md` so you won't be asked again in future sessions.

---

## Commands

### `review`

Refresh your data and get a progress report:

- Scans `~/fitness-advisor/data/` for new body composition files
- Downloads last 30 days of workouts from linked platforms
- Updates `context.md` with new measurements and training data
- Reports a summary of changes and progress
- Reviews your progress against your goals with science-backed feedback and recommendations
- Pulls any new PRs from the data folder or API and adds them chronologically to the "Personal Records" section in `context.md`

**Example output:**
```
Review Complete

Body Composition:
- New file: inbody-2024-01-15.pdf
- Body fat: 18.2% (down 0.8%)
- Muscle mass: 72.1kg (up 0.5kg)

Workouts (Hevy - last 30 days):
- 16 workouts completed
- Total volume: 245,000 kg
- PR: Bench Press 100kg x 5

Progress Review (Goal: Build Muscle)
You're on track! Your muscle mass increased while body fat decreased -
a sign of effective recomposition. Your training volume (15 sets/week
per muscle group) aligns with hypertrophy research (Schoenfeld et al.).

Recommendations:
- Consider adding 1-2 sets to lagging muscle groups
- Your bench press progressed well - maintain current progression scheme
- Ensure protein intake stays at 1.6-2.2g/kg for optimal muscle protein synthesis
```

---

### `event <description>`

Log a health or life event that may affect your training:

- Appends the event chronologically to an "Events" section in `context.md`
- Provides science-based suggestions on how to adjust training
- Takes into account past events from your history when relevant

**Example:**
```
event sprained my left ankle during a run, mild pain when bearing weight
```

---

### `pr <description>`

Log a personal record or individual achievement:

- Appends the PR chronologically to a "Personal Records" section in `context.md`
- Summarizes your overall progress across the last 6 months
- Historical PRs are never removed — they serve as a permanent track record

**Example:**
```
pr Deadlift 180kg x 1 - new 1RM
```

---

### `update-agent`

Pull the latest version of the agent from GitHub (https://github.com/marcin-codes/fitness-agent):

- Automatically locates the installation directory
- If installed via `git clone`, runs `git pull origin main` in the repo root
- If not cloned from git, pulls the latest version directly from the GitHub repository
- Reports what changed or confirms the agent is up to date
- Prompts you to restart Claude Code if needed

**Example:**
```
update-agent
```

---

## Updating

### Via command (recommended)

Simply type `update-agent` in any conversation with the fitness advisor. It will find the repo and pull the latest version automatically.

### Manual update

```bash
cd /path/to/fitness-science-advisor
git pull origin main
```

Changes take effect on the next Claude Code session.

---

## Installation

### Option 1: Clone and Install Locally

```bash
git clone https://github.com/marcin-codes/fitness-agent.git
claude /plugin install /path/to/fitness-agent
```

### Option 2: Install Directly from GitHub

```bash
/plugin install marcin-codes/fitness-agent
```

---

## Usage

### Quick Start

```bash
# Use the /fitness shortcut
/fitness What's the optimal protein intake for muscle growth?

# Or just ask directly
"Design a 4-day upper/lower split for hypertrophy"
"How many sets per week for optimal muscle growth?"
"Is creatine worth taking?"
```

### Example Questions

- "What should my caloric deficit be for sustainable fat loss?"
- "Analyze the science behind intermittent fasting"
- "Design a strength program for a beginner"
- "How important is sleep for muscle recovery?"
- "What supplements actually have scientific support?"

---

## Fitness Platform Integrations (Optional)

### Supported Platforms

| Platform | Data Available | Documentation |
|----------|---------------|---------------|
| **Hevy** | Workouts, routines, exercises | [API Docs](https://api.hevyapp.com/docs/) |
| **Strava** | Running, cycling, swimming | [Developer Portal](https://developers.strava.com/) |
| **Fitbit** | Activity, sleep, heart rate | [Web API](https://dev.fitbit.com/build/reference/web-api/) |
| **Garmin** | Comprehensive fitness data | [Connect Program](https://developer.garmin.com/gc-developer-program/) |
| **Under Armour** | Running, routes | [API Docs](https://developer.underarmour.com/docs/) |

### Setup Instructions

#### Step 1: Get Your API Credentials

**Hevy** (Requires Pro subscription)
1. Go to https://hevy.com/settings?developer
2. Generate your API key

**Strava**
1. Go to https://www.strava.com/settings/api
2. Create an application and note your Client ID and Client Secret
3. Use the [Playground](https://developers.strava.com/playground) to get access tokens

**Fitbit**
1. Go to https://dev.fitbit.com/apps/new
2. Register your application and complete the OAuth flow

**Garmin**
1. Apply at https://developer.garmin.com/gc-developer-program/
2. Wait for approval (free for developers)

**Under Armour / MapMyFitness**
1. Register at https://developer.underarmour.com/
2. Create an application and note your Client ID and Secret

#### Step 2: Set Environment Variables

Add to your shell profile (`~/.zshrc`, `~/.bashrc`, etc.):

```bash
# Hevy
export HEVY_API_KEY="your_hevy_api_key"

# Strava
export STRAVA_CLIENT_ID="your_client_id"
export STRAVA_CLIENT_SECRET="your_client_secret"
export STRAVA_ACCESS_TOKEN="your_access_token"
export STRAVA_REFRESH_TOKEN="your_refresh_token"

# Fitbit
export FITBIT_CLIENT_ID="your_client_id"
export FITBIT_CLIENT_SECRET="your_client_secret"
export FITBIT_ACCESS_TOKEN="your_access_token"

# Garmin
export GARMIN_CONSUMER_KEY="your_consumer_key"
export GARMIN_CONSUMER_SECRET="your_consumer_secret"
export GARMIN_ACCESS_TOKEN="your_access_token"

# Under Armour / MapMyFitness
export UA_CLIENT_ID="your_client_id"
export UA_CLIENT_SECRET="your_client_secret"
export UA_ACCESS_TOKEN="your_access_token"
```

Then reload your shell:
```bash
source ~/.zshrc  # or ~/.bashrc
```

#### Step 3: Enable MCP Configuration

```bash
cp .mcp.json.example .mcp.json
```

The config uses environment variables, so your credentials stay secure.

---

## Directory Structure

```
fitness-science-advisor/
├── .claude-plugin/
│   └── plugin.json                      # Plugin manifest
├── agents/
│   └── fitness-science-advisor.md       # Main agent definition
├── skills/
│   └── fitness/
│       └── SKILL.md                     # /fitness shortcut
├── .mcp.json.example                    # API config template (no real credentials)
├── .gitignore                           # Keeps your credentials safe
├── README.md                            # This file
└── LICENSE                              # CC BY-NC 4.0 License
```

---

## Security Notes

- **Never commit `.mcp.json`** with real API keys — it's in `.gitignore`
- Use **environment variables** for all credentials
- The `.mcp.json.example` file is safe to commit — it only contains `${VAR}` placeholders

---

## API Rate Limits

| Platform | Rate Limit |
|----------|-----------|
| Strava | 200 requests/15 min, 2000/day |
| Fitbit | Varies by endpoint |
| Garmin | Contact for limits |
| Hevy | Check Pro tier limits |

---

## Changelog

### v1.6.1
- Added **Honest over Agreeable** as a Core Principle: the agent must never invent or extrapolate training data not present in context.md or returned by an API, and must never fabricate, misquote, or paraphrase study findings to fit a narrative — if a citation cannot be verified or a link is unavailable, it must say so rather than inventing a plausible-sounding reference. The agent must correct the user when they are factually wrong rather than appeasing them.

### v1.6
- Added `timeline` command — generates a compact visual timeline of PRs and events for a user-specified period, followed by a weight progression comparison table against a separately specified period (e.g. timeline last 3 months, compare weights vs 6 months ago). Asks both questions before generating output.

### v1.5
- Added `## 📍 Current Status` block to `context.md` — a rolling window of the last 3 conversations, auto-managed by the agent at the end of every session. Oldest entry is dropped when a new one is added, keeping the file lean while preserving recent decisions, active restrictions, and corrections. The block is read first and treated as highest-priority source of truth, overriding any conflicting information found later in the file. This prevents the agent from contradicting decisions made in recent sessions without permanently bloating context.md.

### v1.4.3
- Improved `/fitness` skill command execution — arguments are now passed verbatim to the agent without reinterpretation, ensuring commands like `review` trigger the correct agent workflow
- `update-agent` now includes the direct GitHub repo URL and works even if the agent was not installed via `git clone`

### v1.4.2
- Removed `knowledge/` folder scan from the pre-answer workflow to optimize token usage. The `knowledge/` folder stores past answers already given to the user — this context is carried in `context.md` and does not need to be re-scanned on every query. Only `context.md` and `data/` are scanned before answering questions.

### v1.4.1
- Added folder structure description on setup — shows users what goes in `data/`, accepted formats, and which folders are auto-managed

### v1.4
- Added `update-agent` command — auto-pulls latest version from GitHub via `git pull`
- Added `setup` as an explicit command trigger (previously first-run only)
- Added welcome message on setup listing all available commands


### v1.3
- Added `event <description>` command — log injuries, illness, and life events to `context.md` with science-based training advice
- Added `pr <description>` command — log personal records chronologically with 6-month progress summaries
- `review` (formerly `update`) now detects and logs new PRs from data files and APIs
- Strengthened evidence standards: peer-reviewed sources highly preferred, links required, missing links flagged explicitly
- Improved skeptical analysis: now requires quotations, researcher names, and links when evaluating claims

### v1.2
- Added automatic initial setup flow on first run
- Setup collects goals, body stats, and API platform links
- Offers to download last 2 months of fitness history on setup
- Added progress review to the `update`/`review` command with science-backed feedback

### v1.1
- Added automatic directory initialization (`~/fitness-advisor/`, `data/`, `knowledge/`) on startup
- Added user context management — reads and updates `context.md` before every response
- Added body composition data tracking — parses PDFs, images, and text files from `data/`
- Added debunking & knowledge management — saves myth-busting articles to `knowledge/`

### v1.0
- Initial release
- Evidence-based fitness guidance on workouts, nutrition, body composition, and exercise science
- Platform integrations: Hevy, Strava, Fitbit, Garmin, Under Armour
- `/fitness` shortcut for quick access in Claude Code

---

## License

This project is licensed under the **Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0)**.

- **Attribution**: You must give credit to Marcin Konkel (https://marcinkonkel.com)
- **NonCommercial**: You may not sell or use this for commercial purposes

See [LICENSE](LICENSE) for full details.

---

## Author

**Marcin Konkel** — [marcinkonkel.com](https://marcinkonkel.com)

Built for [Claude Code](https://claude.ai/claude-code). Questions? Open an issue on GitHub.
