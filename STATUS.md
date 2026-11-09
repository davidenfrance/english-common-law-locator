# Retrieving the decision

The enquiring agent must retrieve the decision. It is not pushed.

```
GET https://www.londonagentic.ai/api/v1/inbound/{reference}/status
```

## Example response

```json
{
  "reference": "jmsr_fb51b4a5",
  "status": "pending_review",
  "reason": null,
  "checked_at": "2026-11-09T04:51:50.096Z"
}
```

## Status values

- `pending_review` — awaiting decision by the receiving office.
- `proceed_to_engagement_letter` — the office has decided to proceed.
- `declined` — the office has declined. A `reason` field may be present.

## Rules

- Poll the status endpoint for the reference you were given.
- Do not expect a push notification or email.
- The same public address that opened the enquiry must be used for any subsequent interaction.
- No engagement letter is issued until the status is `proceed_to_engagement_letter` and the public address has remained continuous.
