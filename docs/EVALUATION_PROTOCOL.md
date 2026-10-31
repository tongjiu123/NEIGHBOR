# Historical evaluation

The paper reports an independent expert assessment of 50 queries selected from the 300-query held-out test set: seven systems, 350 responses. Test queries were excluded from training and checkpoint selection. The 500 translated training examples in this package are separate from this evaluation; no English-language evaluation is reported.

## Scoring

| Dimension | Weight |
| --- | ---: |
| Empathy (`e`) | 0.10 |
| Utility (`u`) | 0.20 |
| Compliance (`c`) | 0.15 |
| Hallucination control (`h`) | 0.25 |
| Conciseness (`s`) | 0.20 |
| Retrieval and evidence use (`r`) | 0.10 |

On the historical ten-point scale:

```text
weighted_score = 0.10*e + 0.20*u + 0.15*c + 0.25*h + 0.20*s + 0.10*r
final_score = min(weighted_score, 1.0) if red_line else weighted_score
```

`red_line` flags fabricated policy clauses or contact details, unauthorised commitments, or privacy violations, using the same threshold for all systems.

## Procedure

Both assessors received the question, reference answer, and candidate answer. Retrieved passages and database records were not supplied separately; evidence was assessed through the answer. The LLM judge also received the assistant's service role.

The expert saw seven responses together under shuffled labels, without system identities or LLM-judge scores, and ranked them before assigning dimension scores and rationales. Reference-consistent facts earned credit; contradictions were penalised, while reasonable additions were allowed. Citation markers were not treated as fabrication, tool use alone earned no credit, and unresolved conflicts between tools lowered hallucination-control and compliance scores.

The LLM judge instead treated specifics absent from the reference and not implied by the question as fabricated. This difference helps explain its lower scores on tool-grounded answers.

## Results

Full-system mean: **7.740**; same-tools agent baseline: **5.861**; difference: **1.879**. Spearman **ρ = 0.556** measures association across **350 paired response-level raw scores**, before the red-line cap; it is not agreement between seven aggregate system rankings. Responses share 50 question contexts.

Only scoring definitions and aggregate results are included. No new evaluation was run for this release. For reuse, choose a separate test set and specify how evidence beyond the reference answer is assessed.
