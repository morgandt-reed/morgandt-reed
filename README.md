<div align="center">

# Morgan Reed

**Senior Solutions Engineer**

[![Repositories](https://img.shields.io/badge/Repositories-14_public-2ea44f?logo=github)](https://github.com/morgandt-reed?tab=repositories)
[![Decision records](https://img.shields.io/badge/Decision_records-32-blue)](#how-i-decide)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Tech Radar](https://img.shields.io/badge/Tech_Radar-Skills-orange?logo=target)](https://gist.github.com/morgandt-reed/ceba0f61b20253c9d3de2b7b284ed396)

*Platform engineering, cloud infrastructure, data platforms, and AI systems*

</div>

---

## About

I build the engineering around a system, not just the system: the gates, the
guardrails, the tests and the decision records that let other people change it
safely six months later.

Two things are true of every repository below, and they are the point of the
portfolio rather than a detail of it.

**The CI badge means something.** No repository here uses `continue-on-error`,
`|| true` or `soft_fail` to keep a badge green. Every pipeline can fail, and
several did until the code was fixed — a nonexistent action version, a Maven
reactor that needed every module present, an nginx that ran perfectly while every
health probe was refused because `localhost` resolved to IPv6 first. A badge that
cannot fail measures nothing.

**Each README describes what the code does, not what it aspires to.** Where a
feature is designed but not built, it sits under Roadmap and the decision record
says so. Where a decision record describes a direction rather than the current
contents, its status is *Proposed*, not *Accepted* — seven of the thirty-two are.

---

## Featured work

<table>
<tr>
<td width="50%">

### Agentic SDLC

[![Agentic SDLC Harness](https://img.shields.io/badge/ASF-Agentic_SDLC_Harness-D97757?style=flat-square&logo=anthropic)](https://github.com/morgandt-reed/agentic-sdlc-harness)

Agent configuration treated as compiler output. A tool-neutral spec format
compiles into `.claude/` — and into a second, deliberately different layout, so
tool-independence is exercised rather than asserted — with a lock file and a
drift gate whose whole rule is one equality:
`render(merge(fresh, on_disk)) != on_disk`. Output is byte-identical across
three operating systems, because a gate that reports differences nobody made
gets switched off.

[![Brownfield AI Readiness](https://img.shields.io/badge/Brownfield-AI_Readiness_Scanner-3776AB?style=flat-square&logo=python)](https://github.com/morgandt-reed/brownfield-ai-readiness)

An assessment method for whether an existing application estate is ready for
agentic tooling, and a scanner implementing only the part of it that is
mechanical. Dimensions with no machine signal are reported unscored rather than
as zero, there is deliberately no composite score, and the README's worked
example is diffed against live CLI output in CI.

</td>
<td width="50%">

### AI economics

[![LLM Inference Economics](https://img.shields.io/badge/Build_vs_Buy-LLM_Inference_Economics-2E8B57?style=flat-square&logo=nvidia)](https://github.com/morgandt-reed/llm-inference-economics)

A build-vs-buy model for LLM inference where every price is public, dated and
cited — a provenance test suite fails the build if any number loses its source.
The position it defends: self-hosting an open-weight model competes against that
model's own API, not a frontier one, and the one break-even the tool does find
prints together with the warning that the comparison is rigged.

</td>
</tr>
<tr>
<td width="50%">

### AI systems

[![LangGraph RAG](https://img.shields.io/badge/LangGraph-RAG_Assistant-412991?style=flat-square&logo=openai)](https://github.com/morgandt-reed/langgraph-rag-assistant)

A retrieval service on a LangGraph state machine. Chroma returns *distances*, so
they are converted to similarities before routing — without that, the closest
match scores lowest and the confidence gate runs backwards. Answers cite the
chunks they used, and low-similarity retrieval reaches a fallback instead of a
confident guess.

[![HuggingFace Local LLM](https://img.shields.io/badge/HuggingFace-Local_LLM-FF6F00?style=flat-square&logo=huggingface)](https://github.com/morgandt-reed/huggingface-local-llm)

Local LoRA/QLoRA fine-tuning that derives its configuration from the hardware it
finds. 4-bit quantisation and paged optimizers are CUDA-only, so on Apple Silicon
it selects fp32 and a batch of one rather than failing halfway through a model
load.

</td>
<td width="50%">

### Event-driven and data

[![Event-Driven](https://img.shields.io/badge/RabbitMQ-Event_Driven-FF6600?style=flat-square&logo=rabbitmq)](https://github.com/morgandt-reed/event-driven-architecture)

Event sourcing with an aggregate that enforces its own invariants, optimistic
concurrency in the event store, and idempotent consumption keyed on
`(event_id, handler_name)` — a single-column key would let one consumer suppress
an event for every other, which in an order domain reads as "sometimes we don't
charge".

[![Databricks ETL](https://img.shields.io/badge/Databricks-ETL_Pipeline-FF3621?style=flat-square&logo=databricks)](https://github.com/morgandt-reed/databricks-etl-pipeline)

Medallion pipeline where Silver is a Delta `MERGE` on `event_id`, so re-running it
is idempotent rather than duplicating the layer. Data-quality checks dispatch on
column type instead of assuming numeric.

</td>
</tr>
<tr>
<td width="50%">

### Containers and Kubernetes

[![Docker Microservices](https://img.shields.io/badge/Docker-Microservices_Template-2496ED?style=flat-square&logo=docker)](https://github.com/morgandt-reed/docker-microservices-template)

Three-tier FastAPI/PostgreSQL/nginx stack with RED metrics on the API and a
readiness probe that returns 503 when the database is unreachable, rather than
reporting healthy with a disconnected dependency.

[![Kubernetes Patterns](https://img.shields.io/badge/Kubernetes-Deployment_Patterns-326CE5?style=flat-square&logo=kubernetes)](https://github.com/morgandt-reed/kubernetes-deployment-patterns)

Manifests, a Helm chart and blue-green/canary examples, validated with
`kubeconform` and scanned in CI. The chart's pod and container security contexts
are split, because the merged form the API server rejects renders fine locally.

</td>
<td width="50%">

### Backend and observability

[![Spring Boot](https://img.shields.io/badge/Spring_Boot-Microservices-6DB33F?style=flat-square&logo=springboot)](https://github.com/morgandt-reed/spring-boot-microservices)

Spring Cloud services where the gateway verifies the JWT and injects identity
headers after stripping any the client supplied, and inventory updates are a
single conditional `UPDATE` so the database arbitrates oversell rather than a
read-modify-write losing it.

[![Monitoring Stack](https://img.shields.io/badge/Prometheus-Observability_Stack-E6522C?style=flat-square&logo=prometheus)](https://github.com/morgandt-reed/monitoring-observability-stack)

Prometheus, Grafana, Loki and Alertmanager with alert rules unit-tested by
`promtool test rules` — CPU normalised by host cores, memory guarded against a
zero limit, and container-down detected per container rather than only when
every container disappears.

</td>
</tr>
<tr>
<td width="50%">

### Infrastructure as code

[![Terraform IaC](https://img.shields.io/badge/Terraform-IaC_Demos-7B42BC?style=flat-square&logo=terraform)](https://github.com/morgandt-reed/infrastructure-as-code-demos)

AWS modules including a VPC whose NAT topology is correct in both the
single-gateway and per-AZ branches, plus a bootstrap phase for the
chicken-and-egg problem module libraries usually skip. Session Manager by
default; no SSH rule unless you ask for one.

[![AWS CDK](https://img.shields.io/badge/AWS_CDK-Cloud_Patterns-FF9900?style=flat-square&logo=amazonaws)](https://github.com/morgandt-reed/aws-cdk-patterns)

TypeScript CDK with Aurora Serverless v2 in isolated subnets and deletion
protection derived from the environment's backup retention, so dev tears down and
prod is protected by the same expression. `cdk synth` runs for all three
environments in CI, because a cross-stack cycle only appears when the whole app
synthesises.

</td>
<td width="50%">

### Delivery

[![CI/CD Pipelines](https://img.shields.io/badge/GitHub_Actions-CI/CD_Templates-2088FF?style=flat-square&logo=githubactions)](https://github.com/morgandt-reed/cicd-pipeline-templates)

Reusable workflows (`on: workflow_call`) for Docker, Terraform, Python and
Kubernetes. Images are scanned **before** they are pushed and on pull requests,
OIDC replaces stored cloud credentials, and the Terraform plan reaches the PR
comment through an environment variable rather than string interpolation — a
backtick in a resource name is otherwise code execution.

</td>
</tr>
</table>

---

## How I decide

Each repository carries architecture decision records in `docs/adr/`. They state
what was decided, what it costs, and what was rejected — including the decisions
that turned out to be wrong. Six worth reading:

- **[Self-hosting competes with the open model's own API, not a frontier API](https://github.com/morgandt-reed/llm-inference-economics/blob/main/docs/adr/0001-what-self-hosting-competes-with.md)**
  — the comparison everyone runs prices weights you cannot download onto GPUs you
  are paying for. Against the correct comparator, scale dilutes fixed costs but
  never drops below marginal cost, so no head count breaks even.

- **[Prefer workload identity over any stored credential](https://github.com/morgandt-reed/infrastructure-as-code-demos/blob/main/docs/adr/0002-eliminate-the-secret.md)**
  — eliminating a requirement beats automating it. With platform-native identity
  a connection string carries no confidential material and the token refreshes
  itself, so there is no rotation problem left to solve. With the honest limits:
  third-party SaaS that only accepts a static key, and legacy systems.

- **[RAG maturity level: naive retrieval behind a deterministic state machine](https://github.com/morgandt-reed/langgraph-rag-assistant/blob/main/docs/adr/0001-rag-maturity-level.md)**
  — names the tier this repository actually implements and argues it is the right
  default. The common mistake is reaching for agentic RAG where advanced RAG was
  enough: it buys cost, latency and error surface for nothing.

- **[Alert on error-budget burn rate, not on static thresholds](https://github.com/morgandt-reed/monitoring-observability-stack/blob/main/docs/adr/0002-slo-burn-rate-over-static-thresholds.md)**
  — *Proposed*, and it says why it is not simply switched on: at 99.9%, a service
  serving ten requests an hour hits a burn rate of 100 the moment one returns a
  500, so a minimum-request guard has to come first.

- **[Borrow distributed-systems patterns for agentic systems, but not the retry semantics](https://github.com/morgandt-reed/event-driven-architecture/blob/main/docs/adr/0003-agentic-systems-are-not-microservices.md)**
  — saga compensation transfers; blind retry does not. A retry that is safe for a
  deterministic handler becomes dangerous when the same input can be interpreted
  differently on the second attempt.

- **[Scanner gates block the build](https://github.com/morgandt-reed/cicd-pipeline-templates/blob/main/docs/adr/0003-scanner-gates-must-block.md)**
  — and the honest cost of that: real gates create friction and false positives,
  so the answer is tuned severity thresholds and justified per-finding
  suppressions that still fail on anything new, not a blanket bypass.

The remaining twenty-six are linked from each repository's **Design decisions**
section.

---

## Tech

| | |
|---|---|
| **Languages** | Python · Java · TypeScript · HCL · SQL |
| **Containers** | Docker · Kubernetes · Helm |
| **Cloud** | AWS · Terraform · AWS CDK · GitHub Actions |
| **Data** | PostgreSQL · Databricks · Spark · Delta Lake |
| **AI/ML** | LangGraph · LangChain · Hugging Face · PEFT/LoRA · ChromaDB |
| **Observability** | Prometheus · Grafana · Loki · Alertmanager |
| **Backend** | Spring Boot · FastAPI · RabbitMQ · Redis |

---

<div align="center">

**Open to opportunities** in Solutions Engineering, Platform Engineering and DevOps.

</div>
