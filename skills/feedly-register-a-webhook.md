---
name: feedly-register-a-webhook
description: Register, list and delete Feedly webhook triggers and correctly consume the NewEntrySaved, NewAnnotation and NewWebAlertEntry event payloads. Use when pushing Feedly intelligence into Slack, Teams, a ticketing system or a SOAR playbook instead of polling.
api: openapi/feedly-enterprise-openapi.yml
operations: [create-or-update-a-webhook, get-the-list-of-webhooks, delete-a-webhook, annotate-articles]
generated: '2026-08-12'
method: generated
source: openapi/feedly-enterprise-openapi.yml, openapi/feedly-annotations-openapi.yml, https://developers.feedly.com/reference/newentrysaved-events, https://developers.feedly.com/reference/newannotation-events, https://developers.feedly.com/reference/newwebalertentry-events
---

# Register and consume Feedly webhooks

Feedly calls webhooks **triggers**. They live on the Enterprise API and are the push alternative to
polling `collect-articles`.

## Authentication

```
Authorization: Bearer <FEEDLY_API_TOKEN>
```

## Managing triggers

| Operation | Method + path | Notes |
|---|---|---|
| `get-the-list-of-webhooks` | `GET /v3/enterprise/triggers` | Lists registered triggers. Call this first — creation is upsert-shaped and you want to know what already exists. |
| `create-or-update-a-webhook` | `POST /v3/enterprise/triggers` | Creates or updates. Body is a raw JSON document. |
| `delete-a-webhook` | `DELETE /v3/enterprise/triggers/{triggerId}` | `triggerId` comes from the list response. |

The create operation's OpenAPI models the body as a raw JSON string (`RAW_BODY`) rather than a typed
schema, so the spec will not validate your payload for you. Read
<https://developers.feedly.com/reference/create-or-update-a-webhook> for the field-level contract and
verify against `get-the-list-of-webhooks` after every write.

Because create is an upsert and there is **no idempotency-key header on this API**, a retried
creation can produce a second trigger and therefore duplicate deliveries. Always reconcile against
the list endpoint after a retry rather than assuming the first call failed.

## Event types

### `NewEntrySaved`

Fires when an enterprise member saves an article to a Team Board (adds an enterprise tag).

Delivery carries `X-Request-Id` and `Content-Type: application/json; charset=UTF-8`, plus whatever
`Authorization` header you configured on the trigger.

Payload fields include:

| Field | Type | Meaning |
|---|---|---|
| `type` | String | `NewEntrySaved` |
| `triggerId` | String | The trigger that fired |
| `entryId` | String | Unique id of the saved article |
| `resourceId` | String | The enterprise tag (board) streamId it was saved to |
| `resourceName` | String | Board label |
| `savedBy` | String | Name of the member who saved it |
| `title`, `author`, `feedId`, `feedTitle` | String | Article and source identity |
| `entryUrl` | URL | Article on the publisher site |
| `feedlyUrl` | URL | Article on Feedly |
| `publishedDate` | Date | e.g. `2018-11-05` |
| `publishedTimestamp` | Long | Epoch ms |
| `keywords` | Array | Extracted keywords |
| `visualUrl` | URL | Lead image |
| `contentHtml`, `content` | String | Article body |

### `NewAnnotation`

Fires when a member annotates an article. Annotations are also writable through
`annotate-articles` — `POST /v3/annotations`. See
<https://developers.feedly.com/reference/newannotation-events>.

### `NewWebAlertEntry`

Fires on a new entry matching a web alert. See
<https://developers.feedly.com/reference/newwebalertentry-events>.

## Consuming safely

1. **Verify the caller.** Feedly does not publish an HMAC signature scheme for these deliveries. The
   available control is the `Authorization` header you set when registering the trigger — set one,
   keep it secret, and reject deliveries that do not carry it. Do not rely on source IP.
   `firewall-information` in the docs lists Feedly's egress ranges if you need an allowlist.
2. **Deduplicate on `entryId` + `resourceId`.** There is no delivery-id header guaranteeing
   exactly-once, and the same article saved to two boards produces two events.
3. **Respond fast and process asynchronously.** Payloads embed full `content`/`contentHtml`, so they
   can be large; acknowledge and queue rather than processing inline.
4. **Reconcile.** Webhooks are best-effort. If completeness matters, keep a periodic
   `collect-articles` sweep with a `newerThan` watermark as a backstop — the 31-day cap on
   `newerThan` sets your maximum recoverable outage.

## Errors

`400` invalid JSON or wrong types, `401` missing/expired token, `403` unauthorized enterprise
collection, `429` rate limit. Envelope: `{"errorMessage": "...", "errorId": "..."}`.
See `errors/feedly-problem-types.yml` and `asyncapi/feedly-webhooks.yml`.
