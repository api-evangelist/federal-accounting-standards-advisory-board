---
name: Track FASAB board activity and documents for comment
description: Monitor FASAB board meetings, active projects, exposure drafts open for comment, and newsroom announcements using the anonymous fasab.gov WordPress REST API.
api: openapi/federal-accounting-standards-advisory-board-wp-content-openapi.yml
operations: [listPages, getPage, listPosts, listTags, listMedia, search]
method: generated
generated: '2026-09-09'
---

# Track FASAB board activity and documents for comment

FASAB's standards-setting runs on a public due-process cycle: active projects, board and ASIC meeting
material, briefing documents, and exposure drafts open for public comment. All of it is published as
pages on fasab.gov and is readable anonymously.

## Before you start

- Base URL: `https://fasab.gov/wp-json`
- No credential. Read-only.
- The site publishes almost everything as **pages**, not posts — there are only 4 posts in total, so
  do not build a monitor around `listPosts` alone.

## Steps

1. **Find recently changed content.** Call `listPages` with a modification window —
   `GET /wp/v2/pages?modified_after={ISO8601}&orderby=modified&order=desc&per_page=50&_fields=id,link,title,modified,parent`.
   This is the closest thing FASAB has to a change feed for board activity. Poll it rather than
   scraping the site.

2. **Locate the standing sections.** Call `search` for the section, or `listPages` and filter on
   `parent`, to find and then watch these pages:
   - Documents For Comment — `https://fasab.gov/board-activities/documents-for-comment/`
   - Board Meetings — `https://fasab.gov/board-activities/meeting/`
   - Briefing Materials — `https://fasab.gov/board-activities/briefing-materials/`
   - Active Projects — `https://fasab.gov/projects/active-projects/`
   Retrieve each with `getPage` and diff `content.rendered` between polls.

3. **Check the tag taxonomy.** Call `listTags` — `GET /wp/v2/tags`. FASAB uses tags such as
   "AAPC Docs for Comment". Where a tag has a non-zero `count`, filter pages or posts by it with
   `?tags={id}` rather than diffing HTML.

4. **Pick up new documents.** Call `listMedia` —
   `GET /wp/v2/media?orderby=date&order=desc&per_page=20&_fields=id,date,title,source_url,mime_type`.
   New uploads surface here. Note that most large FASAB PDFs live on `files.fasab.gov` and are linked
   from page content instead of being media records, so treat this as a supplement to step 1, not a
   replacement.

5. **Watch announcements.** Call `listPosts` for the small post corpus, and read
   `https://fasab.gov/feed/` (RSS) and the newsroom pages for news releases and the bimonthly
   newsletter. FASAB also runs a listserv at `https://fasab.gov/newsroom/listserv-signup/`, which is
   the channel FASAB itself treats as authoritative for announcements.

## Rules

- **There is no webhook, event stream or AsyncAPI.** Polling is the only mechanism. `modified_after`
  on `listPages` plus the RSS feed is the efficient combination; do not re-crawl the whole site.
- **Respect the cache.** Responses are `cache-control: max-age=60` behind a CDN. Polling faster than
  once a minute returns you the same bytes.
- **Comment deadlines live in page HTML.** The API exposes no structured deadline, status or project
  phase field — there is no project entity, only pages. Parse the rendered content and never infer a
  deadline the page does not state.
- **`X-WP-Total` and `X-WP-TotalPages` are exposed cross-origin** via
  `access-control-expose-headers`, so a browser client can page correctly too.
- **This is not an authoritative feed.** FASAB does not operate this surface as an API and makes no
  availability or compatibility commitment about it. For anything binding, cite the PDF on
  files.fasab.gov, not this API.
