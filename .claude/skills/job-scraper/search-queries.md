# Search Queries for Job Scraper

<!-- Market: Boston, MA, United States (candidate based in 02135) -->

## Search Sites

Primary (US job market):
- **linkedin.com/jobs** - LinkedIn job listings (filter: Boston, MA / Massachusetts)
- **indeed.com** - largest US job board
- **glassdoor.com** - job board + company reviews
- **ziprecruiter.com** - US job board

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies

## Query Categories

Queries are grouped by priority. Each query should be combined with location terms
(e.g. "Boston", "Boston, MA", "Greater Boston", "Massachusetts", "Remote") where the
site supports it. Candidate is open to remote and hybrid roles.

### Priority 1: Customer Service & Administrative

Strongest match: direct experience in customer-facing retail (CVS Health) and
front-desk/admin coordination (Pelham Fritz Recreation Center internship).

```
site:linkedin.com/jobs "Customer Service Representative" "Boston, MA"
site:indeed.com "Customer Service Representative" Boston
site:linkedin.com/jobs "Administrative Assistant" "Greater Boston"
site:indeed.com "Administrative Assistant" Boston OR Remote
```

### Priority 2: Legal / Investigative Support

Matches Law & Society coursework at John Jay College plus hands-on Field Investigator
experience (surveillance documentation, case report writing).

```
site:indeed.com "Legal Assistant" Boston OR Cambridge
site:linkedin.com/jobs "Legal Intern" "Massachusetts"
site:indeed.com "Investigative Assistant" OR "Research Assistant" Boston
site:linkedin.com/jobs "Case Assistant" Boston
```

### Priority 3: Adjacent Entry-Level Roles

Broader net drawing on event-coordination and general office experience.

```
site:linkedin.com/jobs "Front Desk" OR "Office Assistant" Boston
site:indeed.com "Client Services" OR "Client Coordinator" Boston
site:glassdoor.com "entry level" administrative OR "customer service" Boston
```

## Location Filter

Candidate is based in **02135 (Brighton, Boston)**. Not looking for a long commute -
strongly prefers roles in Boston proper or nearby, or fully remote/hybrid.

- Boston, MA and immediate surrounding neighborhoods (Brighton, Allston, Brookline, Cambridge) - PASS
- Remote (US) - PASS
- Hybrid with Boston-area office - PASS
- Anywhere requiring a long commute or relocation outside Greater Boston - FAIL unless remote

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has
not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Notes on the shipped portal CLIs

The `.agents/skills/jobbank-search`, `jobdanmark-search`, `jobindex-search`, and
`jobnet-search` CLI tools target Danish job boards and are not relevant to a Boston, MA
search - leave them installed (they don't hurt anything) but they won't surface useful
results here. Use `.agents/skills/linkedin-search` instead, which is location-agnostic:

```
bun run .agents/skills/linkedin-search/cli/src/cli.ts search -q "customer service representative" -l "Boston, Massachusetts, United States" --jobage 14 --format table
bun run .agents/skills/linkedin-search/cli/src/cli.ts search -q "legal assistant" -l "Remote" --jobage 14 --format table
```

If you want a purpose-built local-market scraper (e.g. for a niche legal or admin job
board), run `/add-portal` and point it at the board's URL.

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also
generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
