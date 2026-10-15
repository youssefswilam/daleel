# Senior AI Engineer Study Plan

Oct 15, 2026 · @Youssef

24 weeks, 120 study days, 2–3 hours a day, 5 days a week. You finish with one deployed, evaluated AI product, six public write-ups, and interview practice.

## How to use this plan

Open the doc, find today's day number, do it, tick the box. Days are numbered 1 to 120 so falling behind never breaks the plan: you just continue from the next unticked day.

- **Daily rhythm.** Study first (about 1.5 hours), then practice (about 1 hour). In most weeks, Days 1–3 are learning and Days 4–5 are building.
- **Your week.** Plan days are Sunday to Thursday. Saturday is catch-up: if a day runs long, finish it on Saturday rather than skipping it. From 18 December 2026, Friday is for the IBM course. Never skip a build day.
- **The capstone: "Daleel".** One personal project you grow through all 24 weeks: a bilingual Arabic/English assistant that answers questions over public documents you choose (for example Saudi tourism rules or Egyptian labor law). It starts as a clean Python project and ends as a deployed, evaluated, monitored AI product. It is separate from your THV work, so it can be fully public.
- **Write as you go.** Keep a `LEARNING.md` file in the repo with 3–5 lines per day. Six public write-ups (Days 20, 60, 75, 90, 105, 114) turn these notes into portfolio pieces.
- **One book backbone.** Buy Chip Huyen's *AI Engineering* (O'Reilly). It appears throughout the plan by chapter.
- **Setup.** You're on Windows, so install WSL2 (Ubuntu) on Day 1 and do all coding inside it. Use VS Code with the WSL extension, Python 3.12+, Docker Desktop, and a GitHub account.
- **Budget.** Most material is free. Expect roughly $30–60 for the book plus a small LLM API budget (set a monthly spending limit; use the cheapest models while developing). Use free Google Colab GPUs for Weeks 7, 8 and 20.
- **Use Claude as a tutor, not a crutch.** Ask it to explain or quiz you, but type the code yourself, especially in Phases 1 and 2.

## At a glance

Seven phases, each ending with something that works and a short write-up.

| Phase | Weeks | Days | Focus | Daleel finishes the phase with |
| --- | --- | --- | --- | --- |
| 1. Engineering foundations | 1–4 | 1–20 | Git, typed Python, testing, FastAPI, Docker, CI | A tested, containerized API, deployed |
| 2. How LLMs work | 5–8 | 21–40 | Neural nets, transformers, tokenization, Hugging Face | A small fine-tuned intent classifier |
| 3. LLM app engineering | 9–12 | 41–60 | Prompting, structured outputs, embeddings, hybrid RAG | Bilingual RAG with citations and a UI |
| 4. Evaluation and observability | 13–15 | 61–75 | Golden sets, LLM-as-judge, tracing, error analysis | Evals running in CI, every request traced |
| 5. Agents and tool use | 16–18 | 76–90 | Agent loops, LangGraph, MCP, human approval | A tool-using agent and an MCP server |
| 6. Production | 19–21 | 91–105 | Cost, latency, caching, LoRA, serving, security | Cheaper, faster, guarded, load-tested |
| 7. Design and portfolio | 22–24 | 106–120 | System design, case study, interview prep | Public demo, case study, updated CV |

## Certificates

One course and one exam: study IBM's RAG and Agentic AI course on Fridays from 18 December 2026, and take the IBM exam on Saturday 20 February 2027.

- **The course** ([IBM RAG and Agentic AI Professional Certificate](https://www.coursera.org/professional-certificates/ibm-rag-and-agentic-ai), Coursera) is how you prepare. One enrollment, 10 short courses inside it, done in order.
- **The exam** ([IBM Certified watsonx Generative AI Engineer – Associate](https://credly.com/org/ibm-professional-certification-program/badge/ibm-certified-watsonx-generative-ai-engineer-associ), C1000-185) is the official IBM certification that goes on your CV.
- You don't need to finish all 10 courses before the exam. Skim lessons that repeat the plan; focus on the watsonx labs and the agentic, multi-agent and MCP courses.

Dates assume Day 1 is Sunday 18 October 2026, plan days are Sunday to Thursday, Friday is the course and Saturday is catch-up.

| Date | What |
| --- | --- |
| Fri 18 Dec 2026 | First course session (Week 9) |
| Every Friday until 12 Feb 2027 | One 4–5 hour course session |
| Sun 31 Jan 2027 | Book the exam (Week 16) |
| Fri 5 and Fri 12 Feb 2027 | Study IBM's official exam guide; review prompt tuning and model customization in watsonx |
| Thu 18 Feb 2027 | Plan Day 90, end of Phase 5 |
| **Sat 20 Feb 2027** | **IBM exam (C1000-185)** |
| Sat 13 Mar 2027 | Retake, only if needed (end of Phase 6) |

After the exam, keep the Friday sessions if you also want the Coursera certificate, until all 10 courses are done. Later, in Months 7–8, add one cloud certification (Google Cloud Professional ML Engineer suits your work stack; Microsoft's is now AI-103, since AI-102 retired on 30 June 2026). Never use "exam dump" sites.

## Phase 1: Engineering foundations (Weeks 1–4)

Goal: write Python that other engineers can run, test, and deploy. This closes the biggest gap for people coming from data analysis.

### Day 0: GitHub setup

- [x] **Day 0 — Personal GitHub repo (done).** Repo `youssefswilam/daleel` created and first commits pushed. Personal repos use the SSH alias `github-personal` (key `id_ed25519_personal`); work repos stay on GitHub CLI as `yswilam`, so you never log out of either. Daily routine in the `daleel` folder: `git add .`, `git commit -m "Day N: ..."`, `git push`. For any new personal repo: clone with `git@github-personal:youssefswilam/<repo>.git`, then run `git config user.email` with your personal noreply address inside that repo.
- [ ] **Set your global Git email to your work address,** so work commits are no longer credited to your personal account: `git config --global user.email "<work email>"`.

### Week 1: Shell, Git, project setup

- [ ] **Day 1 — Shell basics.** Study: install [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install), then [Missing Semester](https://missing.csail.mit.edu/) lectures 1–2 (shell, shell tools). Practice: do each lecture's exercises inside WSL. Then set up Git inside WSL, which is separate from Windows: copy your personal SSH key and config into WSL, set your Git name and email, and clone daleel into your WSL home folder using the github-personal address (ask Claude for the exact commands).
- [ ] **Day 2 — Git properly.** Study: Missing Semester "Version Control (Git)" and [Pro Git](https://git-scm.com/book/en/v2) chapters 2–3. Practice: your repo already exists, so practice the workflow in `daleel`: make a branch, commit, push it, then open and merge a pull request on GitHub.
- [ ] **Day 3 — Modern Python tooling.** Study: [uv](https://docs.astral.sh/uv/) and [Ruff](https://docs.astral.sh/ruff/) docs (getting started). Practice: set up `daleel` with a `src/` layout, `pyproject.toml`, uv, and Ruff.
- [ ] **Day 4 — Types and classes.** Study: Real Python [type checking](https://realpython.com/python-type-checking/) and [OOP](https://realpython.com/python3-object-oriented-programming/). Practice: take an old script of yours and refactor it into typed modules; run mypy until it's clean.
- [ ] **Day 5 — Build: ingestion.** Practice: a CLI that reads a folder of PDFs and text files, splits them into chunks, and saves them as JSON. Pick your document set (about 30–100 documents, Arabic and English). Write the README.

### Week 2: Testing, validation, logging

- [ ] **Day 6 — pytest.** Study: Real Python [pytest guide](https://realpython.com/pytest-python-testing/). Practice: write tests for your chunker, including empty files and Arabic text.
- [ ] **Day 7 — Fixtures and mocks.** Study: [pytest fixtures and parametrize](https://docs.pytest.org/en/stable/how-to/fixtures.html) and Python's [unittest.mock](https://docs.python.org/3/library/unittest.mock.html). Practice: build a fake LLM client and test code that calls it.
- [ ] **Day 8 — Pydantic.** Study: [Pydantic docs](https://docs.pydantic.dev/latest/) (models, validation, settings). Practice: `Document` and `Chunk` models; load config from environment variables.
- [ ] **Day 9 — Logging and retries.** Study: Real Python [logging](https://realpython.com/python-logging/) and [Tenacity](https://tenacity.readthedocs.io/). Practice: structured logs plus retry with backoff around a flaky function.
- [ ] **Day 10 — Build: quality gates.** Practice: reach 70%+ test coverage, add [pre-commit](https://pre-commit.com/) hooks (Ruff, mypy). Note in `LEARNING.md` what broke.

### Week 3: Async and FastAPI

- [ ] **Day 11 — Async Python.** Study: Real Python [async IO](https://realpython.com/async-io-python/). Practice: fetch 20 URLs sequentially, then concurrently; compare timings. This is how you'll call LLMs in parallel later.
- [ ] **Day 12 — FastAPI basics.** Study: [FastAPI tutorial](https://fastapi.tiangolo.com/tutorial/) from "First Steps" through "Request Body". Practice: follow along in a scratch project.
- [ ] **Day 13 — FastAPI depth.** Study: FastAPI tutorial sections on Dependencies, Background Tasks, and Testing. Practice: test an endpoint with `TestClient`.
- [ ] **Day 14 — Build: Daleel API.** Practice: `POST /ingest` and `GET /search` (keyword search for now) endpoints.
- [ ] **Day 15 — Build: API tests.** Practice: tests for both endpoints, including bad input. Review the auto-generated OpenAPI docs page.

### Week 4: Docker, CI, deployment

- [ ] **Day 16 — Docker.** Study: [Docker Get Started](https://docs.docker.com/get-started/). Practice: build and run a container for a hello-world app.
- [ ] **Day 17 — Containers for FastAPI.** Study: FastAPI ["FastAPI in Containers"](https://fastapi.tiangolo.com/deployment/docker/) and Docker Compose docs. Practice: Dockerfile for Daleel.
- [ ] **Day 18 — CI.** Study: [GitHub Actions docs](https://docs.github.com/en/actions) (Python quickstart). Practice: a workflow that runs Ruff, mypy and pytest on every push.
- [ ] **Day 19 — Build: compose stack.** Practice: Daleel plus Postgres in Docker Compose; CI green.
- [ ] **Day 20 — Build: deploy and write-up #1.** Practice: deploy to a free tier (Render, Fly.io or Hugging Face Spaces). Publish write-up #1: "Setting up a production-ready Python AI project". **Checkpoint:** can you explain every file in your repo?

## Phase 2: How LLMs work (Weeks 5–8)

Goal: understand what happens inside a model, so you can reason about tokens, sampling, context limits and fine-tuning instead of treating the model as magic. Karpathy's videos are long; pause and type the code yourself.

### Week 5: Neural networks from scratch

- [ ] **Day 21 — Intuition.** Study: [3Blue1Brown neural networks](https://www.3blue1brown.com/topics/neural-networks), chapters 1–4. Practice: write in your own words what a gradient is and why backprop works.
- [ ] **Day 22 — micrograd, part 1.** Study: [Karpathy Zero to Hero](https://karpathy.ai/zero-to-hero.html) lecture 1, first half. Practice: code along.
- [ ] **Day 23 — micrograd, part 2.** Study: lecture 1, second half. Practice: finish micrograd and train the tiny network.
- [ ] **Day 24 — Build: micrograd from memory.** Practice: rebuild it without the video, add one new operation (for example `exp`), and write tests that compare your gradients with PyTorch.
- [ ] **Day 25 — Language modeling.** Study: lecture 2 (makemore: bigram model). Practice: try it on a list of Arabic names.

### Week 6: Training deeper networks

- [ ] **Day 26 — MLP language model.** Study: lecture 3, first half. Practice: code along.
- [ ] **Day 27 — MLP, continued.** Study: lecture 3, second half. Practice: do the exercises in the video description.
- [ ] **Day 28 — Activations and BatchNorm.** Study: lecture 4, first half. Practice: plot activation statistics.
- [ ] **Day 29 — BatchNorm, continued.** Study: lecture 4, second half. Practice: break training on purpose (bad init), then fix it.
- [ ] **Day 30 — Review.** Study: *AI Engineering* chapter 1. Practice: write one page in `LEARNING.md` on how training actually works. Lectures 5–6 are optional extras for later.

### Week 7: Transformers and tokenization

- [ ] **Day 31 — Attention, visually.** Study: Jay Alammar's [Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/). Practice: draw the architecture from memory and label every part.
- [ ] **Day 32 — Build GPT, part 1.** Study: Karpathy lecture 7, "Let's build GPT", first half. Practice: code along in Google Colab.
- [ ] **Day 33 — Build GPT, part 2.** Study: lecture 7, second half. Practice: finish and train it.
- [ ] **Day 34 — Build: Arabic mini-GPT.** Practice: train your GPT on a small public-domain Arabic text. Note how loss and samples change with context length and model size.
- [ ] **Day 35 — Tokenizers.** Study: Karpathy's "Let's build the GPT Tokenizer" (linked from the Zero to Hero page). Practice: count tokens for the same paragraph in Arabic and English with two tokenizers. Arabic often costs more tokens, which matters for your costs.

### Week 8: Hugging Face and fine-tuning basics

- [ ] **Day 36 — Transformer models.** Study: [Hugging Face LLM Course](https://huggingface.co/learn/llm-course) chapter 1. Practice: run its notebooks.
- [ ] **Day 37 — Using Transformers.** Study: LLM Course chapter 2 (pipelines, tokenizers, models). Practice: load a multilingual model and inspect its outputs.
- [ ] **Day 38 — Fine-tuning.** Study: LLM Course chapter 3. Practice: fine-tune a small classifier on the course dataset.
- [ ] **Day 39 — Build: Daleel intent classifier.** Practice: label about 200 example questions (in-scope, out-of-scope, small talk; Arabic and English) and fine-tune a small multilingual model. Report accuracy and the confusion matrix. Your data background shines here.
- [ ] **Day 40 — Foundation models and write-up.** Study: *AI Engineering* chapter 2 (sampling, temperature, structured outputs). Practice: short notes post on what you built in Phase 2 (can be part of write-up #2 later).

## Phase 3: LLM application engineering (Weeks 9–12)

Goal: build retrieval-augmented generation properly, with measured choices instead of defaults, and handle Arabic well.

**IBM course:** starts Friday 18 December 2026, then every Friday (see Certificates).

### Week 9: APIs, prompting, structured outputs

- [ ] **Day 41 — Prompting, part 1.** Study: Anthropic's [prompt engineering tutorial](https://github.com/anthropics/prompt-eng-interactive-tutorial), chapters 1–4. Practice: do every exercise.
- [ ] **Day 42 — Prompting, part 2.** Study: tutorial chapters 5–9. Practice: write prompts for answering a question from a given document, in Arabic and English.
- [ ] **Day 43 — Prompting in depth.** Study: *AI Engineering* chapter 5 and the [Claude docs](https://docs.claude.com) prompt engineering guide. Practice: rewrite your Day 42 prompts and compare outputs side by side.
- [ ] **Day 44 — Structured outputs.** Study: [Instructor docs](https://python.useinstructor.com/) and Anthropic's [courses repo](https://github.com/anthropics/courses) (tool use section). Practice: extract structured fields (title, date, entity) from Arabic documents into Pydantic models, with validation and retries.
- [ ] **Day 45 — Build: LLM client layer.** Practice: one provider-agnostic interface in Daleel with timeouts, retries, streaming, and logging of tokens and cost per call. Tests use your fake client from Day 7.

### Week 10: Embeddings and vector search

- [ ] **Day 46 — Embeddings.** Study: [Sentence Transformers docs](https://sbert.net/) and the [MTEB leaderboard](https://huggingface.co/spaces/mteb/leaderboard) (filter for Arabic and multilingual). Practice: embed 10 sentences and inspect cosine similarities.
- [ ] **Day 47 — Vector databases.** Study: [pgvector README](https://github.com/pgvector/pgvector) (distance types, HNSW and IVFFlat indexes) and skim [Qdrant docs](https://qdrant.tech/documentation/) concepts. Practice: create a vector table and index in your Postgres container.
- [ ] **Day 48 — Compare embedding models.** Practice: write 30 test questions with the correct document for each. Compare 2–3 models (for example [BGE-M3](https://huggingface.co/BAAI/bge-m3) and a multilingual E5 model) on recall@5. Keep this question set: it grows into your eval set.
- [ ] **Day 49 — Build: semantic indexing.** Practice: embed all Daleel chunks with the winning model and store them in pgvector.
- [ ] **Day 50 — Build: semantic search endpoint.** Practice: `GET /search` now returns semantic results with scores. Add tests.

### Week 11: RAG done properly

- [ ] **Day 51 — RAG theory.** Study: *AI Engineering* chapter 6, RAG half. Practice: list three ways your retrieval could fail on your own documents.
- [ ] **Day 52 — Chunking and context.** Study: Anthropic's [Contextual Retrieval](https://www.anthropic.com/news/contextual-retrieval) article. Practice: try two chunk sizes and contextual chunk headers; measure recall@5 on your 30 questions.
- [ ] **Day 53 — Hybrid search and Arabic text.** Study: BM25 ([rank\_bm25](https://github.com/dorianbrown/rank_bm25)), reciprocal rank fusion, and [CAMeL Tools](https://github.com/CAMeL-Lab/camel_tools) for Arabic normalization (alef forms, diacritics, ta marbuta). Practice: normalize Arabic before keyword search.
- [ ] **Day 54 — Build: hybrid retrieval.** Practice: combine BM25 and vector results with reciprocal rank fusion. Measure recall@5 before and after.
- [ ] **Day 55 — Build: reranking and answers.** Practice: add a reranker (for example a BGE reranker), then `POST /ask` that answers with citations to the source chunks.

### Week 12: Patterns, polish, midpoint

- [ ] **Day 56 — Lessons from practitioners.** Study: [What We Learned from a Year of Building with LLMs](https://applied-llms.org/), the tactical part. Practice: list 5 lessons that apply to Daleel.
- [ ] **Day 57 — Common patterns.** Study: Eugene Yan's [Patterns for Building LLM-based Systems](https://eugeneyan.com/writing/llm-patterns/). Practice: map each pattern to what Daleel has or lacks.
- [ ] **Day 58 — Build: graceful answers.** Practice: answer "I don't know" when retrieval scores are weak; route out-of-scope questions using your Day 39 classifier; stream responses.
- [ ] **Day 59 — Build: simple UI.** Practice: a chat UI in [Gradio](https://www.gradio.app/guides/quickstart) or Streamlit with source citations shown, right-to-left Arabic rendering included.
- [ ] **Day 60 — Write-up #2 and midpoint review.** Practice: publish "Bilingual RAG: what actually improved retrieval, with numbers" (chunking, hybrid, reranking results). **Checkpoint:** you should be able to design a RAG system on a whiteboard and justify each component.

## Phase 4: Evaluation and observability (Weeks 13–15)

Goal: prove with numbers whether a change made the system better. This is the clearest sign of seniority, and where your data background is a real advantage.

### Week 13: Evals and error analysis

- [ ] **Day 61 — Why evals.** Study: Hamel Husain, [Your AI Product Needs Evals](https://hamel.dev/blog/posts/evals/). Practice: write down what "a good answer" means for Daleel in 5 concrete criteria.
- [ ] **Day 62 — Error analysis.** Study: Hamel Husain, [A Field Guide to Rapidly Improving AI Products](https://hamel.dev/blog/posts/field-guide/). Practice: run 50 real questions through Daleel, read every answer, and tag failure types in a spreadsheet.
- [ ] **Day 63 — Evaluation methods.** Study: *AI Engineering* chapter 3. Practice: decide which of your failure types need exact checks, code checks, or a judge.
- [ ] **Day 64 — Build: golden set.** Practice: grow your Day 48 questions into 60–100 cases (Arabic and English, easy and hard, some unanswerable), each with the expected source document and a reference answer.
- [ ] **Day 65 — Build: eval runner.** Practice: a script that runs the golden set and reports retrieval recall@k, MRR, and answer pass rate to a CSV and a summary table.

### Week 14: LLM-as-judge and evals in CI

- [ ] **Day 66 — LLM judges.** Study: Hamel Husain, [Using LLM-as-a-Judge](https://hamel.dev/blog/posts/llm-judge/). Practice: write a binary pass/fail faithfulness judge prompt.
- [ ] **Day 67 — Evaluating AI systems.** Study: *AI Engineering* chapter 4. Practice: add a correctness judge alongside faithfulness.
- [ ] **Day 68 — Trust your judge.** Practice: label 40 answers by hand, compare with the judge, and compute true positive and true negative rates. Improve the judge prompt until agreement is high.
- [ ] **Day 69 — Eval libraries.** Study: [Ragas docs](https://docs.ragas.io/) (faithfulness, context precision). Practice: run Ragas on your set and compare with your own judge. Note where they disagree.
- [ ] **Day 70 — Build: evals in CI.** Practice: a GitHub Actions job that runs a fast subset of evals on every pull request and fails if scores drop below a threshold.

### Week 15: Observability and feedback

- [ ] **Day 71 — Tracing.** Study: [Langfuse docs](https://langfuse.com/docs), tracing quickstart. Practice: run Langfuse locally with Docker.
- [ ] **Day 72 — Build: trace everything.** Practice: every request in Daleel records retrieval results, prompt, tokens, latency, and cost.
- [ ] **Day 73 — Evals FAQ.** Study: Hamel Husain, [Evals FAQ](https://hamel.dev/blog/posts/evals-faq/). Practice: write down 3 things you'd change in your eval setup.
- [ ] **Day 74 — Build: feedback loop.** Practice: thumbs up and down in the UI, logged to traces; a weekly view of the top failure categories.
- [ ] **Day 75 — Write-up #3.** Practice: publish "How I evaluate a bilingual RAG system" with your judge agreement numbers and one before-and-after improvement.

## Phase 5: Agents and tool use (Weeks 16–18)

Goal: build agents that take actions reliably, with limits, approvals and evals, and know when a simple workflow is better than an agent.

**IBM exam:** book it on Sunday 31 January 2027, use Fridays 5 and 12 February for the exam guide, and sit the exam on **Saturday 20 February 2027**.

### Week 16: Agents from first principles

- [ ] **Day 76 — Agent patterns.** Study: Anthropic's [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents). Practice: classify Daleel's features as workflow or agent, and justify each.
- [ ] **Day 77 — Tool use.** Study: the tool use section of the [Claude docs](https://docs.claude.com) and the tool use course in Anthropic's [courses repo](https://github.com/anthropics/courses). Practice: one tool call end to end.
- [ ] **Day 78 — Agent concepts.** Study: [Hugging Face Agents Course](https://huggingface.co/learn/agents-course) unit 1. Practice: the unit's exercises.
- [ ] **Day 79 — Build: agent loop without a framework.** Practice: write the loop yourself with three tools: `search_docs`, `calculator`, `get_today`. Log every step.
- [ ] **Day 80 — Build: make it safe.** Practice: validate tool inputs with Pydantic, cap the number of steps, handle tool errors, and add tests for each failure.

### Week 17: Frameworks, approvals, MCP

- [ ] **Day 81 — Frameworks overview.** Study: Agents Course unit 2 (smolagents, LlamaIndex, LangGraph). Practice: note what each framework hides from you that your Day 79 loop showed.
- [ ] **Day 82 — LangGraph.** Study: [LangGraph](https://www.langchain.com/langgraph) docs: state, nodes, edges, and human-in-the-loop interrupts. Practice: a two-node graph with a pause for approval.
- [ ] **Day 83 — Build: approval for actions.** Practice: give Daleel one "write" action (for example save a note or create a support ticket) that must be approved by a human before it runs. Make it idempotent so it never runs twice.
- [ ] **Day 84 — MCP.** Study: [Model Context Protocol docs](https://modelcontextprotocol.io/) introduction and the [Hugging Face MCP Course](https://huggingface.co/learn/mcp-course) unit 1. Practice: run an example MCP server.
- [ ] **Day 85 — Build: Daleel as an MCP server.** Practice: expose `search_docs` as an MCP tool and use it from Claude Desktop.

### Week 18: Evaluating and hardening agents

- [ ] **Day 86 — Agent failure modes.** Study: *AI Engineering* chapter 6, agents half. Practice: list how your agent could loop, misuse a tool, or act on bad input.
- [ ] **Day 87 — Agent evals.** Study: the observability and evaluation bonus unit of the Agents Course. Practice: decide what to measure: task success, steps taken, tool errors, cost.
- [ ] **Day 88 — Build: agent eval set.** Practice: 20 multi-step tasks with expected outcomes; run them and record success rate, steps and cost.
- [ ] **Day 89 — Build: fix the top 3 failures.** Practice: change prompts, tool descriptions or flow; rerun the eval and record the improvement.
- [ ] **Day 90 — Write-up #4.** Practice: publish "Building a tool-using agent with human approval, and how I measured it".

## Phase 6: Production (Weeks 19–21)

Goal: make the system cheaper, faster, safer and more reliable, and know when fine-tuning or self-hosting is worth it.

**IBM exam retake, only if needed:** Saturday 13 March 2027, after Week 20's fine-tuning work.

### Week 19: Cost and latency

- [ ] **Day 91 — Inference optimization.** Study: *AI Engineering* chapter 9. Practice: from your traces, find Daleel's three most expensive and three slowest steps.
- [ ] **Day 92 — Caching.** Study: [prompt caching](https://docs.claude.com/en/docs/build-with-claude/prompt-caching) in the Claude docs, and semantic caching as a concept. Practice: decide which parts of your prompt are stable enough to cache.
- [ ] **Day 93 — Build: caching.** Practice: an exact-match answer cache (Redis in Docker Compose) plus prompt caching. Measure cost and latency before and after.
- [ ] **Day 94 — Build: model routing.** Practice: send easy questions to a small, cheap model and escalate to a stronger one when confidence is low. Compare quality and cost on your eval set.
- [ ] **Day 95 — Build: load test.** Study: [Locust](https://locust.io/) quickstart. Practice: load-test Daleel and record p50 and p95 latency and errors under load.

### Week 20: Fine-tuning and self-hosting

- [ ] **Day 96 — When to fine-tune.** Study: *AI Engineering* chapter 7, and skim chapter 8 (dataset engineering). Practice: write when you would fine-tune versus prompt versus RAG, with one example each.
- [ ] **Day 97 — LoRA.** Study: [PEFT docs](https://huggingface.co/docs/peft) (LoRA) and [Unsloth docs](https://docs.unsloth.ai/). Practice: run an Unsloth example notebook in Colab.
- [ ] **Day 98 — Build: LoRA fine-tune.** Practice: fine-tune a small open model in Colab for one narrow Daleel task, such as rewriting Arabic questions into better search queries.
- [ ] **Day 99 — Serving.** Study: [vLLM docs](https://docs.vllm.ai/) quickstart. Practice: serve a small model with vLLM's OpenAI-compatible server in Colab and call it from Daleel's client layer.
- [ ] **Day 100 — Compare.** Practice: your fine-tuned small model versus an API model on the eval set: quality, cost per 1,000 queries, latency. Write the trade-off in `LEARNING.md`.

### Week 21: Security and reliability

- [ ] **Day 101 — LLM risks.** Study: [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/). Practice: rate each risk for Daleel as high, medium or low.
- [ ] **Day 102 — Prompt injection.** Study: Simon Willison's [prompt injection posts](https://simonwillison.net/tags/prompt-injection/), including "the lethal trifecta". Practice: try to break your own agent with injected instructions inside a document.
- [ ] **Day 103 — Build: guardrails.** Practice: add injection cases to the eval set, input and output checks, PII redaction in logs, and restrict which tools can run on untrusted content.
- [ ] **Day 104 — Build: reliability.** Practice: timeouts everywhere, fallback to a second provider, rate-limit handling, and a clear error message for users when things fail.
- [ ] **Day 105 — Write-up #5.** Practice: publish "Making an LLM app cheaper, faster and safer" with your before-and-after numbers.

## Phase 7: System design and portfolio (Weeks 22–24)

Goal: think and talk like a senior: design whole systems with trade-offs, and show finished, measured work.

### Week 22: AI system design

- [ ] **Day 106 — Architecture.** Study: *AI Engineering* chapter 10 (architecture and user feedback). Practice: draw Daleel's full architecture as it stands now.
- [ ] **Day 107 — Platform view.** Study: Chip Huyen's post "Building A Generative AI Platform" on [her blog](https://huyenchip.com/blog/). Practice: mark which platform components Daleel has and which it lacks.
- [ ] **Day 108 — Design exercise 1.** Practice: a 2-page design doc for "a guest support assistant for a vacation rental platform, 50,000 users a day": components, data flow, evals, cost estimate per month, failure modes.
- [ ] **Day 109 — Design exercise 2.** Practice: a design doc for "document Q&A for a bank with strict data privacy": self-hosted versus API, access control, audit logging.
- [ ] **Day 110 — Defend your designs.** Practice: have Claude play a demanding interviewer on both designs; revise what you couldn't defend.

### Week 23: Finish the capstone

- [ ] **Day 111 — Clean the repo.** Practice: README with an architecture diagram, setup steps, and a results table (retrieval, answer quality, cost, latency).
- [ ] **Day 112 — Demo video.** Practice: a 3-minute video showing an Arabic and an English question, citations, the approval flow, and the eval dashboard.
- [ ] **Day 113 — Final deploy.** Practice: a stable public demo link with spending limits and rate limits set.
- [ ] **Day 114 — Write-up #6: the case study.** Practice: "Daleel: building a bilingual AI assistant end to end": the problem, architecture, key decisions, numbers, and what you'd do next.
- [ ] **Day 115 — CV and profiles.** Practice: update your CV, LinkedIn and GitHub profile with the capstone, the six write-ups, and the measured results from your THV work.

### Week 24: Interview preparation

- [ ] **Day 116 — Question bank.** Study: relevant chapters of Chip Huyen's [ML Interviews Book](https://huyenchip.com/ml-interviews-book/). Practice: list 30 AI engineering questions (RAG, evals, agents, cost, security) and answer 10 in writing.
- [ ] **Day 117 — Answer out loud.** Practice: answer 10 more out loud and record yourself; fix vague answers.
- [ ] **Day 118 — Timed coding.** Practice: build a minimal RAG service from an empty folder in 60 minutes, with tests.
- [ ] **Day 119 — Mock system design.** Practice: a full 45-minute mock design interview with a friend or Claude, on a problem you haven't seen.
- [ ] **Day 120 — Retrospective.** Practice: list your weakest areas and plan the next 3 months; choose your cloud certificate and book its exam for Month 7 or 8; apply to your first 5 roles.

## Sources

All free unless marked paid. If a link has moved, search the resource's name; course pages get reorganized often.

| Resource | Type | Used in |
| --- | --- | --- |
| [AI Engineering, Chip Huyen](https://www.oreilly.com/library/view/ai-engineering/9781098166298/) | Book (paid) | Throughout |
| [Missing Semester (MIT)](https://missing.csail.mit.edu/) | Course | Phase 1 |
| [Pro Git](https://git-scm.com/book/en/v2) | Book | Phase 1 |
| [Real Python](https://realpython.com/) | Tutorials | Phase 1 |
| [FastAPI tutorial](https://fastapi.tiangolo.com/tutorial/) | Docs | Phase 1 |
| [Docker Get Started](https://docs.docker.com/get-started/) | Docs | Phase 1 |
| [Neural Networks: Zero to Hero, Karpathy](https://karpathy.ai/zero-to-hero.html) | Video course | Phase 2 |
| [3Blue1Brown neural networks](https://www.3blue1brown.com/topics/neural-networks) | Videos | Phase 2 |
| [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) | Article | Phase 2 |
| [Hugging Face LLM Course](https://huggingface.co/learn/llm-course) | Course | Phase 2 |
| [Anthropic prompt engineering tutorial](https://github.com/anthropics/prompt-eng-interactive-tutorial) | Course | Phase 3 |
| [Anthropic courses (API, tool use)](https://github.com/anthropics/courses) | Course | Phases 3, 5 |
| [Contextual Retrieval, Anthropic](https://www.anthropic.com/news/contextual-retrieval) | Article | Phase 3 |
| [What We Learned from a Year of Building with LLMs](https://applied-llms.org/) | Article | Phase 3 |
| [Patterns for Building LLM-based Systems, Eugene Yan](https://eugeneyan.com/writing/llm-patterns/) | Article | Phase 3 |
| [pgvector](https://github.com/pgvector/pgvector) | Docs | Phase 3 |
| [CAMeL Tools (Arabic NLP)](https://github.com/CAMeL-Lab/camel_tools) | Library | Phase 3 |
| [Hamel Husain on evals](https://hamel.dev/blog/posts/evals/) | Articles | Phase 4 |
| [Ragas](https://docs.ragas.io/) | Docs | Phase 4 |
| [Langfuse](https://langfuse.com/docs) | Docs | Phase 4 |
| [Building Effective Agents, Anthropic](https://www.anthropic.com/engineering/building-effective-agents) | Article | Phase 5 |
| [Hugging Face Agents Course](https://huggingface.co/learn/agents-course) | Course | Phase 5 |
| [Model Context Protocol](https://modelcontextprotocol.io/) | Docs | Phase 5 |
| [Hugging Face MCP Course](https://huggingface.co/learn/mcp-course) | Course | Phase 5 |
| [Unsloth](https://docs.unsloth.ai/) and [PEFT](https://huggingface.co/docs/peft) | Docs | Phase 6 |
| [vLLM](https://docs.vllm.ai/) | Docs | Phase 6 |
| [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/) | Guide | Phase 6 |
| [ML Interviews Book, Chip Huyen](https://huyenchip.com/ml-interviews-book/) | Book | Phase 7 |

Optional extras if you have spare time: [DeepLearning.AI short courses](https://www.deeplearning.ai/short-courses/) (1–2 hours each, good for single topics) and the [Open-Source AI Cookbook](https://huggingface.co/learn/cookbook).
