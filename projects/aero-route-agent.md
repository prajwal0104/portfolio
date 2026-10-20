# AeroRoute Agent: Multi-Hop Flight Optimizer & Pareto Layover Engine

[![Python](https://img.shields.io/badge/Python-3.11%2B-blue.svg)](https://www.python.org/)
[![Pydantic](https://img.shields.io/badge/Validation-Pydantic%20v2-e92063.svg)](https://pydantic.dev/)
[![Optimization](https://img.shields.io/badge/Algorithm-Pareto%20Frontier-blueviolet.svg)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Privacy](https://img.shields.io/badge/Repository-Private-critical.svg)](#)

An intelligent multi-hop flight route explorer and multi-objective Pareto optimization agent. AeroRoute simultaneously optimizes ticket cost, total travel duration, layover transfer risk, and baggage inclusions to identify non-dominated Pareto frontier travel itineraries.

Built on **Playwright**, **Pydantic v2**, **BeautifulSoup4**, and **Rich**.

---

## 🎯 Architecture & Data Flow

```mermaid
flowchart TD
    Req[Travel Request: Origin, Dest, Dates] --> RouteSearch[Flight Graph Traverser]
    RouteSearch --> MultiHop[Multi-Hop Connection Generator]
    MultiHop --> FlightLegs[Flight Legs & Layover Buffers]
    FlightLegs --> LayoverRisk[Airport Transfer & Customs Risk Evaluator]
    FlightLegs --> CostModel[Fare Class & Baggage Cost Normalizer]
    LayoverRisk & CostModel --> ParetoOptimizer[Multi-Objective Pareto Engine]
    ParetoOptimizer --> NonDominated[Pareto Optimal Frontier Itineraries]
    NonDominated --> Ranker[Trade-off Ranker: Fastest vs Cheapest vs Balanced]
    Ranker --> CLI[Rich Terminal Itinerary Table]
```

---

## 🔬 Working Model & CLI Execution Walkthrough

### Example Command
```bash
python -m src.main --origin SFO --dest TYO --max-layovers 2 --balance-weights cost=0.5 duration=0.5
```

### Live Working Model Output
```text
╭──────────────────────────────────────────────────────────────────────────────╮
│                       ✈️ AeroRoute Agent v1.0.0                              │
│   Origin: SFO (San Francisco) ➔ Destination: TYO (Tokyo) | Max Layovers: 2   │
╰──────────────────────────────────────────────────────────────────────────────╯

Pareto Frontier Itinerary Evaluation:
┏━━━━━━━━┳━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━┓
┃ Option ┃ Routing Legs     ┃ Total Duration   ┃ Fare (USD)       ┃ Trade-off  ┃
┣━━━━━━━━╋━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━━━━━━━╋━━━━━━━━━━━━┫
┃ #1     ┃ SFO ➔ HND (Nonstop)┃ 11h 25m          ┃ $ 1,120.00       ┃ FASTEST    ┃
┃ #2     ┃ SFO ➔ ICN ➔ NRT   ┃ 14h 50m (2h lay) ┃ $   685.00       ┃ BALANCED ⭐┃
┃ #3     ┃ SFO ➔ SEA ➔ HND   ┃ 15h 10m (2h lay) ┃ $   720.00       ┃ RELIABLE   ┃
┃ #4     ┃ SFO ➔ TPE ➔ MNL ➔ NRT┃ 24h 30m         ┃ $   490.00       ┃ CHEAPEST   ┃
┗━━━━━━━━┻━━━━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━━━┻━━━━━━━━━━━━┛

⭐ Recommended Optimal Selection: Option #2 (Balanced)
  • Savings over Direct : $ 435.00 (38.8% discount)
  • Time Penalty        : + 3h 25m duration
  • Incheon (ICN) Layover Risk Score: 0.12 (Ultra-low transfer friction)
```

---

## ⚡ Core Features

- **Multi-Objective Pareto Optimization**: Discards dominated flight options that are both slower and more expensive than existing candidates.
- **Airport Minimum Connect Time (MCT) Validation**: Flags dangerous sub-45 minute international connections prone to luggage loss or missed boarding.
- **Unified Luggage Normalization**: Automatically normalizes baseline fares to account for carry-on vs checked bag add-on charges.
