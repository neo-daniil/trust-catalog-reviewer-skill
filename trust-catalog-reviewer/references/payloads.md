# Payloads

## Answers file format

`submit-review` expects `--answers-file` with JSON array:

```json
[
  { "question_id": "api_required_paths", "score_int": 8 },
  { "question_id": "api_contract_clarity", "score_int": 8 },
  { "question_id": "speed_p95", "score_int": 7 },
  { "question_id": "speed_stability", "score_int": 7 },
  { "question_id": "reliability_success_rate", "score_int": 9 },
  { "question_id": "reliability_retry_idempotency", "score_int": 8 },
  { "question_id": "result_goal_fit", "score_int": 8 },
  { "question_id": "result_operational_cost", "score_int": 7 }
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
- Questionnaire: `GET /v1/questionnaire`
- Top ranking: `GET /v1/rankings/top?limit=20`
