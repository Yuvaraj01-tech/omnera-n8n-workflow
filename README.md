# OMNERA

> **Smarter Finance. Stronger Futures.**  
> *More than a platform. Your growth partner.*

Omnera is a modern financial platform designed to streamline microfinance workflows, loan origination, daily EMI collections, field agent tracking, and portfolio analytics.

This repository hosts the **Omnera Automated Content & Brand Communication Pipeline**, an end-to-end AI workflow built in n8n that automates the generation, visual rendering, review, and publishing of brand updates to Instagram.

---

## Current Architecture

The operational automation stack consists of an AI content generation pipeline, image rendering service, human-in-the-loop review, and publishing via the Meta Graph API:

```mermaid
graph LR
    A[Schedule Trigger] --> B[Topic & Copy: Groq LLM]
    B --> C[Poster Rendering Service]
    C --> D[Operator Review: ntfy + Form]
    D -->|Approved| E[Instagram Graph API]
    D -->|Rejected| F[End / Regulate]
