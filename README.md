# OffPeakAI

![Status](https://img.shields.io/badge/Status-Prototype-orange)
![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)

**High-Performance AI. Low-Priority Pricing.**

**OffPeakAI** is a demand-response interface for Large Language Models (LLMs). It democratizes "Compute Arbitrage" by allowing students and researchers to trade *latency* for *cost*, accessing top-tier reasoning models (like GPT-4o, DeepSeek-V3, Claude 3.5) at significantly reduced rates by utilizing "Batch" and "Off-Peak" API windows.

---

##The Problem
**The "Compute Heatwave":** AI inference costs are static for consumers ($20/mo), regardless of global server load.
- Users pay "Peak Prices" even when they don't need instant answers.
- Students in regions with lower purchasing power are priced out of "Reasoning" class models (O1, Gemini 1.5 Pro).

## ⚡ The Solution
Cloud compute has "Off-Peak" hours and "Batch" processing modes that are 50-75% cheaper. **OffPeakAI** acts as a smart router (middleman) to access these savings:

1.  **🚀 Instant Mode:** Routes directly to standard APIs (Market Price).
2.  **⏳ Thrift Mode (Batch):** Queues prompts to be processed within 12-24 hours via OpenAI/Anthropic Batch APIs (50% Discount).
3.  **🌙 DeepNight Mode:** (Experimental) Routes traffic to providers offering specifically timed off-peak incentives.

##Architecture
The system functions as a proxy layer between the User and the Model Providers.

```mermaid
graph TD
    A[User Prompt] --> B{Router Logic}
    
    %% Expensive Path
    B -- Urgent? --> C[Direct API Call]
    C --> E[Response $$$]
    
    %% Cheap Path
    B -- Can Wait? --> D[Batch Queue .jsonl]
    D --> F[Cron Job / Worker]
    F --> G[Batch API Endpoint]
    G --> H[Response $]

    %% Styling (Optional - Makes it look Pro)
    style E fill:#ffcccc,stroke:#ff0000,stroke-width:2px
    style H fill:#ccffcc,stroke:#009900,stroke-width:2px
