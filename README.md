# Feedly

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

Feedly is a content aggregation and threat intelligence platform that reads millions of open sources and turns them into structured, machine-readable intelligence. Its consumer product is a feed reader built on RSS/Atom; its commercial product, Feedly Threat Intelligence, applies a family of AI models ("Leo") to build a Real-Time Threat Graph covering threat actors, malware families, CVEs, indicators of compromise, MITRE ATT&CK techniques, and cyberattacks. The Feedly API is a REST API over api.feedly.com/v3 that exposes those objects to security teams for SOAR/SIEM automation — collecting articles from AI Feeds, Folders and Boards, searching and asking questions of the corpus with LLMs, pulling CVE/malware/threat-actor insight cards and their relationships, exporting IoCs with context, and registering webhooks for saved-article and annotation events. Feedly also operates a hosted, OAuth-protected Model Context Protocol server over its Threat Graph, and publishes an open-source library of CTI Agent Skills and prompts for Claude.

**Areas:** Threat Intelligence · Cybersecurity · Content Aggregation · RSS · News · Vulnerability Management · Indicators of Compromise · Malware · Threat Actors · mitre-attack · Security Automation · Artificial Intelligence

## Feedly on APIs.io

Everything profiled for Feedly is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/feedly/](https://apis.io/providers/feedly/)** — or go straight to one of the APIs or properties below.

### APIs (30)

- [Feedly Threat Graph MCP Server](https://apis.io/apis/feedly/feedly-threat-graph-mcp-server/) — Hosted, remote Model Context Protocol server exposing the Feedly Real-Time Threat Graph to AI agents. Feedly documents 16 tools covering threat actors,…
- [Feedly Alerts API](https://apis.io/apis/feedly/feedly-alerts-api-api/) — The Alerts API API from Feedly — 1 operation(s) for alerts api.
- [Feedly Annotations API](https://apis.io/apis/feedly/feedly-annotations-api-api/) — The Annotations API API from Feedly — 1 operation(s) for annotations api.
- [Feedly Contents API](https://apis.io/apis/feedly/feedly-contents-api/) — The Contents API from Feedly — 2 operation(s) for contents.
- [Feedly Custom Agents API](https://apis.io/apis/feedly/feedly-custom-agents-api/) — > 🚧 Alpha: Custom Agents is a new capability and still under active development. Endpoints, fields, and behavior may change without notice. Custom Agents…
- [Feedly Detection Rules API](https://apis.io/apis/feedly/feedly-detection-rules-api/) — The Detection Rules API from Feedly — 1 operation(s) for detection rules.
- [Feedly Entities API](https://apis.io/apis/feedly/feedly-entities-api-api/) — The Entities API API from Feedly — 5 operation(s) for entities api.
- [Feedly Entities API](https://apis.io/apis/feedly/feedly-entities-api/) — The Entities API from Feedly — 2 operation(s) for entities.
- [Feedly Entity Lists API](https://apis.io/apis/feedly/feedly-entity-lists-api/) — Manage and retrieve enterprise entity lists
- [Feedly Entries API](https://apis.io/apis/feedly/feedly-entries-api/) — The Entries API from Feedly — 1 operation(s) for entries.
- [Feedly Folders API](https://apis.io/apis/feedly/feedly-folders-api/) — The Folders API from Feedly — 1 operation(s) for folders.
- [Feedly Insight Cards API](https://apis.io/apis/feedly/feedly-insight-cards-api/) — The Insight Cards API from Feedly — 1 operation(s) for insight cards.
- [Feedly Ioc? API](https://apis.io/apis/feedly/feedly-ioc-api/) — The Ioc? API from Feedly — 1 operation(s) for ioc?.
- [Feedly Memes API](https://apis.io/apis/feedly/feedly-memes-api/) — The Memes API from Feedly — 2 operation(s) for memes.
- [Feedly .mget API](https://apis.io/apis/feedly/feedly-mget-api/) — The .mget API from Feedly — 1 operation(s) for .mget.
- [Feedly Ner Gazetteer API](https://apis.io/apis/feedly/feedly-ner-gazetteer-api/) — The Ner Gazetteer API from Feedly — 1 operation(s) for ner gazetteer.
- [Feedly New Malwares API](https://apis.io/apis/feedly/feedly-new-malwares-api/) — The New Malwares API from Feedly — 1 operation(s) for new malwares.
- [Feedly Prediction API](https://apis.io/apis/feedly/feedly-prediction-api/) — The Prediction API from Feedly — 1 operation(s) for prediction.
- [Feedly Rag API](https://apis.io/apis/feedly/feedly-rag-api/) — The Rag API from Feedly — 1 operation(s) for rag.
- [Feedly Relationships API](https://apis.io/apis/feedly/feedly-relationships-api/) — The Relationships API from Feedly — 5 operation(s) for relationships.
- [Feedly Tags API](https://apis.io/apis/feedly/feedly-tags-api-api/) — The Tags API API from Feedly — 2 operation(s) for tags api.
- [Feedly Tags API](https://apis.io/apis/feedly/feedly-tags-api/) — The Tags API from Feedly — 1 operation(s) for tags.
- [Feedly Threat Actors API](https://apis.io/apis/feedly/feedly-threat-actors-api/) — The Threat Actors API from Feedly — 1 operation(s) for threat actors.
- [Feedly Threats API](https://apis.io/apis/feedly/feedly-threats-api/) — The Threats API from Feedly — 1 operation(s) for threats.
- [Feedly Trend Discovery API](https://apis.io/apis/feedly/feedly-trend-discovery-api/) — The Trend Discovery API from Feedly — 1 operation(s) for trend discovery.
- [Feedly Triggers API](https://apis.io/apis/feedly/feedly-triggers-api/) — The Triggers API from Feedly — 2 operation(s) for triggers.
- [Feedly Ttp Dashboard API](https://apis.io/apis/feedly/feedly-ttp-dashboard-api/) — The Ttp Dashboard API from Feedly — 2 operation(s) for ttp dashboard.
- [Feedly Users API](https://apis.io/apis/feedly/feedly-users-api/) — The Users API from Feedly — 1 operation(s) for users.
- [Feedly Vulnerabilities API](https://apis.io/apis/feedly/feedly-vulnerabilities-api/) — The Vulnerabilities API from Feedly — 1 operation(s) for vulnerabilities.
- [Feedly CV Es API](https://apis.io/apis/feedly/feedly-cves-api/) — The CVEs API from Feedly — 2 operation(s) for cves.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Feedly Webhooks](https://apis.io/asyncapis/feedly/feedly-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [feedly-threat-graph](https://apis.io/servers/feedly/feedly-threat-graph/)

#### Collections (18)

Postman and Open Collection request collections.

- [Feedly API](https://apis.io/collections/feedly/open-feedly-agents/)
- [Alerts API](https://apis.io/collections/feedly/open-feedly-alerts/)
- [Annotations API](https://apis.io/collections/feedly/open-feedly-annotations/)
- [Enterprise API](https://apis.io/collections/feedly/open-feedly-enterprise/)
- [Enterprise Collections](https://apis.io/collections/feedly/open-feedly-enterprise-collections/)
- [Enterprise Users API](https://apis.io/collections/feedly/open-feedly-enterprise-users/)
- [Entities API](https://apis.io/collections/feedly/open-feedly-entities/)
- [Entries](https://apis.io/collections/feedly/open-feedly-entries/)
- [Get Intel Profiles](https://apis.io/collections/feedly/open-feedly-intel-profiles/)
- [IoCs](https://apis.io/collections/feedly/open-feedly-iocs/)
- [Memes API](https://apis.io/collections/feedly/open-feedly-memes/)
- [ML Endpoint](https://apis.io/collections/feedly/open-feedly-ml/)
- [Search API](https://apis.io/collections/feedly/open-feedly-search/)
- [Streams API](https://apis.io/collections/feedly/open-feedly-streams/)
- [Tags API](https://apis.io/collections/feedly/open-feedly-tags/)
- [TI Endpoints](https://apis.io/collections/feedly/open-feedly-ti-endpoints/)
- [Trends API](https://apis.io/collections/feedly/open-feedly-trends/)
- [Feedly Vulnerability Agent API](https://apis.io/collections/feedly/open-feedly-vulnerability-agent/)

#### Overlays (18)

OpenAPI overlays, including conversational phrasing for each operation.

- [Feedly Agents Overlay](https://apis.io/overlays/feedly/feedly-agents-overlay/)
- [Feedly Alerts Overlay](https://apis.io/overlays/feedly/feedly-alerts-overlay/)
- [Feedly Annotations Overlay](https://apis.io/overlays/feedly/feedly-annotations-overlay/)
- [Feedly Enterprise Collections Overlay](https://apis.io/overlays/feedly/feedly-enterprise-collections-overlay/)
- [Feedly Enterprise Overlay](https://apis.io/overlays/feedly/feedly-enterprise-overlay/)
- [Feedly Enterprise Users Overlay](https://apis.io/overlays/feedly/feedly-enterprise-users-overlay/)
- [Feedly Entities Overlay](https://apis.io/overlays/feedly/feedly-entities-overlay/)
- [Feedly Entries Overlay](https://apis.io/overlays/feedly/feedly-entries-overlay/)
- [Feedly Intel Profiles Overlay](https://apis.io/overlays/feedly/feedly-intel-profiles-overlay/)
- [Feedly Iocs Overlay](https://apis.io/overlays/feedly/feedly-iocs-overlay/)
- [Feedly Memes Overlay](https://apis.io/overlays/feedly/feedly-memes-overlay/)
- [Feedly Ml Overlay](https://apis.io/overlays/feedly/feedly-ml-overlay/)
- [Feedly Search Overlay](https://apis.io/overlays/feedly/feedly-search-overlay/)
- [Feedly Streams Overlay](https://apis.io/overlays/feedly/feedly-streams-overlay/)
- [Feedly Tags Overlay](https://apis.io/overlays/feedly/feedly-tags-overlay/)
- [Feedly Ti Endpoints Overlay](https://apis.io/overlays/feedly/feedly-ti-endpoints-overlay/)
- [Feedly Trends Overlay](https://apis.io/overlays/feedly/feedly-trends-overlay/)
- [Feedly Vulnerability Agent Overlay](https://apis.io/overlays/feedly/feedly-vulnerability-agent-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Feedly Authentication](https://apis.io/security/feedly/feedly-authentication/)
- [Feedly Domain Security](https://apis.io/security/feedly/feedly-domain-security/)
- [Feedly Trust Center](https://apis.io/security/feedly/feedly-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Feedly Plans Pricing](https://apis.io/plans/feedly/feedly-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Feedly Rate Limits](https://apis.io/rate-limits/feedly/feedly-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://feedly.com/)
- [Documentation](https://docs.feedly.com/)
- [Getting started](https://developers.feedly.com/reference/building-your-first-ti-integration)
- [API reference](https://developers.feedly.com/reference/introduction)
- [Pricing](https://feedly.com/threat-intelligence/pricing)
- [Sign up](https://feedly.com/i/team/api)
- [Support](https://docs.feedly.com/)
- [Changelog](https://developers.feedly.com/changelog/)
- [Blog](https://feedly.com/new-features)
- [Security](https://feedly.com/legal/security)
- [Compliance](https://trust.feedly.com/)
- [Trust centre](https://trust.feedly.com/)
- [Terms of service](https://feedly.com/legal/terms)
- [Privacy policy](https://feedly.com/legal/privacy)
- [GitHub](https://github.com/feedly)
- [Status](https://status.feedly.com/)

## API Evangelist rating

**Kin Score 59.6** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 60.0 |
| Contract governance | 18.2 |
| Operational transparency | 55.3 |
| Developer ergonomics | 51.2 |
| Access clarity | 68.4 |

**Agent readiness 65.3** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | verified |
| Event Surface Described | yes |
| Agent Skills | yes |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 27.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/feedly/](https://apis.io/providers/feedly/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Feedly: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/feedly/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
