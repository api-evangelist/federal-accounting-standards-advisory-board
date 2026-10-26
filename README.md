# Federal Accounting Standards Advisory Board (federal-accounting-standards-advisory-board)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

The Federal Accounting Standards Advisory Board (FASAB) is the U.S. federal advisory body designated to set
generally accepted accounting principles for the federal government and its component reporting entities.
FASAB issues Statements of Federal Financial Accounting Standards (SFFAS), technical releases, interpretations
and staff implementation guidance, consolidates them into the FASAB Handbook, and runs the public due-process
cycle of board and ASIC meetings, active projects and exposure drafts open for comment.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/federal-accounting-standards-advisory-board/refs/heads/main/apis.yml)

## The API surface, and what it is

FASAB publishes **no developer program, no API documentation and no machine-readable specification.**

Its website runs on WordPress and serves the standard WordPress REST API anonymously at
`https://fasab.gov/wp-json/`. That is a real, callable, read-only content API over 402 pages
(Standards & Guidance, handbook-by-chapter, active and archived projects, board and ASIC meeting material,
briefing documents, training and the resources library), 4 posts, 214 media records, the site taxonomies,
public author records and cross-type site search.

The OpenAPI in `openapi/` is **derived by API Evangelist, not published by FASAB.** Every path, method,
parameter and parameter schema comes from the live route discovery document — saved verbatim alongside it as
`federal-accounting-standards-advisory-board-wp-routes-original.json` (519 routes) — and all 28 operations
were individually confirmed to return HTTP 200 to an unauthenticated request on 2026-09-09. The confirming
URL and status are recorded on each operation as `x-verified`.

**It is read-only.** Collection responses carry `Allow: GET`, and the whole administrative and plugin surface
(`/wp/v2/settings`, `/plugins`, `/themes`, `/block-types`, `/users/me`, revisions, and the `wp-abilities/v1`
namespace) returns `401 rest_forbidden` anonymously. None of it is modelled.

**Important limit.** The authoritative pronouncements — the FASAB Handbook, SFFAS statements, technical
releases and interpretations — are PDFs on `files.fasab.gov`, linked from page content. This API will tell an
agent which page carries a standard and where its PDF lives. It will not return the text of a standard as
structured data.

## What FASAB does not publish

No SDKs or client libraries in any registry, no CLI, no Postman collection, no GitHub organisation, no MCP
server, no A2A agent card, no `/llms.txt`, no `/.well-known/` documents of any kind, no webhooks or events,
no GraphQL, gRPC or SOAP surface, no status page, no changelog, no sandbox, no OAuth scopes, no trust centre
and no published certifications. Each of those is recorded as a probed absence in the artifacts, with the
URL and status returned.

## Scope

- **Type:** Index
- **Position:** Producing
- **Access:** 3rd-Party

## Tags

 - Accounting, Federal Government, Standards, Financial Reporting, Government, Regulations, Content, Publications

## Timestamps

- **Created:** 2024-12-25
- **Modified:** 2026-09-09

## Common Properties

- [Website](https://fasab.gov/)
- [Blog](https://fasab.gov/newsroom/)
- [Blog RSS](https://fasab.gov/feed/)
- [Support / Contact](https://fasab.gov/about-fasab/contact-information/)
- [LinkedIn](https://www.linkedin.com/company/federal-accounting-standards-advisory-board)

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
