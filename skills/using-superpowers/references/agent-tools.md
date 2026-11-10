# Agent Tool Notes

Agent is the reference harness: skills speak its vocabulary
(`Agent` for a subagent dispatch, todos, `Skill`). These notes cover the
one place Agent can run a plan cheaper than the skills' default
shape. It is opt-in by your human partner and changes nothing the skills
require.

## Cheaper orchestration for subagent-driven development

The controller session is the most expensive seat in a
superpowers:subagent-driven-development run: it reads every dispatch
result and every report, and it usually runs on the session's most
capable model. Agent supports nested subagents (three layers below
the main conversation by default; `Agent_CODE_MAX_SUBAGENT_SPAWN_DEPTH`
adjusts it), so the whole loop can run one layer down.

When your human partner asks for it â€” or has said the session model is
too expensive to spend on coordination â€” dispatch ONE orchestrator
subagent on a mid-tier model with the plan path and the instruction to
use superpowers:subagent-driven-development end to end. The orchestrator
dispatches its own implementers and reviewers per that skill's Model
Selection; the workspace and ledger live on disk, so nothing is lost to
the extra layer. Its final message must carry the "Rulings I made" list
verbatim â€” that list is how the decisions reach your human partner, and
you relay it, not summarize it.

Do this only for a whole plan. Nesting a single task's dispatch buys
nothing and adds a seat.

## Multi-round council deliberation (`superpowers:council-grade`)

When running `superpowers:council-grade`:
- **Round 1 (Parallel Blind Grading):** Issue 3 `Agent` (or `Task`) tool calls (`subagent_type: "general-purpose"`) in a single response so all 3 specialists run concurrently.
- **Round 2 & Round 3 (Cross-Deliberation & Mandatory Re-grade):** Resume each of the 3 council subagents in parallel in a single response using the `resume` parameter (`resume: "<agentId>"`), or issue 3 parallel `Agent` dispatches carrying the full Round 1 critiques / Round 2 upgraded artifact.

