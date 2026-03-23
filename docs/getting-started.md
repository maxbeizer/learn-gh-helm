---
layout: default
title: Getting Started
nav_order: 2
---

# Getting Started with gh-helm

Welcome! This guide will walk you through setting up **gh-helm** in a new project. In less than 10 minutes, you'll have agent-driven automation running on your repo.

## Installation

First, install the gh-helm extension for GitHub CLI:

```
gh extension install maxbeizer/gh-helm
```

You're ready to use `gh helm`!

## Checking Your Project Health

Verify your project is ready for gh-helm:

```
gh helm doctor
```

Typical output:

```
✅ GitHub CLI detected
✅ gh-helm extension installed
⚠️  helm.toml not found
```

If `helm.toml` is missing, gh-helm can scaffold one for you.

## Setting Up Configuration

To create `helm.toml`, either fix automatically or upgrade:

```
gh helm doctor --fix
```
_or_
```
gh helm upgrade
```

This creates a starter `helm.toml` file in your repo. You'll see output like:

```
Scaffolding helm.toml...
✅ helm.toml created in project root
```

## Interactive Project Setup

Initialize your project interactively:

```
gh helm project init
```

You'll be prompted for key fields. Example interaction:

```
? What is the GitHub Project Board URL? [https://github.com/maxbeizer/learn-gh-helm/projects/1]
? Which agent model do you want to use? [manager, project]
? Notification method: [slack, email, none]
```

Complete these steps. Your `helm.toml` will be ready for editing.

## Key helm.toml Fields Explained

Here's a sample `helm.toml`:

```toml
[project]
board_url = "https://github.com/maxbeizer/learn-gh-helm/projects/1"

[agent]
model = "project" # Choices: project, manager

[notifications]
method = "slack"
channel = "#gh-helm-updates"
```

- **board_url**: The GitHub project board to track issues and PRs.
- **model**: `project` automates issues/prs per project; `manager` supervises agents.
- **notifications**: Configure where the agent sends updates (Slack, email, or none).

## Verify It's Working

Run your first agent health check:

```
gh helm doctor
```

Expected output:

```
✅ GitHub CLI detected
✅ gh-helm extension installed
✅ helm.toml validated
```

If you see all green checks, you’re ready to start using gh-helm!

---

**Next steps:**

- [Project Agent](project-agent.md): Learn how the project agent drives your workflow.
- [Configuration Reference](configuration.md): Deep dive into advanced setup.

You’re on your way — this site was built by gh-helm, and now you can use it too!
