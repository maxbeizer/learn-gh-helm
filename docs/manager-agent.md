---
layout: default
title: Manager Agent
nav_order: 4
---

# Manager Agent — Observing Your Team

Welcome to the Manager Agent section of gh-helm! Here you'll learn how gh-helm automates monitoring your team's activity and maps their work to performance pillars, so you can focus on coaching—not paperwork.

## What the Manager Agent Does

The Manager Agent is your digital counterpart, tracking progress across the whole team and turning daily activity into actionable insights. It observes team members as they complete work, automatically categorizing their contributions using your defined performance pillars. These pillars make it easy to see who's excelling, who's stuck, and what to focus on in 1-1s.

**High-level capabilities:**
- Monitors repos and projects
- Maps work (issues, PRs, commits) to performance pillars
- Tracks activity for team members
- Prepares 1-1 notes
- Summarizes trends and stats

## Key Commands

gh-helm empowers managers with these agent-specific commands:

### Observe

```shell
gh helm manager observe
```

*Monitors all configured repos, labels, and team members. Records activity for each pillar.*

**Example output:**
```text
🕵️  Observing activity for team: docs-team
- alice: 4 PRs merged, 2 issues resolved (Delivery, Collaboration)
- bob: 3 reviews, 1 new doc section (Collaboration, Documentation)
Pillar mapping complete. See `gh helm manager stats` for details.
```

### Prepare 1-1s

```shell
gh helm manager prep
```

*Compiles recent activity and flags discussion topics for upcoming 1-1s.*

**Example output:**
```text
📝 Preparing 1-1 prep for: alice
- Notable: Drove 'docs/project-agent.md' overhaul (Delivery)
- Opportunity: Missed deadline on 'docs/configuration.md' (Ownership)
- Coaching: Requested help on technical review (Collaboration)
Prep ready for manager-agent review.
```

### Pulse

```shell
gh helm manager pulse
```

*Summarizes team trends and highlights significant shifts.*

**Example output:**
```text
📈 Weekly Pulse:
- Team delivery up 15%
- Documentation pillar lagging
- More cross-team reviews (Collaboration +)
```

### Report

```shell
gh helm manager report
```

*Generates a full report on team activity mapped to pillars, for any time period.*

**Example output:**
```text
💡 Manager Agent Report
June 1–7, 2024
Delivery: 12 PRs merged, 6 features shipped
Collaboration: 18 reviews, 3 co-authored docs
Ownership: 2 blockers resolved
Documentation: 4 new tutorial pages
```

### Stats

```shell
gh helm manager stats
```

*Displays pillar breakdown for each team member.*

**Example output:**
```text
🏆 Team Pillar Stats
alice: Delivery 8, Collaboration 5, Ownership 2, Documentation 3
bob: Delivery 3, Collaboration 7, Ownership 1, Documentation 5
```

## Pillar Mapping: How It Works

The Manager Agent categorizes work using your performance pillars. It's powered by a mapping system:

**Mapping Layers (in order):**
1. **Labels** (e.g., `delivery`, `documentation`)
2. **Repositories** (specific repos for certain pillars)
3. **File Paths** (files or directories linked to pillars)
4. **Keywords** (in issue titles, PR descriptions)

When the agent sees activity, it checks for known labels, repo matches, file paths, or relevant keywords, assigning each piece of work to the right pillar in your helm-manager.toml config.

## Configuration — helm-manager.toml

Pillar mapping and agent rules live in your `helm-manager.toml` file. Example snippet:

```toml
[pillars]
delivery      = ["docs/*", "feature", "bugfix"]
documentation = ["docs/*.md", "tutorial"]
collaboration = ["review", "pairing"]
ownership     = ["blocker", "urgent"]

[team]
alice = "alice-gh"
bob   = "bob-gh"
```

## 1-1 Prep and Observations

The Manager Agent helps you lead effective 1-1s:
- Prepares individualized notes before each meeting
- Flags highlights, opportunities, and coaching moments
- Observes recent activity, trends, and pillar progress

**Typical Workflow:**
1. Run `gh helm manager observe` to capture the latest
2. Run `gh helm manager prep` for personalized 1-1 notes
3. Use the output to guide your conversation, celebrate wins, and identify growth areas

---

Next: [Configuration Reference](./configuration.md) for details on customizing your manager agent.
