---
name: apavin-agents
description: "Run Apavin background agents (inbox replies, follow-ups, LinkedIn posts, custom jobs) and set them up as scheduled tasks so they work while the person is away. Use when the person asks to run an Apavin agent, set up their Apavin agents, make Apavin work in the background, or when a scheduled task asks you to start an Apavin agent run."
---

# Apavin background agents

The person sets up agents in Apavin (Settings, MCP, Background agents): what each one does and when. The thinking
happens here, in the person's own app and on their own plan. Apavin does the rest in the background: it syncs mail,
holds what you write for approval, sends approved messages on time, and shows every run in its log.

## Running one agent

1. `list_background_agents` if you do not have the agent's id.
2. `start_agent_run` with `agent_id`. It returns `run_id`, the `job` in plain steps, and `tools_to_use`. If it returns
   `nothing_to_do`, stop there: no work, no report.
3. Do the job exactly as written, with Apavin's tools. Follow the `apavin` skill's rules for writing.
4. `finish_agent_run` with `run_id` and a report of at most three short lines: what you did, and anything a person
   must do. Set `failed` when the job could not be done, with the reason.

When a scheduled task runs this, nobody is watching: do not ask questions, do not wait for answers, finish the run and
report. Everything outbound already waits for approval in Apavin, so drafting and submitting is the right default.

## Setting up the schedule

When the person asks to put their agents on a schedule:

1. `list_background_agents` and show them each agent with its schedule (for example "Inbox replies, every 15 minutes",
   "LinkedIn posts, Tue and Thu at 09:00").
2. For each agent they want, create one scheduled task in this app with your scheduling tool, on that schedule and in
   their time zone, with this prompt, filling in the name and id:

   > Run my Apavin agent "NAME" (agent_id ID): call start_agent_run with that agent_id, do the job it returns with
   > Apavin's tools, then call finish_agent_run with the run_id and a three-line report.

3. Confirm what you scheduled in one line per agent.

If this app has no scheduling tool, say so and give them the prompt above to paste into a scheduled task themselves.
Apps differ in how often a scheduled task may run; if every 15 minutes is not allowed, use the shortest interval it
allows and say which.
