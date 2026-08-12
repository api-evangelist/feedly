---
name: feedly-triage-a-cve
description: Assess whether a vulnerability warrants emergency patching using Feedly's CVE Insights Card, its timeline, and the Vulnerability Agent's exploitation filters (exploited, PoC, weaponized, CISA KEV, CVSS). Use for vulnerability triage, patch prioritization and SOAR vulnerability workflows.
api: openapi/feedly-entities-openapi.yml
operations: [cve-insights-card, get-multiple-cves, getCveTimeline, getVulnerabilityAgent, trending-cves]
generated: '2026-08-12'
method: generated
source: openapi/feedly-entities-openapi.yml, openapi/feedly-ti-endpoints-openapi.yml, openapi/feedly-vulnerability-agent-openapi.yml, openapi/feedly-memes-openapi.yml, https://developers.feedly.com/reference/cve-json
---

# Triage a CVE for exploitation risk

## Authentication

```
Authorization: Bearer <FEEDLY_API_TOKEN>
```

## Step 1 — pull the CVE Insights Card

`cve-insights-card` — `GET /v3/entities/{CVEID}`

Returns the enriched CVE record: CVSS score and vector, EPSS, exploitation status, affected products,
associated threat actors and malware, and the articles behind each claim. The JSON shape is
documented at <https://developers.feedly.com/reference/cve-json>.

For a batch, use `get-multiple-cves` — `POST /v3/entities/.mget` rather than looping. One request
against a 100,000/month quota is materially cheaper than fifty.

## Step 2 — read the timeline, not just the score

`getCveTimeline` — `GET /v3/entities/{entityId}/timeline`

Returns a chronological list of significant events for the CVE: **CVSS score changes, exploitation
reports, vendor advisories, threat-intelligence reports and relationship discoveries**.

This is the operation that answers "did this get worse, and when". A CVE that was CVSS 7.5 and
unexploited last week and is now weaponized is a different decision from one that has been 9.8 and
quiet for a year. A point-in-time score cannot tell you which you are looking at.

## Step 3 — query the Vulnerability Agent for a filtered set

`getVulnerabilityAgent` — `POST /v3/trends/vulnerability-dashboard`

The request body is a layered filter document. **Filters within a layer are OR'd; layers are AND'd.**

- `layers[].filters[].field` — one of `period`, `trending`, `created`, `exploited`, `poc`,
  `weaponized`, `inCisaKev`, `cvssScore`, `cvssEstimate`, `cvssVector`
- `layers[].filters[].value` —
  - `period` → `{"type": "Last7Days"|"Last30Days"|"Last3Months"|"Last6Months"|"Custom", "label": "...", "start": "<ISO datetime>", "end": "<ISO datetime>"}`
  - `cvssScore` → `{"gte": 9}`
  - `cvssEstimate` → `"HIGH"|"MEDIUM"|"LOW"`
  - `cvssVector` → a vector component, e.g. `"AV:N"`, `"PR:N"`, `"UI:N"`
  - boolean fields (`exploited`, `poc`, `weaponized`, `inCisaKev`, `trending`) → `true`
- `count` — max results per page
- `continuation` — page token from the previous response
- `sort` — `{"field": "cveId"|"cvssScore"|"epssScore"|"publishedDate", "order": "asc"|"desc"}`

Feedly's own guidance: open the Vulnerability Agent in the UI and click the **API** button to have it
generate the exact JSON body. Do not hand-construct the layers if you can copy them.

### Polling on a cadence

Use `"type": "Custom"` with full ISO 8601 `start`/`end` datetimes to poll every N hours without
overlapping bucket boundaries. The fixed windows (`Last7Days` etc.) re-return the same records on
every poll; custom windows are what make a SOAR/SIEM integration return only new rows.

### Breaking change to know about

`attackVector` was **removed** from this endpoint and replaced by `cvssVector`. The old values were
`NETWORK`, `LOCAL`, `ADJACENT_NETWORK`, `PHYSICAL`; the replacement uses standard CVSS vector
notation (`AV:N`, `AV:L`, `AV:A`, `AV:P`). Integrations written against `attackVector` will filter on
a field that no longer exists. See `changelog/feedly-changelog.yml`.

## Step 4 — situate against the landscape

`trending-cves` — `GET /v3/memes/vulnerabilities/en` returns trending vulnerabilities from the Threat
Landscape dashboard. Use it to distinguish a CVE that is genuinely spiking in reporting from one your
scanner merely happened to surface today.

## Triage heuristic

Escalate when the Insights Card or Agent shows **`inCisaKev: true`**, or **`weaponized: true`**, or
`exploited: true` with a recent exploitation event on the timeline — and the affected product is in
your estate. CVSS alone is a severity ceiling, not a probability; `epssScore` and the exploitation
booleans are the likelihood signal.

## Pagination, limits, errors

Page with `continuation` until it is absent. 100,000 requests/month per token, with
`X-RateLimit-Count`/`X-RateLimit-Limit`/`X-RateLimit-Reset` on every response and `429` on
exhaustion. Errors return `{"errorMessage": "...", "errorId": "..."}`.
