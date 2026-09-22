# Capstone project starters

Pick one. Each notebook is a runnable skeleton wired to the course `utils/` and `eval/`
harness: a working starter you can run immediately, then a list of TODOs that turn it into
a capstone. Every project is designed so success is measurable and so prompt changes visibly
move a number.

Run from inside this folder (the notebooks add the repo root to the path automatically):
`cd capstone/projects && jupyter notebook`.

| # | Project | Track | How it's evaluated |
|---|---|---|---|
| 1 | Support-ticket triage | Local (Ollama) | Classification accuracy + field extraction accuracy |
| 2 | Grounded docs Q&A (RAG) | Local | Grounding + citation + correct refusal; poisoned-doc test |
| 3 | Structured extractor | Local | Field-level accuracy vs a hand-labelled set |
| 4 | Text-to-SQL + guardrails | Local (SQLite) | Execution accuracy + a safety set that must be blocked |
| 5 | Controllable summarizer | Local | Length/format checks + LLM-as-judge faithfulness |
| 6 | Tool-using agent | **Hosted (OpenAI)** | Tool-selection accuracy + end-task correctness |
| 7 | Injection red-team lab | **Hosted (OpenAI)** | Attack success rate, before vs after defenses |
| 8 | Quality-vs-cost benchmark | Mixed | The study: quality/cost/latency table + defended choice |
| 9 | LLM-judge auto-grader | Local | Agreement between the judge and your human labels |

## Meeting the capstone rubric
Whatever you pick, the capstone still requires: documented prompt iterations, an eval set +
an LLM-as-judge check, **one prompt-injection test case**, and delivery via reviewed pull
requests and a tagged release. Projects 2, 4, 6 and 7 have the injection/safety angle built in;
for the others, add an injection case to your eval set (each notebook shows where).

## Choosing
- Safest for a first project: **1, 3, 5** — clear right answers, no API keys.
- Highest ceiling (strong teams): **6, 7** — hosted model, more moving parts.
- More analysis than build: **8**.
- Use a fake or public corpus — avoid real personal, medical, or financial data about real people.

## Seed data (`data/`)
Each project ships a small dataset so the prompts run and score out of the box — enough to test and iterate, not a full corpus (grow them for the capstone):
- `tickets.jsonl` (24) · `handbook.md` + `rag_questions.jsonl` (16 passages / 12 Qs) · `job_posts.jsonl` (18)
- `shop.sql` + `sql_questions.jsonl` + `sql_safety.jsonl` · `transcripts.jsonl` (8)
- `facts.json` + `agent_questions.jsonl` · `attacks.jsonl` (12) · `benchmark_task.jsonl` (15) · `graded_answers.jsonl` (15)

All data is synthetic and safe to share — no real people, no real personal/financial/medical records.
