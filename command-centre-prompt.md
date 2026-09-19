# The build prompt

This is the prompt for building a Command Centre from scratch ~ not the
daily prompt that runs it (that's in `README.md`, under "The prompt
(redacted)"). Hand this one to an agent once, at setup time, to design and
scaffold the system. Placeholders in `[brackets]` are yours to fill in.

```
Design and set up a personal "Command Centre": a scheduled agent that runs
on its own every day, pulls fresh research plus my own project state, and
publishes one always-current dashboard I can open any time ~ not a new
document each day, the same one, kept current.

CORE REQUIREMENTS

1. Persistent output, not a chat reply. The result has to live somewhere
   I can reopen without re-running anything ~ a hosted page, a pinned
   document, whatever this environment's equivalent is. Every future run
   updates that same place in place.

2. Modules (pick what's relevant, each is independent):
   - AI News: search the last 24 hours for the top 5 stories in [your
     interest areas, e.g. AI enablement, agentic engineering, SaaS
     disruption]. For each, produce a hook, a short-form angle, a
     long-form/thought-leadership angle, and a relevance score against
     those interest areas.
   - Market Intel: search the last 24~48 hours for funding rounds,
     acquisitions, product launches, and policy developments relevant to
     [your domain/region]. Group by category.
   - Pipeline: read from [your persistent state ~ a memory store, a
     shared tracker, a project doc] and report status, next action, and
     priority for every active thread found there, plus a short
     "today's action items" list of what's genuinely time-sensitive
     right now ~ not everything, just what changed or what's urgent.

3. Full replace, not an accumulating log. Every run recomputes "what's
   true right now" for each module. Nothing gets appended to a growing
   list ~ stale entries get dropped, not buried under new ones.

4. Verify before publish. Anything pulled from search gets checked
   against the actual source page before it's included, not just trusted
   from a search snippet or headline.

5. Template continuity. Before rebuilding, read the previous version of
   the output as the layout template ~ reuse its structure/design and
   refresh only the content, so the format doesn't drift run to run.

6. Fail loud. If a data source is unreachable, or the publish step
   itself fails, say so explicitly in the output (or fall back to a
   plain message explaining what failed and why) instead of silently
   producing a thinner result that looks complete.

7. Schedule it to run automatically ~ daily, no manual trigger, no one
   watching it fire.

Ask me whatever you need to scope this (my actual interest areas, where
my project state lives, how often I want it to run, what the very first
version's layout should look like) before building it.
```

## Why it's written this way

- **Requirement 1 comes first on purpose.** Everything else is pointless
  if the output doesn't persist ~ get the agent committed to a stable,
  reopenable destination before it starts reasoning about content.
- **The modules are described as independent and optional.** A prompt
  that hard-codes exactly three modules only works for someone who wants
  exactly those three. Naming the pattern (search + verify + score, or
  read-state + reconcile + surface-urgent) lets it generalize to a
  different mix without a rewrite.
- **Requirements 3~6 are the actual engineering discipline**, and they're
  stated as rules, not left for the agent to infer from the module
  descriptions. This is the same lesson from the daily prompt in
  `README.md`: an agent that isn't told "full replace" will start
  accumulating; one that isn't told "fail loud" will degrade silently.
  Naming the failure mode is what prevents it.
- **The closing line hands scoping back to the agent, not to you filling
  out a form first.** Cheaper to let it ask than to guess wrong and build
  the wrong thing once, then have to redo it.
