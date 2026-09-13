# Agora Real Estate

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

Agora (**[agorareal.com](https://agorareal.com/)**) is a real estate investment management platform
for general partners, syndicators, owners/operators and investment firms — fundraising and investor
onboarding, an investor portal and investor CRM, digital subscriptions, data rooms, cap table and
transaction management, waterfall automation, capital calls, ACH and cross-border payments, K-1 and
document management, investor reporting, and integrated fund accounting, bookkeeping and tax
services. Pricing starts at $749/month (Essential); Pro and Enterprise are quoted.

## What this profile found (2026-09-12)

| Surface | Status |
|---|---|
| **Agora Website Content API** — `https://websiteapi.agorareal.com/wp-json` | **Public and callable anonymously.** Headless WordPress with a first-party `agora/v1` namespace of 25 Agora-authored routes. No OpenAPI is published by Agora; the specification in `openapi/` was **derived** from the live self-describing route index (HTTP 200, 326,828 bytes). |
| **Agora Authorization Server** — `https://auth.agorareal.com` | **Discovery documents public.** OpenID Connect discovery and RFC 8414 authorization-server metadata both served anonymously; authorization-code + PKCE S256, device code, refresh token; scopes `openid profile email offline_access`. |
| **Agora Client Platform API** — `https://{tenant}.acp.agorareal.com/api` | **Gated.** Multi-tenant (390 client-platform hosts and 389 investor-portal hosts in certificate transparency). Every anonymous `/api/*` request returns nginx 502. "API Access" is an Enterprise line item on the pricing page marked *Priced Separately*, with no public reference. |
| **MCP / agent surface** | **Announced, not shipped.** Agora's own release feed schedules "API + MCP" for **2026-09-22** and "Agora Connect" for 2026-10-06; Cortex is waitlist-only. No MCP endpoint answers on any host today, so no `MCPServer` pointer is claimed. |
| **Compliance** | SOC 2 Type II, SOC 1, ISO 27001:2022 and GDPR, all *fully implemented* per Agora's own Scytale-hosted trust center at [trust.agorareal.com](https://trust.agorareal.com/). |

Not found anywhere: a developer portal, API reference, security.txt, status page, agent card, SDK on
any package registry, or any published rate limit. The one programmatic write path a third party can
reach today is Agora's Zapier app.
