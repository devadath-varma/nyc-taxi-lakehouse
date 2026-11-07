---
title: "Agile Approach to the Big Data Project"
subtitle: "Team T03 | NYC Yellow Taxi 2023 lakehouse pipeline | ABDA Skill-Gap Capstone"
---

# 1. Why we use Agile

Our project is a data pipeline built on Databricks by six people who are new to coding, with a fixed end date (presentations 30 Nov to 2 Dec 2026) and four checkpoints that give us written feedback along the way. That is a good fit for Agile: we do not try to plan everything on day one and build it in one go. We work in short **sprints**, each ending in something that runs and can be reviewed, and we change the plan when feedback or errors tell us to.

Agile also matches our job posting (Cognizant, Azure Data Engineer returnship), where the work is done in a team using version control, code reviews and regular communication with business users. Practising that way of working is part of the gap we are closing.

# 2. The framework we use: Scrum-style sprints with a Kanban board

We keep it deliberately light, because a team of six students with other classes cannot run full Scrum.

| Agile idea | How we apply it |
|---|---|
| Product Owner (the client) | The fleet manager in our business problem, represented by the job posting and the instructor's checkpoint feedback. The Project Captain keeps the backlog in the order the client would want. |
| Scrum Master (facilitator) | Project Captain: runs the stand-up, removes blockers, keeps the board up to date. |
| Development team | All six members. Each holds one working role (below) and swaps roles after Checkpoint 3 so everyone tries something new. |
| Product backlog | A list of user stories on a GitHub Projects board in our repository. |
| Sprint | One checkpoint period, from one Tuesday submission to the next. |
| Increment | Something that runs: a notebook, a table, a chart. Not a half-finished plan. |

**Working roles (from the course guide):** Data Wrangler (builds bronze and silver), Analyst (gold tables and checks), Storyteller (dashboard and report), Governance Guardian (licence, privacy, quality log), Project Captain (facilitation and planning). The sixth member shares a role.

# 3. Sprint plan against the course calendar

| Sprint | Dates | Goal | Output (checkpoint) | Marks |
|-------|--------|--------------|--------------|------|
| 1 | 20 to 27 Oct | Pick the job posting, rate our skills, find the top 3 gaps | Posting link, saved copy, gap matrix (CP1) | 4 |
| 2 | 27 Oct to 3 Nov | Design the project: problem, dataset and licence, pipeline steps tied to gaps | One-page plan (CP2) | 3 |
| 3 | 3 to 17 Nov | Build the bronze and silver layers and the first quality checks | Notebook and five-line progress note (CP3), plus Git repository | 2 |
| 4 | 17 to 24 Nov | Build gold tables, dashboard, Databricks Job, README, governance note | Finished pipeline (CP4) | 5 |
| 5 | 24 Nov to 2 Dec | Final report (27 Nov) and presentation with mock interview | Report and presentation | 6 |

Sprint 3 is two weeks long because the data volume (about 38 million trips) and the Free Edition daily quota make us build on January first and run the full year later.

# 4. Product backlog (user stories)

Each story is written from the point of view of a user, has a clear "done" test, and is tied to one of our three gaps (Azure and big data tools, ETL pipelines, Python and PySpark).

| ID | As a... I want... so that... | Gap | Sprint | Done when |
|-----|-------------------------|-----------|------|-------------------|
| US1 | As the fleet manager I want the raw 2023 taxi data stored untouched so we can always go back to the original. | Azure / big data | 3 | Bronze table holds every file with file name and load time; row counts per file shown. |
| US2 | As an analyst I want clean, correctly typed trips with zone names so I can query them without fixing data each time. | Python / PySpark, ETL | 3 | Silver table passes the range and null checks in the notebook. |
| US3 | As the governance guardian I want every removed trip to have a recorded reason so nothing disappears unexplained. | ETL | 3 and 4 | Quality log adds up: bronze rows = duplicates + removed + silver, for every month. |
| US4 | As the fleet manager I want trips and fare per minute by pickup area and hour so I can send drivers to the right places. | ETL, Python | 4 | Gold table by area and hour exists and is checked against silver totals. |
| US5 | As the fleet manager I want demand and earnings by weekday and month so I can plan shifts. | ETL, Python | 4 | Gold table by weekday and month exists. |
| US6 | As the fleet manager I want airport versus city trips and card tip rates so I know if airport waits pay off. | ETL, Python | 4 | Gold table with airport flag and tip rate (card trips only). |
| US7 | As the fleet manager I want a dashboard that answers my three questions. | Communication | 4 | Heat map, trend chart and airport comparison are on one dashboard. |
| US8 | As a team we want the notebooks to run in order as one Databricks Job. | Azure / big data | 4 | Job runs bronze, silver, gold with no manual steps (if quota allows). |
| US9 | As a classmate I want a README and a governance note so I can rerun the project in one sitting. | Communication | 4 | A classmate follows the README and gets the same tables. |
| US10 | As the instructor I want a report and a clear recommendation with its limits. | Communication | 5 | Recommendation uses the "Because the data shows..." format. |

The backlog is ordered by value to the client and by dependency: silver cannot start before bronze, and gold cannot start before silver. We add a story whenever we find new work (for example, "handle column name changes between months" was added during Sprint 3).

# 5. The routine inside every sprint

| Event | When | Length | What happens |
|-----|-------|---|-----------------|
| Sprint planning | Start of each sprint (the day after a checkpoint is submitted) | 30 to 45 min | Read the instructor's feedback, choose stories for the sprint, split them into small tasks, assign each task to one person. |
| Daily work on the board | Every day | as needed | Move cards: Backlog, Ready, In progress, In review, Done. Maximum two cards in progress per person. |
| Stand-up | Once a week on a fixed day (course rule) | 15 min | Each person answers three questions: what I did, what blocks me, what I do next. |
| Peer review | Before a story is Done | 15 min | A second member reads the notebook or the pull request and runs it. |
| Sprint review | When written feedback arrives (within three working days) | 20 min | Compare what we submitted with the feedback; update the backlog. |
| Retrospective | After each checkpoint | 20 min | Start, stop, continue (template in section 8); results go into the learning log. |

# 6. Definition of Done

A story is Done only when **all** of these are true:

1. The notebook runs from top to bottom without errors, first on January only, then on the full year.
2. The built-in checks at the end of the notebook pass (row counts add up, values in range).
3. Code is committed to the GitHub repository with a clear message that names the story (for example "Add silver quality log (US3)").
4. A second team member has reviewed it and run it.
5. Each notebook cell has a short explanation, so any member can explain every line in the mock interview.
6. A dated entry is added to the learning log. If an AI assistant helped with code or writing, the log says so.

# 7. How Git supports the way we work

* One shared repository, `nyc-taxi-lakehouse`. Raw data files are never committed (they are large and the licence is stated in the README); only code and documents are.
* Notebooks live in `notebooks/`, submissions in `submission/`, write-ups in `docs/`.
* Small, frequent commits. A message says what changed and why, and names the story ID.
* For each story, one member works on a branch (for example `feature/silver-quality-log`) and opens a **pull request**; a second member reviews it before it is merged into `main`. This is our version of the code review named in the job posting.
* If Git feels too heavy at first, the minimum is: upload the notebook to the right folder on the GitHub website, with a good commit message, and ask a teammate to review it.

# 8. Learning from each sprint

**Retrospective template** (20 minutes after each checkpoint):

| Start doing | Stop doing | Keep doing |
|---|---|---|
| | | |

**Learning log entry format** (one shared page, every member adds entries):

`Date | Name | What broke | How we fixed it | What we learned | What we do next`

Because both the retrospective and the learning log feed the final report (section 5 of the report: what broke, how we fixed it, what we would do next), the way we work is also evidence for the individual contribution mark.

# 9. How Agile shaped Sprint 3 (Checkpoint 3)

| Choice | Agile reason |
|---|---|
| Build everything on January only first, then run the full year once. | Small increment first: errors are found early, cheaply, and without using up the Free Edition daily quota. |
| Split the work into two notebooks (bronze, silver) plus a single combined submission notebook. | Each notebook is one story that can be reviewed and rerun on its own; the combined one is the increment we hand in. |
| Add checks at the end of each notebook that stop the run if something is wrong. | Quality is built in, so "Done" is a test, not an opinion. |
| Record every removed trip with a reason in a quality log. | Transparency for the client and for the Governance Guardian. |
| Rerunning a notebook never creates duplicates (it overwrites bronze and silver). | Safe to repeat, so every member can run the finished notebooks on their own account. |

**Sprint 3 timeline**

| Date | Activity |
|---|---|
| 7 to 8 Nov | Sprint planning, download the data, create the GitHub repository and board |
| 9 to 10 Nov | Upload January, run bronze and silver, review results as a team |
| 11 to 12 Nov | Upload the other 11 months, run the full year (bronze one day, silver the next if the quota requires it) |
| 13 to 14 Nov | Check the quality log, export the notebook, commit to GitHub, peer review |
| 15 to 16 Nov | Progress note, retrospective, learning log, submit (due Tuesday 17 Nov, 6 pm) |

# 10. Risks and how we handle them the Agile way

| Risk | Early warning | Response |
|---|---|---|
| Daily Free Edition quota runs out | Compute stops mid-run | Run heavy steps one per day; test on January; no looping jobs. |
| A member falls behind (new to coding) | Same card in progress for more than three days | Pair up on the card; split it smaller; swap roles after Checkpoint 3. |
| A notebook error blocks everyone | Nobody can move a card | Raise it at once in the team chat, not only at the stand-up; log it in the learning log. |
| Feedback asks for a change | Written feedback after each checkpoint | Re-order the backlog at the next sprint planning. |
