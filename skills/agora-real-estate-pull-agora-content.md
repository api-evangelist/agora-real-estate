---
name: pull-agora-content
description: >-
  Pull Agora's published articles, case studies and author profiles from the first-party content API
  — by slug, by category, or as a paged collection.
api: agora-real-estate:agora-website-content-api
base_url: https://websiteapi.agorareal.com/wp-json
auth: none
operations:
- getAgoraV1GetCategories
- getAgoraV1PostsByCategorySlugOrId
- getAgoraV1GetPostsByPostSlug
- getAgoraV1GetCaseStudyByPostSlug
- getAgoraV1GetAllAuthors
- getAgoraV1GetAuthorByAuthorSlug
- getAgoraV1Sitemap
- getWpV2Posts
- getWpV2CaseStudy
- getWpV2Search
generated: '2026-09-12'
method: generated
source: openapi/agora-real-estate-website-content-api-openapi.yml
---

# Pull Agora content

Agora's marketing site is a headless WordPress install and its content API answers anonymously.
There are two ways in: Agora's own `agora/v1` routes, which return pre-joined, site-shaped payloads,
and the stock `wp/v2` routes, which return raw records with full filtering and pagination. Prefer
`agora/v1` when you know the slug; prefer `wp/v2` when you need to page or filter.

## Steps

1. **List what exists.** `GET /agora/v1/get-categories` (`getAgoraV1GetCategories`) returns the
   content categories with `id`, `name` and `slug` — reports-and-research, webinars, gp-hub, blog,
   product-updates, agora-news, deal-makers, compare, learn. `GET /agora/v1/sitemap`
   (`getAgoraV1Sitemap`) returns every published page and post URL in one document.

2. **Pull a category.** `GET /agora/v1/posts-by-category-slug-or-id`
   (`getAgoraV1PostsByCategorySlugOrId`) takes a category slug or id and returns the post list with
   titles, dates, slugs and featured images already resolved.

3. **Pull one article by slug.** `GET /agora/v1/get-posts-by-post-slug/{post_slug}`
   (`getAgoraV1GetPostsByPostSlug`) — the slug is the last path segment of the public URL, e.g.
   `multifamily-syndication`. For a customer story use
   `GET /agora/v1/get-case-study-by-post-slug/{post_slug}` (`getAgoraV1GetCaseStudyByPostSlug`).
   Related reading: `GET /agora/v1/get-more-articles-by-blog-slug/{blog_slug}`.

4. **Resolve bylines.** `GET /agora/v1/get_all_authors` (`getAgoraV1GetAllAuthors`) for the full
   contributor list, or `GET /agora/v1/get-author-by-author-slug/{author_slug}`
   (`getAgoraV1GetAuthorByAuthorSlug`) for one profile.

5. **Page properly when you use wp/v2.** `GET /wp/v2/posts` (`getWpV2Posts`) accepts `page`,
   `per_page` (max 100), `search`, `categories`, `tags`, `author`, `slug`, `after`, `before`,
   `order`, `orderby` and `_fields`. Read `X-WP-Total` (365 posts at last observation) and
   `X-WP-TotalPages`, and follow the `Link: ...; rel="next"` header rather than incrementing blindly.
   `GET /wp/v2/search` (`getWpV2Search`) searches across content types when you do not know which one
   holds the answer.

## Rules

- Read-only. Every operation above is a GET and none needs a credential. Do not attempt writes: the
  write routes require a WordPress session Agora does not issue to integrators, there is no
  idempotency key, and no reversal is documented.
- Use `context=view` (the default). `context=edit` requires authentication and will return
  `rest_forbidden`.
- Request only the fields you need with `_fields` — post payloads carry rendered HTML and are large
  (a single post is ~22KB).
- This is Agora's WEBSITE content. It contains no investor, fund, or transaction data. The
  investment-management platform API is a separate, tenant-scoped, credential-gated surface that
  Agora does not document publicly.
