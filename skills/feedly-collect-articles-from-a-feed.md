---
name: feedly-collect-articles-from-a-feed
description: Poll a Feedly AI Feed, Folder or Board for new articles on a schedule without gaps or duplicates. Use when ingesting Feedly intelligence into a SIEM, SOAR, data warehouse or newsletter pipeline.
api: openapi/feedly-streams-openapi.yml
operations: [collect-articles, get-list-of-ai-feeds, get-list-of-team-boards, getTeamFolders]
generated: '2026-08-12'
method: generated
source: openapi/feedly-streams-openapi.yml, openapi/feedly-alerts-openapi.yml, openapi/feedly-enterprise-openapi.yml, openapi/feedly-enterprise-collections-openapi.yml, https://developers.feedly.com/docs/understanding-continuation
---

# Collect articles from a Feedly stream

Every collection surface in Feedly is a **stream**, addressed by a `streamId`. AI Feeds, Folders and
Team Boards are all streams, so one operation reads all three.

## Authentication

All operations take a bearer token in the `Authorization` header:

```
Authorization: Bearer <FEEDLY_API_TOKEN>
```

Tokens are generated at <https://feedly.com/i/team/api> by an account admin and are Enterprise-only.
See `authentication/feedly-authentication.yml`.

## Step 1 — find the streamId

Pick the operation that matches the surface you want:

- `get-list-of-ai-feeds` — `GET /v3/alerts/` returns the team's AI Feeds.
- `get-list-of-team-boards` — `GET /v3/enterprise/tags` returns team board streamIds.
- `getTeamFolders` — `GET /v3/enterprise/collections` returns team folders with their feeds.

A streamId looks like `enterprise/<team>/category/<uuid>` or `enterprise/<team>/tag/<uuid>`.

## Step 2 — collect the articles

`collect-articles` — `GET /v3/streams/contents`

| Parameter | Required | Notes |
|---|---|---|
| `streamID` | yes | **URI-encode it.** The `/` and `+` characters in a streamId will break the request otherwise. |
| `count` | no | 1–100, default 20. |
| `newerThan` | no | Epoch ms. **Cannot be older than 31 days ago** — the API will not serve a longer window. |
| `olderThan` | no | Epoch ms. |
| `continuation` | no | Page token from the previous response. |
| `includeAiActions` | no | Default true; returns AI Actions on each article. |
| `similar` | no | Default true; returns `numRelatedEntries`. |

## Step 3 — page with `continuation`, not with offsets

The response envelope is:

```json
{ "id": "<streamId>", "updated": 1649805845596, "continuation": "180056e12c9:1a7979e:26e2bd2e", "items": [ ... ] }
```

Loop while `continuation` is present, passing it back on the next call. **When `continuation` is
absent from the response, you have reached the end of the stream — stop.** Do not treat an empty
`items` array alone as the terminator.

## Step 4 — poll without gaps or duplicates

Persist the `updated` value from each successful run and pass it as `newerThan` on the next run.
This is the watermark; do not use wall-clock time, because article ingestion is not instantaneous.

Do not combine `newerThan` with `continuation` on the same paging loop — finish the page walk for a
watermark first, then advance the watermark.

Because the `newerThan` window is capped at 31 days, a pipeline that stops for more than a month
cannot backfill the gap through this endpoint.

## Deduplication

Articles legitimately appear in more than one stream, and the same story is often republished. Two
mechanisms exist:

- Deduplicate on the article `id` (the entry id) in your own store — always correct.
- Feedly ships an **experimental** deduplication feature for the Streams API; see
  <https://developers.feedly.com/docs/removing-duplicates-from-streams-api>. Treat it as experimental
  and keep your own id-based dedupe.

## Rate limits

100,000 requests per month per token. Every response carries `X-RateLimit-Count`,
`X-RateLimit-Limit` and `X-RateLimit-Reset` (seconds until reset). On exhaustion the API returns
**429**. Read the headers on every response rather than counting locally — see
`rate-limits/feedly-rate-limits.yml`.

## Errors

`400` invalid JSON or wrong value types, `401` missing/expired token, `403` unauthorized access to an
enterprise collection, `429` rate limit. The envelope is `{"errorMessage": "...", "errorId": "..."}`
(some responses use `errorCode`/`requestId`/`errorMessage`). Quote the `errorId` or `requestId` when
contacting Feedly support. See `errors/feedly-problem-types.yml`.

There is **no idempotency-key mechanism** on this API; retries of writes are not deduplicated by the
server. Reads are safe to retry.
