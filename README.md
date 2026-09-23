# Agent Crew

A multi-agent orchestration demo — one lead agent that plans, delegates, and coordinates a small team of specialist AI agents to complete a goal. Built with the [Claude API](https://docs.claude.com).

## Live demo

**[Try it here](https://claude.ai/artifact/P3dCzQKbKUdfEFNLxVx3T3)** — note: trying the interactive part requires a free Claude account to sign in with (a platform requirement for any page that calls Claude live, not specific to this project).

## The problem

Most "AI agent" demos are really one model doing one task end to end. But real coordination work — the kind a project lead actually does — looks different: break a goal into the right pieces, assign each piece to the right specialist, make sure each stage actually builds on the last instead of working in isolation, and sign off on the finished result. This project demonstrates that pattern directly, with agents actually coordinating rather than working in parallel isolation.

## What it does

Given any goal, typed in plain language:

1. **A Lead Agent plans the work** — breaks the goal into exactly 3 sequential tasks and decides what specialist role each one needs (it names and defines the roles itself based on the specific goal, not a fixed template)
2. **Each specialist agent runs in real sequence** — and genuinely receives the previous agent's actual output as context before starting, so the second agent is demonstrably building on the first's real work, not just running in parallel
3. **The Lead Agent reviews and signs off** — reads everything the team produced and delivers the final, ready-to-use result along with a short summary of what happened

The UI shows this happening live: each agent card visibly moves from Queued → Working → Done, with its actual output visible once finished, so the coordination is observable, not just claimed.

## Example flow

Goal: *"Write a launch announcement for our new eco-friendly water bottle"*

- **Lead Agent** plans: assigns a Research Agent (identify the key selling points and audience), a Draft Agent (write the announcement using that research), and an Editor Agent (tighten and polish the draft)
- Each agent runs in order, the Draft Agent's prompt literally includes the Research Agent's real output, and the Editor Agent's prompt includes both prior outputs
- The Lead Agent reviews the final draft and delivers it as the finished deliverable, with a short sign-off

## How it works

- Three sequential Claude API calls for the specialist agents, one planning call, one sign-off call — five calls total per run
- Each specialist's prompt explicitly includes the accumulated output of every prior agent, which is what makes this genuine coordination rather than independent parallel generation
- Structured JSON output for the plan and final sign-off; plain text for each specialist's actual work product

## Tech

- HTML / CSS / JavaScript (single file, no build step)
- Claude API, via Anthropic's Artifact runtime
- Multi-agent orchestration pattern (lead/planner + sequential specialist agents)
