---
name: feedly-enrich-an-ioc
description: Resolve a raw indicator of compromise (domain, IP address, URL or file hash) into a Feedly entity ID and pull its full intelligence context — threat actor attribution, malware associations, relationships and export links. Use when enriching alerts in a SOC, SOAR or detection pipeline.
api: openapi/feedly-search-openapi.yml
operations: [autocomplete-entities, getEntityDetails, entity-lookup, collect-iocs]
generated: '2026-08-12'
method: generated
source: openapi/feedly-search-openapi.yml, openapi/feedly-iocs-openapi.yml, openapi/feedly-entities-openapi.yml, openapi/feedly-enterprise-openapi.yml, https://developers.feedly.com/docs/ioc-lookup
---

# Resolve and enrich an indicator of compromise

Feedly does not enrich a raw indicator directly. IoC lookup is a **two-step workflow**: resolve the
raw value to a stable Feedly entity ID, then enrich that ID. Skipping step 1 and guessing an entity
ID will not work — entity IDs are opaque and namespaced.

## Authentication

```
Authorization: Bearer <FEEDLY_API_TOKEN>
```

## Step 1 — resolve the raw indicator to an entity ID

`autocomplete-entities` — `GET /v3/search/entities`

| Parameter | Required | Notes |
|---|---|---|
| `query` | yes | The raw indicator, or a keyword to match to an entity / AI Model. |
| `count` | no | Number of suggestions; Feedly recommends 10. |

Pass the raw domain, IP, URL or file hash as `query`. The response returns candidate entities; an
IoC entity ID has the shape:

```
nlp/f/entity/ioc:74fba9a5-04c1-5b42-8b7e-16dc482dc841
```

**Match carefully.** This is an autocomplete endpoint, so it returns candidates ranked by match, not
a single authoritative answer. Confirm the returned entity's label equals the indicator you searched
for before enriching. If nothing matches, the indicator is simply not in the Threat Graph — record
that as a collection gap. Do not substitute a near-match.

## Step 2 — enrich the entity

`getEntityDetails` — `GET /v3/entities/{entityId}`

| Parameter | Required | Notes |
|---|---|---|
| `entityId` | yes (path) | From step 1. **URI-encode it** — it contains `/` and `:`. |
| `withStats` | no | Include mention statistics over time. |

Returns metadata, relationship data, export options and statistics. Export formats available on IoC
entities include **STIX 2.1, MISP, CSV and Markdown**, which is usually the fastest path into an
existing TIP or SIEM.

`entity-lookup` — `GET /v3/entities/{entityId}` on the Entities API is the general-purpose sibling
for non-IoC entities (threat actors, malware, CVEs, companies).

## Step 3 — pivot (optional)

Once you hold an entity, follow it outward:

- `get-threat-actor-relationships` — `GET /v3/ml/relationships/actor/{threatActorId}`
- `get-malware-relationships` — `GET /v3/ml/relationships/malware/{malwareId}`
- `getCveTimeline` — `GET /v3/entities/{entityId}/timeline` for CVSS changes, exploitation reports
  and vendor advisories in chronological order.

Note a real API change here: threat-actor relationships **used to** be returned inline by
`GET /v3/entities/{threatActorId}`. They were moved to the dedicated `/v3/ml/relationships/actor/`
endpoint, and the original operation no longer includes a `relationships` field. Code written against
the old shape will silently see no relationships rather than an error.

## Bulk export instead of per-indicator lookup

If the goal is "every IoC referenced in this feed", do not loop the two-step workflow. Use:

`collect-iocs` — `GET /v3/enterprise/ioc`

| Parameter | Required | Notes |
|---|---|---|
| `streamId` | yes | URI-encoded stream (AI Feed, Folder or Board). |
| `count` | no | 1–100. |
| `newerThan` | no | Epoch ms; capped at 31 days back. |

This returns IoCs with article context in one pass and is far cheaper against the 100,000/month quota.

## Absence is a finding

If resolution returns no entity, or enrichment returns no relationships, record that explicitly. It
is evidence the indicator is not attributed in open reporting — not a failed lookup to retry.

## Rate limits and errors

100,000 requests/month per token; `X-RateLimit-Count`, `X-RateLimit-Limit`, `X-RateLimit-Reset` on
every response; `429` on exhaustion. Errors return `{"errorMessage": "...", "errorId": "..."}`.
See `rate-limits/feedly-rate-limits.yml` and `errors/feedly-problem-types.yml`.
