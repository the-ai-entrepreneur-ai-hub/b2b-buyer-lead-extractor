# SaaS Buyer Extractor

> Identify companies actively evaluating SaaS tools by mining review sites and buying intent signals

[![Try on Apify](https://img.shields.io/badge/Try_on-Apify_Store-00C7B7?style=for-the-badge&logo=apify)](https://apify.com/george.the.developer/saas-buyer-extractor)
[![GitHub](https://img.shields.io/badge/Source-GitHub-181717?style=for-the-badge&logo=github)](https://github.com/the-ai-entrepreneur-ai-hub/b2b-buyer-lead-extractor)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

---

## Overview

SaaS Buyer Extractor identifies companies showing active buying intent for software solutions. It mines review platforms like G2 and Capterra, monitors comparison pages, and tracks technology adoption signals to find companies in active buying cycles. Delivers sales-ready leads with intent scores and competitive context.

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white) ![Crawlee](https://img.shields.io/badge/Crawlee-00C7B7?style=flat&logo=apify&logoColor=white) ![Cheerio](https://img.shields.io/badge/Cheerio-E88C1F?style=flat&logo=javascript&logoColor=white) ![Apify](https://img.shields.io/badge/Apify_SDK-00C7B7?style=flat&logo=apify&logoColor=white)

---

## Architecture

```mermaid
graph LR
    A["Input: SaaS Category / Filters"] --> B["Crawlee Engine"]
    B --> C["Review Platforms"]
    C --> D["Data Extraction"]
    D --> E["Clean & Structure"]
    E --> F["Output: JSON/CSV"]

    style A fill:#F5C542,stroke:#D4A017,color:#1a1a2e
    style B fill:#6366f1,stroke:#4338ca,color:#ffffff
    style C fill:#f97316,stroke:#c2410c,color:#ffffff
    style D fill:#8b5cf6,stroke:#6d28d9,color:#ffffff
    style E fill:#06b6d4,stroke:#0891b2,color:#ffffff
    style F fill:#34d399,stroke:#065f46,color:#1a1a2e
```

---

## How It Works

```mermaid
sequenceDiagram
    participant U as User
    participant A as SaaS Buyer Extractor
    participant T as Review Platforms
    participant D as Apify Dataset

    U->>A: Provide input (SaaS Category / Filters)
    A->>A: Validate & configure
    A->>T: Navigate & extract data
    T-->>A: Raw HTML / JSON
    A->>A: Parse, clean & deduplicate
    A->>D: Store structured results
    D-->>U: Download JSON / CSV / Excel
```

**Step-by-step:**

1. **Input Validation** — Your configuration is validated and the scraping session is initialized with optimal proxy settings
2. **Smart Crawling** — Crawlee manages request queues, retries, and proxy rotation automatically for maximum reliability
3. **Data Extraction** — Structured data is parsed from each page using optimized selectors and anti-detection measures
4. **Deduplication** — Results are deduplicated and cleaned to ensure high data quality with no duplicates
5. **Output Delivery** — Clean, structured data is saved to your Apify dataset for download or API access

---

## Input Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `softwareCategory` | `String` | SaaS category (e.g., CRM, ERP, HRMS) |
| `targetCompanySize` | `String` | Company size: startup, smb, mid-market, enterprise |
| `maxLeads` | `Number` | Maximum buyer leads to extract |
| `intentSignals` | `Array` | Types of buying signals to track |
| `geography` | `String` | Target geography for leads |

### Input Example

```json
{
  "softwareCategory": "CRM",
  "targetCompanySize": "mid-market",
  "maxLeads": 200,
  "intentSignals": [
    "review_written",
    "comparison_visited",
    "free_trial_started"
  ],
  "geography": "North America"
}
```

---

## Output Fields

| Field | Type | Description |
|-------|------|-------------|
| `companyName` | `String` | Company name |
| `industry` | `String` | Company industry |
| `companySize` | `String` | Employee count range |
| `intentScore` | `Number` | Buying intent score (0-100) |
| `signalsDetected` | `Array` | Specific buying signals found |
| `currentStack` | `Array` | Current software tools detected |
| `reviewActivity` | `String` | Recent review/comparison activity |
| `website` | `String` | Company website |
| `decisionMakers` | `Array` | Key decision-maker titles identified |

### Output Example

```json
{
  "companyName": "TechFlow Solutions",
  "industry": "SaaS",
  "companySize": "201-500",
  "intentScore": 87,
  "signalsDetected": [
    "Wrote G2 comparison review",
    "Visited pricing pages of 3 CRM vendors"
  ],
  "currentStack": [
    "HubSpot (free tier)",
    "Slack",
    "Notion"
  ],
  "reviewActivity": "Compared 4 CRM solutions on G2 in last 7 days",
  "website": "https://techflow.io",
  "decisionMakers": [
    "VP of Sales",
    "Head of Revenue Operations"
  ]
}
```

---

## Use Cases

- **SDR Prospecting** — Feed sales reps with intent-qualified leads showing active buying behavior
- **ABM Campaigns** — Build account-based marketing lists of companies in active software evaluation
- **Competitive Displacement** — Find companies dissatisfied with competitor products based on review signals
- **Market Sizing** — Quantify the active buyer market for any SaaS category by region
- **Channel Sales** — Identify companies that may need implementation partners or consultants

---

## Data Flow

```mermaid
flowchart TD
    subgraph Input
        A["SaaS Category / Filters"] --> B[Proxy Configuration]
        B --> C[Max Results & Filters]
    end
    subgraph Processing
        D[Smart Request Queue] --> E[Anti-Bot Handling]
        E --> F[Data Extraction]
        F --> G[Deduplication & Cleaning]
    end
    subgraph Output
        H[JSON Dataset] --> I[CSV Export]
        I --> J[API Access]
    end
    Input --> Processing --> Output

    style A fill:#F5C542,stroke:#D4A017,color:#1a1a2e
    style G fill:#06b6d4,stroke:#0891b2,color:#ffffff
    style J fill:#34d399,stroke:#065f46,color:#1a1a2e
```

---

## Pricing

This actor uses Apify's **Pay-Per-Event** pricing. You only pay for what you use.

| Event | Price | Description |
|-------|-------|-------------|
| `lead-extracted` | $0.01 | Per buyer intent lead extracted |
| `signal-tracked` | $0.005 | Per buying signal tracked |

> Free tier available on Apify. No credit card required to start.

---

## Getting Started

### Run on Apify Console

1. Go to [SaaS Buyer Extractor on Apify Store](https://apify.com/george.the.developer/saas-buyer-extractor)
2. Click **"Try for free"**
3. Configure your input parameters
4. Click **"Start"** and wait for results
5. Download your data as JSON, CSV, or Excel

### Run via API

```bash
curl -X POST "https://api.apify.com/v2/acts/george.the.developer~saas-buyer-extractor/runs" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -d '{"softwareCategory":"CRM","targetCompanySize":"mid-market","maxLeads":200,"intentSignals":["review_written","comparison_visited","free_trial_started"],"geography":"North America"}'
```

### Run with Python

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("george.the.developer/saas-buyer-extractor").call(
    run_input={
    "softwareCategory": "CRM",
    "targetCompanySize": "mid-market",
    "maxLeads": 200,
    "intentSignals": [
        "review_written",
        "comparison_visited",
        "free_trial_started"
    ],
    "geography": "North America"
}
)

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

---

## Tech Stack

| Technology | Purpose |
|------------|---------|
| **Node.js** | Runtime environment |
| **Crawlee** | Web scraping and crawling framework |
| **Cheerio** | Fast HTML parsing and data extraction |
| **Apify SDK** | Actor lifecycle, storage, and proxy management |

---

## Related Actors

More data extraction tools by [George The Developer](https://apify.com/george.the.developer):

- [Reddit Scraper Pro](https://apify.com/george.the.developer/reddit-scraper-pro) — Extract posts, comments, user profiles, and subreddit data from Reddit at scale 
- [AI Training Data Scraper](https://apify.com/george.the.developer/ai-training-data-scraper) — Collect structured, clean datasets from the web purpose-built for training machi
- [Influencer Marketing Intel](https://apify.com/george.the.developer/influencer-marketing-intel) — Discover and analyze social media influencers with engagement metrics, audience 
- [Google Maps Leads & Website Audit](https://apify.com/george.the.developer/google-maps-leads-website-audit) — Extract business leads from Google Maps with automated website audits for contac
- [App Review Pain Miner](https://apify.com/george.the.developer/app-review-pain-miner) — Extract and analyze app store reviews to discover user pain points, feature requ

[View all actors on Apify Store >>>](https://apify.com/george.the.developer)

---

## Support

- **Apify Store**: [https://apify.com/george.the.developer/saas-buyer-extractor](https://apify.com/george.the.developer/saas-buyer-extractor)
- **GitHub Issues**: [Report a bug](https://github.com/the-ai-entrepreneur-ai-hub/b2b-buyer-lead-extractor/issues)
- **Author**: [George The Developer](https://apify.com/george.the.developer)

---

## License

MIT License. See [LICENSE](LICENSE) for details.

---

*Built with Crawlee and the Apify SDK by [George The Developer](https://apify.com/george.the.developer). Star this repo if you find it useful!*
