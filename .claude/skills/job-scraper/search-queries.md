# Search Queries for Job Scraper

<!-- SETUP: Customize these queries based on your skills, target roles, and location -->
<!-- Market: Boston, MA, United States -->

## Search Sites

Primary (US job market):
- **linkedin.com/jobs** - LinkedIn job listings (filter: Boston, MA / Massachusetts)
- **indeed.com** - largest US job board
- **glassdoor.com** - job board + company reviews
- **ziprecruiter.com** - US job board
- **builtinboston.com** - Boston-area tech job board (Built In Boston)

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies

## Query Categories

Queries are grouped by priority. Each query should be combined with your location terms
(e.g. "Boston", "Boston, MA", "Greater Boston", "Massachusetts") where the site supports it.
Include "Remote" variants where relevant since many Boston-area roles offer hybrid/remote.

### Priority 1: [YOUR_PRIMARY_ROLE_TYPE]

These match your strongest and most desired career direction.

```
site:linkedin.com/jobs "[YOUR_PRIMARY_JOB_TITLE]" "Boston, MA"
site:indeed.com "[YOUR_PRIMARY_JOB_TITLE]" Boston
site:linkedin.com/jobs "[YOUR_KEY_SKILL]" "Greater Boston"
```

### Priority 2: [YOUR_DOMAIN_EXPERTISE]

These match your domain expertise.

```
site:indeed.com [YOUR_DOMAIN_KEYWORD_1] Boston OR Cambridge OR Somerville
site:linkedin.com/jobs [YOUR_DOMAIN_KEYWORD_2] "Massachusetts"
site:builtinboston.com [YOUR_DOMAIN_KEYWORD_1]
```

### Priority 3: [YOUR_ADJACENT_ROLE_TYPE]

Adjacent roles you could pivot into.

```
site:linkedin.com/jobs "[YOUR_ADJACENT_TITLE_1]" [YOUR_KEY_SKILL] Boston
site:indeed.com "[YOUR_ADJACENT_TITLE_2]" [YOUR_KEY_SKILL] Boston
```

### Priority 4: Broader Technical / Consulting

Wider net for general technical roles.

```
site:indeed.com [YOUR_KEY_SKILL] developer Boston
site:linkedin.com/jobs "[YOUR_KEY_SKILL] developer" "Boston, MA"
site:glassdoor.com "technical consultant" [YOUR_DOMAIN] Boston
```

## Location Filter

When evaluating results, verify the job location is within reasonable commute distance
from your home, or is remote/hybrid with acceptable onsite frequency. Define acceptable areas:
- Boston, MA and surrounding areas
- Cambridge, MA
- Somerville, MA
- [ADDITIONAL_ACCEPTABLE_AREA] (e.g. Waltham, Burlington - Rt 128 corridor)
- Remote (US) - [ACCEPTABLE if role is fully remote]
- Outside Massachusetts / requires relocation - too far unless remote

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has
not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Notes on the shipped portal CLIs

The `.agents/skills/jobbank-search`, `jobdanmark-search`, `jobindex-search`, and
`jobnet-search` CLI tools target Danish job boards and are not relevant to a Boston, MA
search - leave them installed (they don't hurt anything) but they won't surface useful
results here. Use `.agents/skills/linkedin-search` instead, which is location-agnostic:

```
bun run .agents/skills/linkedin-search/cli/src/cli.ts search -q "<title/keyword>" -l "Boston, Massachusetts, United States" --jobage 14 --format table
```

If you want a purpose-built local-market scraper (e.g. for Built In Boston or a niche
board), run `/add-portal` and point it at the board's URL.

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also
generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
