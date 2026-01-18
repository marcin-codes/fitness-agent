# Fitness Science Advisor

An evidence-based fitness guidance agent for Claude Code with integrations for popular fitness tracking platforms.

**Author:** [Marcin Konkel](https://marcinkonkel.com)

## Features

- **Evidence-Based Guidance**: Workout programming, nutrition science, body composition, and exercise physiology based on peer-reviewed research
- **Platform Integrations**: Connect to Hevy, Strava, Fitbit, Garmin, and Under Armour/MapMyFitness
- **`/fitness` Shortcut**: Quick access to the fitness advisor from anywhere in Claude Code
- **Myth Busting**: Get scientific analysis of fitness trends and claims
- **Personalized Context**: Remembers your goals, training history, and preferences across sessions
- **Body Composition Tracking**: Reads measurements from Tanita, InBody, or manual entries

## User Data Folder

On first startup, the agent automatically creates a folder structure in your home directory to store your personal fitness data:

```
~/fitness-advisor/
├── context.md          # Your personal context (goals, history, preferences)
├── data/               # Body composition measurements
│   ├── inbody-2024-01-15.pdf
│   ├── tanita-scan.jpg
│   └── measurements.txt
└── knowledge/          # Saved articles and debunked myths
    ├── debunked-cardio-kills-gains.md
    └── debunked-meal-timing.md
```

### Folder Purposes

| Folder/File | Purpose |
|-------------|---------|
| `context.md` | Stores your training history, goals, preferences, and body composition trends. Updated automatically as you chat. |
| `data/` | Place your body composition reports here (PDFs, images, or text files from Tanita, InBody, or manual measurements). The agent reads these to track your progress. |
| `knowledge/` | When you ask about fitness myths, the agent offers to save the debunking as a reference file here. |

### Supported Measurement Formats

The agent can read body composition data from:
- **PDF reports** from InBody, Tanita, or similar bioimpedance analyzers
- **Images** (photos or screenshots of measurement printouts)
- **Text files** with manually entered data

Simply drop your measurement files into `~/fitness-advisor/data/` and the agent will parse them automatically.

## First Start Setup

On your first interaction, the agent runs an initial setup:

1. **Creates directory structure** (`~/fitness-advisor/`, `data/`, `knowledge/`)

2. **Checks for API keys** - detects which fitness platforms you have configured:
   ```
   Hevy: ✓
   Strava: ✓
   Fitbit: ✗
   Garmin: ✗
   ```

3. **Asks which platforms to link** - select one or more to sync your workout data

4. **Offers to download history** - fetches your last 2 months of fitness data to establish a baseline

5. **Asks about your goals** - muscle building, fat loss, strength, endurance, recomposition, etc.

All settings are saved to `context.md` so you won't be asked again in future sessions.

## Commands

### `update`

Type **"update"** anytime to refresh your data:

- Scans `~/fitness-advisor/data/` for new body composition files
- Downloads last 30 days of workouts from linked platforms
- Updates `context.md` with new measurements and training data
- Reports a summary of changes and progress

**Example output:**
```
📊 Update Complete!

Body Composition:
- New file: inbody-2024-01-15.pdf
- Body fat: 18.2% (↓0.8%)
- Muscle mass: 72.1kg (↑0.5kg)

Workouts (Hevy - last 30 days):
- 16 workouts completed
- Total volume: 245,000 kg
- PR: Bench Press 100kg x 5
```

## Installation

### Option 1: Clone and Install Locally

```bash
# Clone the repository
git clone https://github.com/marcinkonkel/fitness-science-advisor.git

# Install in Claude Code
claude /plugin install /path/to/fitness-science-advisor
```

### Option 2: Install Directly from GitHub

```bash
# In Claude Code
/plugin install marcinkonkel/fitness-science-advisor
```

## Usage

### Quick Commands

```bash
# Use the /fitness shortcut
/fitness What's the optimal protein intake for muscle growth?

# Or just ask - the agent auto-activates for fitness questions
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

## Fitness Platform Integrations (Optional)

Connect your fitness tracking accounts to analyze your personal data.

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

Each platform requires you to register as a developer:

**Hevy** (Requires Pro subscription)
1. Go to https://hevy.com/settings?developer
2. Generate your API key

**Strava**
1. Go to https://www.strava.com/settings/api
2. Create an application
3. Note your Client ID, Client Secret
4. Use the [Playground](https://developers.strava.com/playground) to get access tokens

**Fitbit**
1. Go to https://dev.fitbit.com/apps/new
2. Register your application
3. Complete OAuth flow to get access token

**Garmin**
1. Apply at https://developer.garmin.com/gc-developer-program/
2. Wait for approval (free for developers)
3. Access your Consumer Key and Secret

**Under Armour / MapMyFitness**
1. Register at https://developer.underarmour.com/
2. Create an application
3. Note your Client ID and Secret

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
# Copy the example config
cp .mcp.json.example .mcp.json

# The config uses environment variables, so your credentials stay secure
```

## Directory Structure

```
fitness-science-advisor/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── agents/
│   └── fitness-science-advisor.md   # Main agent definition
├── skills/
│   └── fitness/
│       └── SKILL.md         # /fitness shortcut
├── .mcp.json.example        # API config template (no real credentials)
├── .gitignore               # Keeps your credentials safe
├── README.md                # This file
└── LICENSE                  # CC BY-NC 4.0 License
```

## Security Notes

- **Never commit `.mcp.json`** with real API keys - it's in `.gitignore`
- Use **environment variables** for all credentials
- The `.mcp.json.example` file is safe to commit - it only contains `${VAR}` placeholders
- Each user configures their own credentials locally

## API Rate Limits

Be aware of rate limits when using integrations:

| Platform | Rate Limit |
|----------|-----------|
| Strava | 200 requests/15 min, 2000/day |
| Fitbit | Varies by endpoint |
| Garmin | Contact for limits |
| Hevy | Check Pro tier limits |

## Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

This project is licensed under the **Creative Commons Attribution-NonCommercial 4.0 International License (CC BY-NC 4.0)**.

**You are free to:**
- Use this software free of charge
- Share and adapt the material

**Under these conditions:**
- **Attribution**: You must give credit to Marcin Konkel (https://marcinkonkel.com)
- **NonCommercial**: You may not sell or use this for commercial purposes

See [LICENSE](LICENSE) for full details.

## Author

**Marcin Konkel**
- Website: [https://marcinkonkel.com](https://marcinkonkel.com)

## Acknowledgments

- Built for [Claude Code](https://claude.ai/claude-code)
- Fitness science guidance based on peer-reviewed research
- Platform integrations use official APIs

---

**Questions?** Open an issue on GitHub or visit [marcinkonkel.com](https://marcinkonkel.com)
