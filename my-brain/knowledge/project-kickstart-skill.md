# ⚡ Project Kickstart Skill

## What is it?
A structured AI pipeline that reads your GitHub Brain files and runs them through 6 specialist agents — producing a fully reasoned project output with human review at every step.

## How to trigger it
```
Run Project Kickstart
Start new project
Kick off [Project Name]
Run Project Kickstart for: [problem statement]
```

## Pipeline
1. Read master/master.md → Master Summary
2. Read all knowledge/*.md → Combined Context
3. 🔌 Gate → Agent 1: PRD Breakdown (prd_breakdown.md)
4. 🔌 Gate → Agent 2: Discovery (discovery.md)
5. 🔌 Gate → Agent 3: User Flows (userflow.md)
6. 🔌 Gate → Agent 4: UI Thinking (UI_thinking.md)
7. 🔌 Gate → Agent 5: Contents (contents.md)
8. 🔌 Gate → Agent 6: Validation (validation.md)
9. 🎨 Ask for Figma link → Deliver final output

## Rules
- Every agent has a Gate: [Yes, run it] or [Skip]
- Every agent ends with a Preview: [Confirm] or [Edit]
- Cumulative summary passes forward at every step
- Full documentation: knowledge/Project-Kickstart-Skill-Doc.docx
