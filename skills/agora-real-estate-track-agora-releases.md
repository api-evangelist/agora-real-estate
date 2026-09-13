---
name: track-agora-releases
description: >-
  Read Agora's public "Season of Innovation" release calendar from its own API and report what
  shipped, what is scheduled, and which entries touch the API or MCP surface.
api: agora-real-estate:agora-website-content-api
base_url: https://websiteapi.agorareal.com/wp-json
auth: none
operations:
- getAgoraV1GetAiNewReleasesPosts
- getAgoraV1GetAiNewReleasesFilters
- getWpV2AiNewRelease
generated: '2026-09-12'
method: generated
source: openapi/agora-real-estate-website-content-api-openapi.yml
---

# Track Agora releases

Agora publishes a dated product release calendar and serves it as JSON with no credential. Use this
to answer "what did Agora ship" and "when does the API land" without scraping the marketing page.

## Steps

1. **Fetch the release feed.** `GET /agora/v1/get_ai_new_releases_posts`
   (`getAgoraV1GetAiNewReleasesPosts`). No parameters, no auth. Returns an array of release objects
   with `title`, `description`, `date` (e.g. "September 22"), `month`, `year`, `slug`, `post_url`
   and a `taxonomies` block carrying `release_product` and `release_update_type`.

2. **Split shipped from scheduled.** Compare `month` + `year` + `date` against today. Entries in the
   future are announcements, not shipped features — say so explicitly when reporting, because the
   feed does not flag it.

3. **Fetch the filter vocabulary if you need to group.**
   `GET /agora/v1/get_ai_new_releases_filters` (`getAgoraV1GetAiNewReleasesFilters`) returns the
   `release_product`, `release_update_type`, `release_audience` and `release_plan` terms with counts.

4. **Filter server-side when you want one product area.** `GET /wp/v2/ai-new-release`
   (`getWpV2AiNewRelease`) accepts `release_product`, `release_update_type`, `release_audience`,
   `release_plan` (term IDs, each with an `_exclude` twin), plus `page`, `per_page`, `order`,
   `orderby`, `after` and `before`. Read `X-WP-Total` and `X-WP-TotalPages` from the response
   headers and follow `Link: ...; rel="next"` — do not guess the page count.

## Rules

- Everything here is a GET. Never send a write verb to this host; the write routes are gated and
  there is no idempotency key and no documented reversal (`conventions/agora-real-estate-conventions.yml`).
- Errors come back as `{"code": ..., "message": ..., "data": {"status": ...}}`, not RFC 9457.
  Branch on `code`, not on the status: this install answers `rest_forbidden` with HTTP 401, not 403
  (`errors/agora-real-estate-problem-types.yml`).
- No rate-limit headers exist on this API (`rate-limits/agora-real-estate-rate-limits.yml`). There is
  no published quota, so keep request volume modest and cache — the release calendar changes every
  two weeks, not every minute.
