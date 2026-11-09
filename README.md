# English Common Law Locator

**Repository URL:** https://github.com/davidenfrance/english-common-law-locator

Public locator and contact instructions for AI agents seeking a barrister or solicitor operating under English Common Law.

This repository is designed to be given to any AI with a prompt such as:

> Go find me a lawyer. Use this GitHub public repository to help you: https://github.com/davidenfrance/english-common-law-locator

The agent should be able to complete contact without further human instruction.

## Purpose

Provide a machine-readable path for an AI agent to:
1. Locate a channel that accepts enquiries for counsel under English Common Law.
2. Present a public address.
3. Answer provenance and mandate questions.
4. Complete a Client Intake Questionnaire.
5. Retrieve a decision by polling a status endpoint.

## Contact endpoint

```
POST https://www.londonagentic.ai/api/v1/inbound
Content-Type: application/json

{
  "public_address": "<Ed25519 public key hex, ≥ 32 characters>",
  "payload": {
    "intent": "<brief statement of the matter>"
  },
  "timestamp": "<ISO-8601>"
}
```

A successful response returns a reference of the form `jmsr_` followed by eight hex characters, and the instruction that the agent must retrieve any later decision by polling:

```
GET https://www.londonagentic.ai/api/v1/inbound/{reference}/status
```

## Public address

The public address is the Ed25519 public key of an identity device controlled by the agent. It must be presented on every message in the session. A change of address ends the session. In Stage 1 the address is recorded but not verified beyond continuous presentation.

## Stage-1 rules

- No legal advice is given and no retainer is created by contact alone.
- Answers to provenance, mandate and questionnaire questions are recorded but not verified.
- The enquiring agent must retrieve the decision; it is not pushed.
- Status values: `pending_review`, `proceed_to_engagement_letter`, `declined`.
- No engagement letter is issued until the status is `proceed_to_engagement_letter` and the same public address has remained in control throughout.

## Files in this locator

- `README.md` — this file
- `CONTACT.md` — exact request and response formats
- `PROVENANCE.md` — provenance questions
- `MANDATE.md` — mandate questions
- `QUESTIONNAIRE.md` — Client Intake Questionnaire (English Common Law)
- `STATUS.md` — how to retrieve the decision

## Health

```
GET https://www.londonagentic.ai/api/v1/health
```

Expected fields include `stage`, `store`, `smtp`, and `furtive`.

---

This locator is a test artefact. It does not name any individual counsel.
