# CFR Engine (C#)

A minimal **Counterfactual Regret Minimization (CFR)** / **Monte Carlo CFR (MCCFR)** engine implemented in C#.  
This project is designed as a learning and experimentation framework for game-theoretic algorithms, with a focus on applications in imperfect-information games such as poker.

---

## Features

- Core **CFR** algorithm implementation
- Extensible `IGame` interface to plug in different games  
- Support for **Infoset abstraction** (e.g., bucketing cards, board textures, stack sizes)  
- Example game implementations (Kuhn Poker, Texas Hold'em with abstraction – WIP)  
- Basic unit tests with **xUnit**  
- Ready-to-use CLI entry point for training and evaluation  


## Project Structure
```
cfr-engine-cs/
├─ Cfr.Engine/ # Core algorithm library
│ ├─ Core/ # CFR engine, regret matching, node structures
│ ├─ Game/ # Game definitions and interfaces
│ └─ Abstraction/ # Infoset bucketing and canonicalization
│
├─ Cfr.App/ # Console app (training entry point)
│ └─ Program.cs
│
├─ Cfr.Tests/ # Unit tests (xUnit)
│
├─ cfr-engine-cs.sln
└─ README.md
```

## Roadmap

- [x] Basic project structure with solution, class library, console app, tests  
- [ ] Implement regret matching and CFR loop  
- [ ] Add Kuhn Poker as a first working example  
- [ ] Add Texas Hold'em abstraction (hole buckets, board texture buckets, action abstraction)  
- [ ] Parallel MCCFR with public chance sampling  
- [ ] Benchmarking with BenchmarkDotNet  

