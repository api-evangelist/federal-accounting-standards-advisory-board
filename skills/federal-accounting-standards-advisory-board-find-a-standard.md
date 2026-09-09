---
name: Find a FASAB standard or guidance page
description: Locate the fasab.gov page that carries a federal accounting standard, technical release or interpretation by keyword, then retrieve its content and the URL of its authoritative PDF.
api: openapi/federal-accounting-standards-advisory-board-wp-content-openapi.yml
operations: [search, getPage, listPages]
method: generated
generated: '2026-09-09'
---

# Find a FASAB standard or guidance page

FASAB sets U.S. federal GAAP. Its pronouncements — SFFAS statements, technical releases,
interpretations, staff implementation guidance and the consolidated FASAB Handbook — are described on
fasab.gov pages and published as PDFs on `files.fasab.gov`. This skill gets you from a keyword to the
right page and to the PDF link inside it.

## Before you start

- Base URL: `https://fasab.gov/wp-json`
- No credential. Send no `Authorization` header — the read surface is anonymous.
- Read-only. Every collection answers `Allow: GET`; a write attempt will 401.

## Steps

1. **Search by keyword.** Call `search` — `GET /wp/v2/search?search={term}&per_page=20`.
   Each hit returns `id`, `title`, `url`, `type` and `subtype`. `subtype` tells you whether the hit is
   a `page` (almost always, for standards content) or a `post`.
   Useful terms: the standard number (`SFFAS 54`), the topic (`leases`, `deferred maintenance`,
   `sustainability reporting`), or the document class (`technical release`, `interpretation`).

2. **Retrieve the page.** Take the `id` from the hit and call `getPage` —
   `GET /wp/v2/pages/{id}`. Read `title.rendered` and `content.rendered`.
   Add `?_fields=id,link,title,content,modified` to keep the payload small.

3. **Extract the PDF.** The authoritative document is a link inside `content.rendered`, pointing at
   `https://files.fasab.gov/pdffiles/...`. Parse the anchor hrefs out of the rendered HTML. The API
   does not expose the PDF as a record and does not expose the text of the standard as data — you get
   the page that describes it and the file URL.

4. **Browse instead of searching, when the keyword is vague.** Call `listPages` —
   `GET /wp/v2/pages?per_page=100&page={n}&_fields=id,slug,link,title,parent,modified`. There are 402
   pages; read `X-WP-Total` and `X-WP-TotalPages` from the response headers to page through them.
   The `parent` field gives you the site hierarchy (Standards & Guidance, Projects, Board Activities,
   Resources), so you can walk a section rather than guess slugs.

## Rules

- **Cap and page properly.** `per_page` maxes at 100. Use the `Link` header's `rel="next"` URL, or
  increment `page` until it exceeds `X-WP-TotalPages`.
- **Do not request `context=edit`.** It returns HTTP 401 `rest_forbidden`. The default `context=view`
  is what you want.
- **Handle the WordPress error envelope, not RFC 9457.** Errors arrive as
  `{"code": "...", "message": "...", "data": {"status": 401}}` with content-type `application/json`.
  See `errors/federal-accounting-standards-advisory-board-problem-types.yml`.
- **Expect no rate-limit headers.** None are published or returned. Responses carry
  `cache-control: max-age=60`; be polite rather than assuming a quota exists.
- **Do not trust the route set to be stable.** This surface is exposed by WordPress, not managed by
  FASAB as an API. There is no versioning or deprecation policy. Re-read `GET /wp-json/` if a route
  stops answering.
- **Titles are HTML-escaped.** `title.rendered` contains entities such as `&#8211;`. Unescape before display.
