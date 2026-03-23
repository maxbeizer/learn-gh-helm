---
layout: default
title: Project Agent
nav_order: 3
---

# Project Agent

Welcome to the Project Agent page! Here, you'll learn exactly how gh-helm's project agent automates issue-driven development — powering sites like this one 🎉.

---

## What is the Project Agent?

gh-helm's project agent is your friendly bot for turning GitHub issues into actionable code and PRs. It reads issues, generates plans, writes code, and opens draft pull requests for review. Perfect for teams (or solo devs) looking to orchestrate AI-driven contributions safely and transparently.

---

## Workflow Overview

Here's the typical workflow:

1. **Issue**: File a GitHub issue describing what you want (e.g., "Add a Project Agent tutorial page").
2. **Plan**: Project agent analyzes the issue and generates a step-by-step plan.
3. **Code**: Based on the plan, the agent writes code (or Markdown), making the necessary file changes.
4. **Draft PR**: Agent pushes the code to a branch and opens a draft PR for human review.

You stay in control — nothing is merged automatically! The agent's work is always visible and reviewable.

---

## Running the Project Agent

To start the project agent from the command line:

```shell
gh helm project start --issue 42
```

- `--issue N` specifies which GitHub issue to process (replace `42` with your issue number).
- The agent will:
  - Claim the issue
  - Read the project context (language, manifests, config)
  - Generate a plan
  - Write code and create/modify files
  - Open a draft PR tied to the issue

### Dry Run Mode

Not ready to commit changes? Try:

```shell
gh helm project start --issue 42 --dry-run
```

- `--dry-run` shows the plan and proposed file changes, but doesn't actually modify files or open PRs.
- Useful for previewing the agent's decisions before letting it loose.

---

## How Project Context Detection Works

gh-helm automatically reads your repo context to guide code generation:

- **Language Detection**: Looks for files like `Gemfile`, `package.json`, or `pyproject.toml` to guess the primary language.
- **Manifest Reading**: Reads key files (e.g., `Gemfile` for Ruby, `_config.yml` for Jekyll) to understand dependencies and project setup.
- **Configuration**: Uses the `helm.toml` file for agent settings (e.g., which files to edit, PR title templates).

This ensures the agent writes code that matches your project's conventions.

---

## Reviewing the Draft Pull Request

Once the agent opens a draft PR:

1. Open the PR in GitHub
2. Review the plan and files the agent created/modified
3. Suggest edits or corrections if needed
4. When satisfied, convert the PR to "Ready for review" and merge manually

> 💡 All agent-generated PRs are visible in your repo history — proof of transparent, agent-driven development!

---

## Daemon Mode: Automated Issue Watching

Want the agent to monitor your repo for new issues, hands-free? Use daemon mode:

```shell
gh helm project daemon
```

- The agent runs continually, picking up issues labeled `agent-ready`.
- Opens draft PRs automatically for each new issue.
- Great for larger projects where contributors write issues and the agent acts as the code-writing executor.

---

## Tips: Writing Issues That Produce Good Code

To get the best results from gh-helm's project agent:

- **Be specific**: Clearly describe what you want, including filenames, desired features, and any requirements.
- **Include examples**: Show sample input/output, stub code, or an outline of the desired page.
- **Context matters**: Reference relevant files, or highlight project conventions (style guide, folder structure).
- **Label appropriately**: For auto-processing, add the `agent-ready` label.
- **Break work into smaller issues**: The agent works best when each issue is focused and actionable.

*Example Issue:*

```
Title: Add Project Agent workflow tutorial page

- Explain the agent's workflow: issue → plan → code → draft PR
- Show example commands for starting agent work
- Detail context detection and project architecture
- Provide review tips
- Front matter: layout: default, title: Project Agent, nav_order: 3
```

The clearer the issue, the clearer (and more accurate) the agent's output!

---

## Learn More

- [gh-helm repo (maxbeizer/gh-helm)](https://github.com/maxbeizer/gh-helm)
- [Just-the-Docs theme](https://just-the-docs.github.io/just-the-docs/)
- [Jekyll](https://jekyllrb.com/)

---

Ready to let the agent build your site? Try filing a new issue and running `gh helm project start --issue N`!
