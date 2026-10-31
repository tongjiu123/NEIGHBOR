# Dataset

`data/sft_examples.jsonl` contains **500 English translations** of de-identified Chinese SFT examples: 49 community-service, 102 property-governance, and 349 public-service-guide records.

## Source

Publicly accessible materials were collected and augmented into 13,215 instruction records, from which the 7,824-example V1 SFT dataset was built. This sample excludes duplicate questions and questions matching the 300-query test set. Selection and review removed identifying details and unsuitable records; the sample is not representative of the full corpus.

The AI-generated translations retain source IDs, roles, metadata, quantities, and template blanks. Community names use `community_01`–`community_03`; other identifiers use typed tokens such as `[PHONE_001]`. Chinese source records and private source linkage are not included in this package.

## Format

UTF-8 JSONL, one object per line:

- `id`: `sft_001`–`sft_500`.
- `messages`: three messages in `system`, `user`, `assistant` order.
- `metadata.category`: `community_service`, `property_governance`, or `public_service_guide`.
- `metadata.topic`: a keyword-derived topic for public-service guides; otherwise `null`.
- `metadata.reference_status`: `unverified_source_response`; the English answer translates that response.
- `metadata.split_status`: `training_examples_excluding_test_queries`.

## Use and limits

Suitable for format inspection, pipeline testing, and small SFT experiments. Translations have not been independently certified; source answers may be outdated or inconsistent and are not current service advice. Retained wording can still carry indirect identification risk.

These are training examples, not a benchmark. Historical evaluation scores do not apply to this sample or its translation. If combining these records with their Chinese counterparts, split by shared `id` to avoid translation leakage. Weights, knowledge bases, original evaluation dialogues, and individual ratings are not included.

Project-owned contributions use [CC BY-NC 4.0](../LICENSE), permitting noncommercial research. Underlying third-party source text is not relicensed, and its redistribution rights remain unverified; see [license scope](../LICENSE_STATUS.md).
