---
layout: default
title: "Pairs Well With gh-planning"
nav_order: 6
---

# Pairs Well With: [gh-planning](https://github.com/maxbeizer/gh-planning)

**gh-helm** is a powerful automation tool for agent-driven GitHub project work—but for tracking tasks, priorities, and progress, it pairs perfectly with [gh-planning](https://github.com/maxbeizer/gh-planning).

gh-planning is a lightweight command-line tool that manages GitHub Issues and Projects as kanban boards. For details, see its [repository](https://github.com/maxbeizer/gh-planning).

## How They Complement Each Other

gh-planning keeps your project organized:
- Quickly triage, prioritize, and sort issues into boards
- Plan sprints, manage backlogs, and keep a high-level view

gh-helm executes the work:
- Agents pick up issues from gh-planning boards
- Automate PR creation, file generation, and status updates

By using both, your team gets clean separation between *planning* (the what and when) and *execution* (the how).

## Example Workflow: Plan → Helm → Track

1. **Plan:**
   - Use `gh planning` to triage issues, assign priorities, and groom the project board.

2. **Helm Executes:**
   - An issue is ready (labeled and moved to the "Ready" column).
   - Run `gh helm agent run` to let gh-helm pick up the work, generate code or docs, and open a draft PR.

   ```shell
   gh helm agent run
   ```

3. **Track Progress:**
   - Use `gh planning` to see issue/PR status as work moves across the board.

This pairing lets your team spend less time micromanaging, and more time building.

---

Looking for more? See the [gh-planning repo](https://github.com/maxbeizer/gh-planning) for command details and advanced usage.
