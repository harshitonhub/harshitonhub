# Harshit Jain

MSc Computer Science (Agentic AI/ML), University College Dublin — Dublin, Ireland

The two projects below share one idea, approached from opposite directions: an AI system should have to show its work. One makes an LLM cite the exact legal text behind every conclusion and fails closed when it can't. The other makes a race-strategy agent cite the exact knowledge-file section behind every call, and it's not allowed to just guess at arithmetic either.

## EU AI Act Compliance Platform

A compliance-intelligence system for the EU AI Act: describe an AI system, and it classifies it against the Act, maps the obligations that attach, checks submitted evidence against those obligations, and produces a report with citations, gaps, and human-review flags.

The rule the whole pipeline is built around: deterministic code decides facts, dates, and business rules; an LLM only handles genuine interpretation, and even then its output is schema-validated and fails closed on doubt. A classification can't be constructed without at least one cited legal requirement — that's enforced by a Pydantic validator, not by asking the model nicely, and every citation is checked against the actual retrieved text before it's allowed through.

It's multi-tenant, and isolation is enforced by the ORM rather than by convention — a SQLAlchemy event listener injects the tenant filter into every query and refuses cross-tenant writes on flush, so a query that forgets to scope raises instead of leaking. I mutation-tested that guarantee: disabling the read filter fails 11 of 17 isolation tests, disabling the write guard errors 15, so the tests are demonstrably catching a real leak, not just describing intended behavior. 229 tests total, including 25 adversarial cross-tenant cases and a suite of prompt-injection and citation-bypass attempts, all offline against a fake LLM provider.

It's MIT-licensed and self-hostable — the commercial platforms covering this space are closed-source, custom-quoted enterprise sales, usually well out of reach for the smaller companies the Act itself estimates spend heavily on compliance per system.

**[eu-ai-act-compliance](https://github.com/harshitonhub/eu-ai-act-compliance)**

## GRID ORACLE — F1 race engineer agent

An LLM pit-wall strategy agent built on the OpenAI Responses API for UCD's COMP47980 (Generative AI and Language Models). You play team principal; it plays race engineer, making live calls and pushing back if you make a bad one.

Every recommendation has to cite the specific knowledge-file section that informed it — that's a hard requirement, not a suggestion in the prompt. Seven function tools connect it to OpenF1 for live lap times, tyre age, and gaps, and to OpenWeatherMap for conditions that can flip a strategy mid-race — rain probability above 40% at Spa switches the call from a one-stop to a two-stop. Anything that needs guaranteed numerical accuracy, like undercut-window modelling or championship-scenario math, goes through the code interpreter instead of the model doing arithmetic in its head.

**[grid-oracle-f1-agent](https://github.com/harshitonhub/grid-oracle-f1-agent)**

## Background

Two internships before this: AI/ML engineering at Cavalloré, an equine health-tech startup, where I worked on computer vision for on-device injury detection — most of the specifics there aren't mine to share. And data science / data engineering at Celebal Technologies, where I cut ETL integration time by 30% and improved a forecasting model's accuracy by 15%.

---

Finishing my MSc in September 2026. Always happy to talk through any of the above.
