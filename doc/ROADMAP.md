# Project Roadmap

This document describes the planned milestones and tasks for **cfr-engine-cs**.

---

## Milestone 0 — Repo bootstrap
**Goal**: Initialize repository and basic project structure.

- [x] Create solution and three projects (Engine, App, Tests)  
- [x] Add `.gitignore`, `README.md` 
- [x] Verify `dotnet build / test / run` works  
- [x] Add VS Code debug configuration  

---

## Milestone 1 — CFR core with Kuhn Poker
**Goal**: Implement regret matching and the basic CFR loop with Kuhn Poker as the first example.

- [ ] Implement `RegretMatching`  
- [ ] Define `Node` data structure  
- [ ] Add `IGame` interface  
- [ ] Implement `KuhnPoker` game  
- [ ] Implement recursive CFR engine  
- [ ] Add CLI entry point with basic options  
- [ ] Unit tests for regret matching and Kuhn payoff logic  

---

## Milestone 2 — Hardening & Metrics
**Goal**: Stabilize engine and add diagnostics.

- [ ] NaN/zero-sum guards in strategy normalization  
- [ ] Logging of iteration count, node count, elapsed time  
- [ ] CLI options: `--iters`, `--seed`, `--log-interval`, `--export-path`  
- [ ] Export/import average strategy (JSON or binary)  
- [ ] Microbenchmarks with BenchmarkDotNet  

---

## Milestone 3 — MCCFR
**Goal**: Add Monte Carlo CFR with public chance sampling.

- [ ] Implement MCCFR loop  
- [ ] RNG seeding for reproducibility  
- [ ] Evaluation: self-play and exploitability approximation  
- [ ] Unit tests to check distribution and reproducibility  

---

## Milestone 4 — Texas Hold’em abstraction (MVP)
**Goal**: Introduce abstraction for Hold’em and run a minimal MCCFR experiment.

- [ ] Extend `InfosetKey` (street, position, hole bucket, board bucket, SPR bucket, action sequence code)  
- [ ] Add hole-card and board texture bucketing  
- [ ] Add action abstraction (Fold / CheckCall / 0.5P / 1.0P / All-in, plus preflop raises)  
- [ ] Implement canonicalization for suits  
- [ ] Smoke test with training log and infoset growth  

---

## Milestone 5 — Parallelization
**Goal**: Use multi-core processing to speed up training.

- [ ] Per-thread worker tables with periodic merge  
- [ ] Implement regret and strategy sum merging  
- [ ] Benchmark throughput vs. single-thread  
- [ ] Validate correctness between parallel and single-thread  

---

## Milestone 6 — Benchmarking & Visualization
**Goal**: Add performance benchmarks and visualization.

- [ ] BenchmarkDotNet for regret matching and iteration throughput  
- [ ] Export training metrics (entropy, win rate, node count)  
- [ ] Add plots (CSV + Python/Excel/Plot script)  
- [ ] Document benchmark results in README  

---

## Milestone 7 — Packaging & Release
**Goal**: Prepare the engine for external use.

- [ ] Add CLI commands: `train`, `eval`, `export`, `import`  
- [ ] Add versioning to exported strategy files  
- [ ] (Optional) Publish as NuGet package  
- [ ] Provide usage examples in README  
