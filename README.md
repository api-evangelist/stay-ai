# Stay AI (stay-ai)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Stay AI (formerly Retextion) is a subscription retention and growth platform for Shopify direct-to-consumer (DTC) brands. It pairs a no-code, fully customizable customer portal with an **ExperienceEngine** for personalized promotions and upsells across the subscriber journey and a **RetentionEngine** for AI-driven passive and active churn prevention, plus analytics for forecasting subscription revenue.

Stay AI exposes a **documented public REST API** at base `https://api.retextion.com/api/v2`, authenticated with an API key sent in the `X-RETEXTION-ACCESS-TOKEN` header. API keys are created from **Settings > API keys** in the Stay dashboard. The API is included with the platform subscription (no separate API-only tier). Full reference documentation lives at [https://docs.stay.ai](https://docs.stay.ai), with an agent-facing index at [https://docs.stay.ai/llms.txt](https://docs.stay.ai/llms.txt).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/stay-ai/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/stay-ai/refs/heads/main/apis.yml)

## Access Model

- **Public, documented REST API** — not gated behind a partner-only program. Any merchant on the Stay AI Shopify app can generate an API key and call the endpoints below.
- **Authentication** — API key in the `X-RETEXTION-ACCESS-TOKEN` request header. Invalid or missing keys return `401 Unauthorized`.
- **Webhooks** — Stay AI delivers asynchronous events (e.g. `SUBSCRIPTION`, `FAILED_PAYMENT`, `SUCCESSFUL_PAYMENT`) via **outbound HTTP webhooks** to a merchant-registered URL. Each request is signed with a JWT (HS256, `iat` required, no `exp`) in the `x-retextion-webhook-token` header, keyed by the merchant API key, for verification.
- **No public WebSocket API** — the platform's public surface is request/response REST plus outbound webhooks; there is no documented `ws://`/`wss://` transport (see `review.yml`).

The paths, methods, query parameters, path parameters, and authentication in this entry are taken directly from the Stay AI developer documentation. The request/response **body schemas** in `openapi/stay-ai-openapi.yml` are simplified representations of the documented surface; consult the live reference for full payload details.

## Tags

- Subscriptions
- Retention
- Churn
- Shopify
- Ecommerce
- DTC

## Timestamps

- **Created:** 2026-07-10
- **Modified:** 2026-07-10

## APIs

### Stay AI Subscriptions API

Query subscriptions by customer email, status (`ACTIVE`, `PAUSED`, `CANCELLED`), and created date; retrieve a subscription by ID; and manage the subscription lifecycle — cancel, change frequency, update and remove line items, set the shipping address, add order notes, and attach metadata.

- **Human URL:** [https://docs.stay.ai/reference/query-all-subscriptions](https://docs.stay.ai/reference/query-all-subscriptions)
- **Base URL:** `https://api.retextion.com/api/v2/subscriptions`

### Stay AI Subscription Orders API

Query recurring subscription orders by created and updated date windows, and trigger a new recurring charge for a single subscription ("order now").

- **Human URL:** [https://docs.stay.ai/reference/query-orders](https://docs.stay.ai/reference/query-orders)
- **Base URL:** `https://api.retextion.com/api/v2`

### Stay AI Selling Plans API

List selling plan groups, retrieve a group by ID, and create or update selling plan groups — the Shopify selling-plan configuration defining subscription offers, frequencies, and discounts.

- **Human URL:** [https://docs.stay.ai/reference/query-selling-plan-groups](https://docs.stay.ai/reference/query-selling-plan-groups)
- **Base URL:** `https://api.retextion.com/api/v2/selling-plan-groups`

### Stay AI Catalog API

Retrieve the entire subscription-eligible product catalog, or fetch a single product and its variants by Shopify Product ID.

- **Human URL:** [https://docs.stay.ai/reference/get-catalog](https://docs.stay.ai/reference/get-catalog)
- **Base URL:** `https://api.retextion.com/api/v2/products`

### Stay AI Customer Portal API

Generate an authenticated no-code customer portal link for a subscriber, identified by email or phone, so customers can self-manage their subscriptions.

- **Human URL:** [https://docs.stay.ai/reference/generate-portal-link](https://docs.stay.ai/reference/generate-portal-link)
- **Base URL:** `https://api.retextion.com/api/v2/subscriptions`

### Stay AI Webhooks API

List, create, and delete outbound webhook subscriptions for events such as `SUBSCRIPTION`, `FAILED_PAYMENT`, and `SUCCESSFUL_PAYMENT`. Delivered requests are JWT-signed for verification.

- **Human URL:** [https://docs.stay.ai/reference/create-webhook-subscription](https://docs.stay.ai/reference/create-webhook-subscription)
- **Base URL:** `https://api.retextion.com/api/v2/webhooks`

### Stay AI Account and Data API

Read merchant account settings and trigger bulk data exports for subscriptions and orders.

- **Human URL:** [https://docs.stay.ai/reference/query-account-settings](https://docs.stay.ai/reference/query-account-settings)
- **Base URL:** `https://api.retextion.com/api/v2`

## Pricing

Stay AI is sold through the Shopify App Store with a single published plan: **$499 / month + 1% + $0.19 per transaction**, with a **30-day free trial**. The API is included with the platform subscription. Larger or custom arrangements are handled through Stay AI sales. See `plans/stay-ai-plans-pricing.yml` and `finops/stay-ai-finops.yml`.

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/stayai)
- [Website](https://stay.ai)
- [Documentation](https://docs.stay.ai)
- [Sign Up (Shopify App Store)](https://apps.shopify.com/stayai-subscriptions)
- [Plans](plans/stay-ai-plans-pricing.yml)
- [Rate Limits](rate-limits/stay-ai-rate-limits.yml)
- [Fin Ops](finops/stay-ai-finops.yml)
- [Blog](https://stay.ai/blog)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
