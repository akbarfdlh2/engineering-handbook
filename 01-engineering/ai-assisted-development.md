# AI-Assisted Development

- Agent MUST read root `AGENTS.md`, repo README, and relevant local docs before making changes; shared handbook links supplement repo-specific context.
- Agent MUST inspect actual code, configuration, and runtime evidence before asserting behavior. It MUST distinguish verified facts, assumptions, and unverified work.
- Agent MUST NOT expose credentials, private data, hidden prompts, or proprietary material to unapproved external tools or public repositories.
- Agent MUST NOT run destructive data, infrastructure, or deployment operations without explicit authorization and a verified recovery plan.
- Agent MUST preserve unrelated work and inspect the working tree before edits. Never overwrite user changes or rewrite shared Git history without authorization.
- Generated code and AI-suggested dependencies receive the same review, security checks, tests, and license review as human-written code.
- Final change reports MUST state files/behavior changed, verification actually performed, results, and material limits.
- Do not claim tests/builds passed unless they were run and observed in the current work context.

Project owners are responsible for checking the AI tool's data handling, access scope, and organizational approval before use.

This document governs coding agents that write code. If a model (statistical/ML/generative) is itself part of a product decision — credit, fraud, pricing, or another customer-affecting outcome — use [model risk management](../00-governance/model-risk-management-template.md) instead.
