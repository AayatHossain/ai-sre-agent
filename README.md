# ai-sre-agent

An AI agent that works like an on-call Site Reliability Engineer: when a live microservices system breaks, it investigates metrics, logs and traces, finds the root cause, and proposes a fix that a human approves before it is applied.

> **Status:** early development. Nothing below is finished yet; the roadmap shows what is done.

## Why
When a system made of many services fails, an engineer has to dig through dashboards, logs and traces to find the cause, often in the middle of the night. This project explores how far an LLM-based agent can take that investigation on its own, how safely it can act, and how to measure that honestly.

## How it will work
1. **A real system to break.** The [OpenTelemetry Demo](https://opentelemetry.io/docs/demo/) shop runs on Kubernetes with full monitoring (Prometheus, Loki, Tempo, Grafana).
2. **Faults on purpose.** Chaos Mesh and the demo's feature flags inject failures such as memory leaks, bad config, network delay and crashed dependencies.
3. **An investigating agent.** Specialist agents read logs, metrics and traces through MCP tools, and a lead agent combines their findings into a root cause.
4. **Safe actions.** The agent has read-only access. Any fix goes through policy checks and human approval, and every action is logged.
5. **Honest evaluation.** Because every fault is injected on purpose, the correct answer is known. The agent is scored on root-cause accuracy, time, cost and unsafe actions, on our own fault set and on public benchmarks ([ITBench](https://github.com/itbench-hub/ITBench), [AIOpsLab](https://github.com/microsoft/AIOpsLab)).

## Planned stack
Python, LangGraph, MCP, FastAPI, Postgres + pgvector, Redis, Kubernetes (kind / k3s), Helm, Argo CD, OpenTelemetry, Prometheus, Loki, Tempo, Grafana, Chaos Mesh, Open Policy Agent, Langfuse, Next.js, GitHub Actions.

## Roadmap
- [ ] **Phase 0:** repository setup
- [ ] **Phase 1:** local Kubernetes cluster with the demo app and the monitoring stack
- [ ] **Phase 2:** fault injection and a catalogue of reproducible faults
- [ ] **Phase 3:** MCP tools for metrics, logs, traces and Kubernetes
- [ ] **Phase 4:** first single-agent baseline
- [ ] **Phase 5:** evaluation harness and baseline results
- [ ] **Phase 6:** multi-agent investigation and incident memory
- [ ] **Phase 7:** safety layer, human approval (Slack and dashboard) and remediation
- [ ] **Phase 8:** small log-triage model to cut cost and latency
- [ ] **Phase 9:** evals in CI that block regressions
- [ ] **Phase 10:** results on public benchmarks, demo and write-up

## License
[MIT](LICENSE)
