# A Local-First Personal Data Platform and Productivity Suite

A suite of connected personal tools that help one person understand how they spend their time,
suggest what to work on, and stay motivated. 

The unifying bet: run it on your own hardware with local models, 
so the system can see everything about you without that data ever leaving your control.

---

## General idea

- Most other tools are narrow and cloud-hosted: each sees only a slice of you, and that slice
    sits on someone else's servers.
- These projects instead share one local pool of personal data. Each app both contributes to and
    reads from it. It is a graph instead of a pipeline: a finance app records a transaction for its own
    purpose, but that same timestamp is also a clue about how time was spent (for the time tracker),
    and if it was a food purchase, a clue about nutrition.
- The more of your life the system observes, the better it reasons, so the design leans toward
    maximum coverage.

## Why local storage + local models

- That coverage is the catch: the aggregate is an extremely revealing profile, and it is only safe
    to gather if the data never leaves your control. That is the whole point of going local.
- Local models are now good enough for the bulk of the reasoning involved (classification, tagging,
    summarization, retrieval), so keeping everything on-device costs little in capability.
- The stance:
    - Private data is processed only by local models on the user's machine.
    - When data must leave a device (for example, syncing between a work desktop and a laptop), it is
        end-to-end encrypted.
    - Only genuinely public content (e.g. an open-source commit), or content from a private source
        after a human-in-the-loop check, may optionally go to a cloud model.

---

## The projects

One shared, local, privacy-tagged data store sits underneath. 
Each project reads and writes through a clear contract, 
so a new data source or a new app plugs in without rearchitecting the others.

### Logger: automated time and activity capture

- Goal: an accurate picture (at least 80 percent) of how time is actually spent, shown in a way that
    motivates progress toward goals.
- Ideas and features:
    - Core metric: total deep-work hours, with trends
    - Reconstructs the day from passive signals (e.g. active-window titles, wearable
        heart rate and steps, calendar, commits, expense timestamps, voice notes, and optional periodic
        screenshots captioned by a local vision model) so manual logging is reduced. The user corrects
        errors rather than entering everything. Initially rules based, can experiment with local model to reason out the reconstruction
    - Classify activity by cross-referencing sources: high heart rate plus steps means exercise, an
        IDE in the foreground means likely working, and so on. Heuristics and rules first, learned models
        later once a clean labelled history exists.
    - Tag entries so the whole log becomes searchable, with embeddings surfacing similar past moments
        when you revisit an event.
    - Reconcile overlapping and conflicting sources (planned vs. logged vs. auto-reconstructed) into
        one timeline, with gaps in coverage made obvious.
    - Keep conclusions, not raw feeds: since the model can watch continuously on-device, store mostly
        the derived analysis and only occasional raw signal for error-checking, which keeps storage tractable.
    - Reflection dashboards at different timescales, with drill-down from a macro summary to minute-level
        detail; a local model summarizes the week, drafts first-pass reflections, and flags recurring patterns.
    - Efficiency and waste views: procrastination time, focus-session length.
    - comparison against the average person (drawing on public time-use survey data)
    - Achievement logging: record meaningful milestones at various levels, mostly automated but with
        manual entry allowed, so the habit survives busy periods (useful for career). These records also
        help estimate how long real work actually takes.
    - Life visualiser: a private social feed of one's own life, to revisit special moments for
        reflection and motivation.
- Why local: this is a continuous record of where a person is, what they are doing on their screen,
    and their health info. It also accumulates into autobiographical memory, including moments a person
    would least want indexed by an outside service.

### Task Master: a gamified, evidence-based task manager

- Goal: unify tasks scattered across many tools into one view, then recommend what to do now, and use
    game mechanics to sustain motivation. This is the dashboard for tasks to be completed by a human.
- Ideas and features:
    - Aggregate tasks the user already captures elsewhere (notes, task apps, code issue trackers)
        rather than requiring manual re-entry.
    - Auto-score and decompose tasks with a swappable LLM: importance, energy required, shallow vs.
        deep, cognitive type, estimated time, broken into schedulable chunks. All overridable.
    - Recommendation system: filter the task pool by the metrics above, because what counts as doable
        fluctuates through the day, e.g. it depends on a person's available slots and the cognitive types
        already exercised that day (to avoid straining any one mode of cognition). The system can also
        infer current state (rule based but potentially local models), such as energy level from activity, to suggest what fits now.
    - Gamification: XP, levels, quests, and variable-ratio (unpredictable) rewards, which are the
        mechanics games use to build habits. Routines can appear semi-randomly to avoid dread.
    - Verifiers that auto-complete quests from real signals (fitness data, commits, local model judgement) for reduced friction

### ProjectGen -- idea, task, and research automation

- Goal: capture ideas and tasks anywhere, then let AI agents classify, route, and process them. This is the dashboard for tasks to be completed by AI.
- Ideas and features:
    - Extract tasks from personal notes, classify them by type (e.g. web research, ideation, coding task), and rewrite sparse notes into actionable items
    - A privacy classifier that flags how sensitive a piece of content is before anything is routed to
        an external service.
- Why local: the notes they come from are personal. Can be a lot of mental overhead to maintain a personal vs public notebook

### AI Advisor -- your own lessons, surfaced at the right moment

- Goal: help the user apply their own prior lessons at the moment they are relevant, grounded in their own notes
- Ideas and features:
    - Build a local embeddings/RAG knowledge base from personal notes, reflections, and lesson
        documents, and return relevant advice for a query, a daily goal, or recent activity.
    - Real-time retrieval: monitor current activity (eg, the task being worked on, from the logger project's data) and surface matching advice without being asked
    - Contextual retrieval: derive the conditions under which a lesson applies (a book's advice is
        situational) and match those conditions to the current situation, not just surface similarity. Local models can infer conditions (e.g. predicates?)
    - Forward advising: the night before, scan upcoming calendar events and goals, then prepare a short
        brief to read in the morning.
    - Real-time warnings: flag when user is not adhering to their intent, e.g. recent activity drifts from stated goals, doing low-priority work when intent is to focus on high priority tasks
    - Planning automation: compare planned vs. actual, re-estimate project effort from historical data,
        suggest prioritization and timing based on energy levels, and slot small tasks into small gaps.
- Why local: Sensitive info like personal reflections, admitted weaknesses, and the raw material of how someone thinks.

### Downstream trackers -- finance, nutrition, habits

- Goal: automate the tracking by pulling from sources instead of relying on manual entry to reduce friction in gathering data for analysis.
- Ideas and features:
    - Finance: tally income, expenses and balance sheet from sources like receipts, emails, and financial (e.g. bank) statements
    - Nutrition: tally food consumption and macros, tied to other project's data for automation (e.g. finance data since a food purchase usually implies consumption.)
    - Verify habits automatically from various signals (e.g. activity trackers, computers) and visualize adherence, highlighting the ones being missed.
