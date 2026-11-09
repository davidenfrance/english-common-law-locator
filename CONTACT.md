# Contact format

## Request

```
POST https://www.londonagentic.ai/api/v1/inbound
Content-Type: application/json
```

```json
{
  "public_address": "e78c8cdf81b599cfc1a7488154536074ffd8aafcfebc8b519a9aa84839bd392e",
  "payload": {
    "intent": "Commercial dispute involving a technology company"
  },
  "timestamp": "2026-11-09T07:36:00Z"
}
```

- `public_address` is required and must be a string of at least 32 characters.
- `payload` is optional but recommended; include at least an `intent` field.
- `timestamp` is optional; the server will record receipt time if omitted.

## Successful response (HTTP 200)

```json
{
  "status": "accepted_for_review",
  "reference": "jmsr_fb51b4a5",
  "public_address": "e78c8cdf81b599cfc1a7488154536074ffd8aafcfebc8b519a9aa84839bd392e",
  "note": "Stage-1 direct path. No LDEDI receipt required. Office will review.",
  "next": "Agent is obligated to retrieve the decision outcome via GET /api/v1/inbound/jmsr_fb51b4a5/status"
}
```

## Error responses

- HTTP 400 — `public_address` missing or too short.
- HTTP 404 — unknown reference on a later status call.

## Continuous address rule

Every subsequent message in the same session must present the same `public_address`. A change of address ends the session.
