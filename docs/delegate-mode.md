---
layout: default
title: Delegate Mode
nav_order: 8
---

# Delegate Mode

> **Delegate Mode orchestrates coding work by assigning issues to Copilot, rather than generating code directly — perfect for complex projects.**

## When to Use Direct vs Delegate Mode

gh-helm offers two modes for tackling issues:

- **Direct mode** (default): gh-helm generates code responses directly. Best for small, well-defined tasks.
- **Delegate mode**: gh-helm collects project context and hands off the issue to Copilot, letting Copilot work iteratively in a Codespace. Ideal for large features, complex codebases, or when human-like review is needed.

## How Delegate Mode Works

In delegate mode:

1. gh-helm creates a rich context comment for the issue — including project language, build/test commands, Source of Truth, and a file tree.
2. The issue is assigned to the Copilot coding agent (typically `@copilot`).
3. Copilot picks up the issue, starts a Codespace with full context, and works through code changes (builds, tests, iterates, submits PRs).
4. gh-helm manages and tracks the process.

This differs from direct mode, where gh-helm tries to generate the full code solution in a single step.

## Enabling Delegate Mode

You can enable delegate mode in two ways:

- **Config file:**

  ```toml
  # helm.toml
  mode = "delegate"
  ```

- **CLI flag:**

  ```shell
  gh helm project start --issue N --delegate
  ```

This tells gh-helm to hand off orchestration instead of coding directly.

## Context Comment Details

Delegate mode's context comment includes:

- **Detected language** (e.g., Ruby)
- **Build/test commands** (from config or heuristics)
- **Source of Truth** (project architecture, mission, file tree)
- **Current issue and requirements**

This ensures Copilot has everything needed to understand the big picture.

## Example: Delegate Mode in Action

Suppose you want to build a tutorial page for 'Project Agent'.

```shell
# Start a project issue in delegate mode
$ gh helm project start --issue 3 --delegate
```

**gh-helm** will:

- Post a context-rich comment to issue #3
- Assign the issue to `@copilot`
- Copilot spins up a Codespace, reviews the context, and drafts a PR
- gh-helm tracks progress and ensures the solution lands

## Why Delegate Mode Matters

Large codebases and complex tasks benefit from delegate mode:

- Copilot can actually run builds/tests, iterate on feedback
- Multiple files and dependencies are handled gracefully
- The agent can review the whole architecture before coding
- PRs include richer, more accurate changes

Direct mode is great for simple tasks — quick fixes, single files, or boilerplate. Delegate mode goes further, enabling collaborative agent-driven development.

## Summary

- Default is **direct mode** — fast and simple
- For big changes, switch to **delegate mode** via helm.toml or CLI
- Delegate mode lets Copilot work like a human engineer, with full context
- Use the right mode for your task!
