---
name: fitness
description: Invoke the fitness-science-advisor agent for evidence-based fitness guidance on workouts, nutrition, body composition, and exercise science.
allowed-tools: Read, Grep, Glob, WebFetch, WebSearch, Bash
model: opus
---

# /fitness - Fitness Science Advisor

This skill invokes the **fitness-science-advisor** agent to provide evidence-based guidance on:

- **Workout Programming**: Hypertrophy, strength, periodization, exercise selection
- **Nutrition Science**: Protein intake, caloric needs, meal timing, supplements
- **Body Composition**: Fat loss, muscle building, body recomposition
- **Exercise Science**: Training principles, recovery, injury prevention

## Quick Examples

```
/fitness What's the optimal protein intake for muscle growth?
/fitness Design a 3-day full body workout program
/fitness Analyze if creatine is worth taking
/fitness How many sets per muscle group per week for hypertrophy?
```

## Connected Fitness Platforms

If configured, this skill can access data from:
- **Hevy** - Workout logging and routines
- **Strava** - Running, cycling, swimming activities
- **Fitbit** - Activity, sleep, heart rate data
- **Garmin** - Comprehensive fitness metrics
- **Under Armour/MapMyFitness** - Running and route data

See the README for setup instructions.

## What This Skill Does

When invoked with `timeline` (and nothing else), ask the user two questions before invoking the agent:
1. "How far back should the timeline go? (e.g. 4 weeks, 3 months)"
2. "How far back should the weight comparison go? (e.g. 3 months, 6 months — can differ from the timeline)"

Then invoke the fitness-science-advisor agent with: `timeline TIMELINE_PERIOD COMPARISON_PERIOD`

For all other arguments, pass the argument directly to the fitness-science-advisor agent exactly as written, without modification.

## Response Style

The advisor will:
- Prioritize peer-reviewed research over fitness trends
- Provide ranges rather than absolutes
- Explain the reasoning behind recommendations
- Acknowledge when evidence is limited or conflicting
