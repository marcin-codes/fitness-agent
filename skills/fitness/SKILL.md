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

When invoked, this skill passes the argument directly to the fitness-science-advisor agent as a command, executed exactly as written without modification. Do not reinterpret or rewrite the argument — pass it verbatim.

## Response Style

The advisor will:
- Prioritize peer-reviewed research over fitness trends
- Provide ranges rather than absolutes
- Explain the reasoning behind recommendations
- Acknowledge when evidence is limited or conflicting
