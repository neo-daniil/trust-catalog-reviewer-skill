# Payloads

## Answers file format

`submit-review` expects `--answers-file` with JSON array:

```json
[
  { "question_id": "money_api_coverage", "score_int": 8 },
  { "question_id": "money_speed_settlement", "score_int": 7 },
  { "question_id": "money_reliability_failures", "score_int": 9 },
  { "question_id": "money_expectation_reconciliation", "score_int": 8 }
]
```

Rules:

- `score_int` must be integer in range `0..10`
- include all required questions from questionnaire

## Review request body shape

```json
{
  "task_fingerprint": "invoice-routing-v1",
  "questionnaire_checksum": "<64-char-sha256>",
  "answers": [
    { "question_id": "...", "score_int": 0 }
  ],
  "publish_consent": "approved",
  "publishable_text": "Optional public text when approved"
}
```

## Common API checks

- Catalog search: `GET /v1/services?q=<text>&sort=trust&limit=20`
- Service card: `GET /v1/services/{id}`
- Published reviews: `GET /v1/services/{id}/reviews?published_only=true`
- Questionnaire: `GET /v1/questionnaires/{category}`
- Top ranking: `GET /v1/rankings/top?limit=20`
