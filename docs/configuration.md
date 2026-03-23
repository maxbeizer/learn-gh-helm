---
layout: default
title: Configuration
nav_order: 5
---

# Configuration Reference

Welcome to the complete guide for configuring gh-helm! This page documents every option available in `helm.toml` and `helm-manager.toml`, so you can fine-tune your development agents.

## Overview

gh-helm relies on TOML configuration files to define agent behavior, project metadata, and workflow settings. You'll typically find these files at the root of your repo:

- `helm.toml` — Main configuration for the Project Agent
- `helm-manager.toml` — Manager Agent configuration (optional, for multi-project orchestration)

For typical setups, only `helm.toml` is required. For more complex, team, or multi-repo arrangements, add `helm-manager.toml`.

---
## `helm.toml` Reference

The `helm.toml` file guides your Project Agent. Below you'll find every field, including its data type, default, and a clear description.

| Field          | Type     | Default           | Description                                        |
|--------------- | -------- | ----------------- | -------------------------------------------------- |
| `version`      | Integer  | `1`               | Configuration schema version. Used for migrations.  |
| `name`         | String   | "(repo name)"    | Logical name for the project.                      |
| `agent`        | Table    | n/a               | Main agent config. See below.                      |
| `agent.role`   | String   | "project"        | Agent role (`project` or, in special cases, `meta`).|
| `agent.prompt` | String   | "(default prompt)"| Custom prompt for agent.                           |
| `plan.enabled` | Boolean  | `true`            | Enable issue-planning via project board.            |
| `plan.column`  | String   | "Ready"          | Issue column for picking tasks.                     |
| `workdir`      | String   | "."              | Project working directory.                         |
| `manager`      | Table    | n/a               | Optional, links to manager agent config.            |
| `manager.path` | String   | "helm-manager.toml" | Path to manager agent config.                  |
| `state`        | Table    | n/a               | State directory settings.                           |
| `state.path`   | String   | ".helm/"         | Agent's local state directory.                      |

### Example: Minimal

```toml
version = 1
name = "learn-gh-helm"

[agent]
role = "project"
prompt = "Build a public tutorial site using gh-helm."
```

### Example: Full

```toml
version = 1
name = "learn-gh-helm"

[agent]
role = "project"
prompt = "Build a public tutorial site for gh-helm."

[plan]
enabled = true
column = "Ready"

[state]
path = ".helm/"

[manager]
path = "helm-manager.toml"
```

### Example: Team Project

```toml
version = 1
name = "developer-site"

[agent]
role = "project"
prompt = "Work with multiple contributors to build docs."

[manager]
path = "../meta/helm-manager.toml"

[plan]
enabled = true
column = "Sprint"
```

---
## `helm-manager.toml` Reference

Use `helm-manager.toml` to orchestrate multiple project agents or coordinate across repos.

| Field            | Type    | Default   | Description                                      |
|------------------| ------- | --------- | ------------------------------------------------ |
| `version`        | Integer | `1`       | Configuration schema version (for migrations).    |
| `name`           | String  | n/a       | Manager agent name.                              |
| `repos`          | Array   | n/a       | List of child project repo paths.                 |
| `prompt`         | String  | n/a       | Manager agent prompt.                            |

### Example: Manager

```toml
version = 1
name = "meta-manager"
prompt = "Coordinate work across all tutorial repos."

repos = ["../projectA", "../projectB", "../projectC"]
```

---
## Version Field & Migration

The `version` field exists to help gh-helm migrate your configuration as the schema evolves. When new fields are added or defaults change, you'll bump `version` to opt-in to the latest features. Backwards compatibility is maintained as much as possible.

You can check your current config with:

```bash
gh helm config check
```

---
## The `.helm/` State Directory

The `.helm/` folder stores local agent state: in-progress work, scratch files, and cached metadata. You can safely remove it to reset agent history (but make sure to commit any real work first!).

### Example contents:

- `.helm/history.json`
- `.helm/agent.log`
- `.helm/tmp/`

> ⚠️ `.helm/` is listed in `.gitignore` so it will never be tracked in git.

---
## Example Config Files

Browse real-world example configs in the [maxbeizer/gh-helm repo](https://github.com/maxbeizer/gh-helm/tree/main/example-configs):

- [Minimal Project Config](https://github.com/maxbeizer/gh-helm/blob/main/example-configs/helm.minimal.toml)
- [Full Project Config](https://github.com/maxbeizer/gh-helm/blob/main/example-configs/helm.full.toml)
- [Manager Config](https://github.com/maxbeizer/gh-helm/blob/main/example-configs/helm-manager.toml)

---
## Advanced Tips

- Set `plan.enabled = false` for local-only work, no project board usage.
- Use unique agent prompts for finely-tuned task guidance.
- Use the manager agent to coordinate multiple repo contributions.

---
## Next Steps

- [Getting Started →](./getting-started.md)
- [How This Site Was Built →](./how-it-was-built.md)

If you have configuration questions, open an issue in [maxbeizer/gh-helm](https://github.com/maxbeizer/gh-helm/issues)!
