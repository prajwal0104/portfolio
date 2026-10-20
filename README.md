# Engineering Portfolio: 12 Production Systems & Autonomous Agents

Welcome to the public portfolio and technical documentation repository for **Prajwal Mahesh** ([github.com/prajwal0104](https://github.com/prajwal0104)).

This repository serves as the public architectural showcase, documentation catalog, and interactive working model for **12 production-grade software systems**, autonomous AI browser agents, and specialized domain engineering tools.

> **Note on Codebase Visibility**: The underlying core source code repositories are maintained as private intellectual property. This public portfolio provides comprehensive architecture specifications, input/output schemas, test matrices, and live interactive working models for all 12 systems.

---

## 🌐 Live Interactive Working Model Playground

Explore live, interactive simulations of all 12 systems directly in your browser:
👉 **[Launch Interactive Working Model Playground](https://prajwal0104.github.io/portfolio/)**

---

## 📚 Master Project Directory

| # | System Name | Category | Primary Stack | Architecture & Specs | Working Model Demo |
|---|-------------|----------|---------------|----------------------|--------------------|
| 1 | **Autonomous Web Agent** | AI Autonomous Navigation | Playwright, Pydantic v2, LLM Reasoning | [Read Specs](projects/autonomous-web-agent.md) | [Try Live](https://prajwal0104.github.io/portfolio/#autonomous-web-agent) |
| 2 | **FinTrack** | Full-Stack Financial Platform | React, TypeScript, ASP.NET Core, EF Core | [Read Specs](projects/fintrack.md) | [Try Live](https://prajwal0104.github.io/portfolio/#fintrack) |
| 3 | **A11y Sentinel** | Web Accessibility Auditor | BeautifulSoup4, Playwright, WCAG 2.1 | [Read Specs](projects/a11y-sentinel.md) | [Try Live](https://prajwal0104.github.io/portfolio/#a11y-sentinel) |
| 4 | **CareerForge AI** | Skill Gap & Resume Engine | BeautifulSoup4, Pydantic v2, NLP | [Read Specs](projects/career-forge-ai.md) | [Try Live](https://prajwal0104.github.io/portfolio/#career-forge-ai) |
| 5 | **PriceRadar Core** | Arbitrage & Glitch Monitor | BeautifulSoup4, Pydantic v2, Playwright | [Read Specs](projects/price-radar-core.md) | [Try Live](https://prajwal0104.github.io/portfolio/#price-radar-core) |
| 6 | **SEC Insight Engine** | SEC 10-K/10-Q Ratio Auditor | BeautifulSoup4, Pydantic v2, SEC EDGAR | [Read Specs](projects/sec-insight-engine.md) | [Try Live](https://prajwal0104.github.io/portfolio/#sec-insight-engine) |
| 7 | **OmniResearch Core** | Deep Web Fact Synthesizer | BeautifulSoup4, Pydantic v2, AI Radar | [Read Specs](projects/omni-research-core.md) | [Try Live](https://prajwal0104.github.io/portfolio/#omni-research-core) |
| 8 | **FlowRPA Core** | Browser RPA & Self-Healing | Playwright, Pydantic v2, Levenshtein | [Read Specs](projects/flow-rpa-core.md) | [Try Live](https://prajwal0104.github.io/portfolio/#flow-rpa-core) |
| 9 | **CyberProbe AI** | OWASP HTTP Security Auditor | Playwright, Pydantic v2, OWASP Top 10 | [Read Specs](projects/cyber-probe-ai.md) | [Try Live](https://prajwal0104.github.io/portfolio/#cyber-probe-ai) |
| 10 | **AeroRoute Agent** | Multi-Hop Route Optimizer | Playwright, Pydantic v2, Pareto Frontier | [Read Specs](projects/aero-route-agent.md) | [Try Live](https://prajwal0104.github.io/portfolio/#aero-route-agent) |
| 11 | **CleanDOM Crawler** | Semantic Scraper & RAG Chunker| BeautifulSoup4, Pydantic v2, RAG | [Read Specs](projects/clean-dom-crawler.md) | [Try Live](https://prajwal0104.github.io/portfolio/#clean-dom-crawler) |
| 12 | **UITest Forge** | UI Bug Hunter & Test Synthesizer| Playwright, Pydantic v2, Pytest | [Read Specs](projects/ui-test-forge.md) | [Try Live](https://prajwal0104.github.io/portfolio/#ui-test-forge) |

---

## 🏗️ Architectural Highlights

```mermaid
graph TD
    subgraph Autonomous Agents & Crawlers
        AWA[Autonomous Web Agent]
        OMNI[OmniResearch Core]
        RPA[FlowRPA Core]
        FORGE[UITest Forge]
    end

    subgraph Data Extraction & Optimization Engines
        AERO[AeroRoute Agent]
        PRICE[PriceRadar Core]
        SEC[SEC Insight Engine]
        DOM[CleanDOM Crawler]
    end

    subgraph Compliance, Security & Enterprise Platforms
        A11Y[A11y Sentinel]
        CYBER[CyberProbe AI]
        CAREER[CareerForge AI]
        FIN[FinTrack Platform]
    end

    AWA & OMNI & RPA & FORGE --> Playwright[Playwright Browser Automation Core]
    AERO & PRICE & SEC & DOM --> Pydantic[Pydantic v2 Data Validation Architecture]
    A11Y & CYBER & CAREER & FIN --> Production[Continuous Multi-OS CI/CD Pipelines]
```

---

## 🧪 Testing & Reliability Standards

- **100% Offline-First Unit Tests**: All backend engines and crawlers are tested with decoupled mock HTML fixtures and strict Pydantic schemas, guaranteeing zero network flakiness.
- **Cross-Platform Matrix CI**: Verified across 9-job GitHub Actions matrix workflows on Ubuntu, Windows, and macOS (Python 3.11, 3.12, 3.13).
- **Type Safety**: Built with strict type hints and Pydantic v2 models for complete contract guarantees.

---

## 📬 Contact & Inquiries

For technical collaborations, enterprise inquiries, or access to underlying private repositories:
- **GitHub**: [@prajwal0104](https://github.com/prajwal0104)
