# 1182.ee Scraper - Estonian Business Directory

Extract structured data from [1182.ee](https://1182.ee) — the 1182.ee Estonian business directory by keyword and get registry codes, phone numbers and emails for every listed company. Search any trade or business name and export clean, structured company records for lead generation and CRM import.

**[1182.ee Scraper - Estonian Business Directory on Apify →](https://apify.com/blackfalcondata/1182-ee-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword and location. Filter by 📝 description format, and more.

**Detail enrichment** — Fetch full descriptions, contact information for each record.

**Incremental mode** — Only get new or changed records since your last run. Content hash per record — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run duplicate detection across runs. Build audit trails of how records evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per ${NOUN} to control output size and cost.

**Result cap** — Stop after N records (up to 10.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every record returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured records from 1182.ee on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor records, track trends, and analyze market dynamics with structured, deduplicated data from 1182.ee.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Lead generation**
Extract contact details alongside ${NOUNS} to build targeted outreach lists for sales teams, partnerships, or B2B prospecting.

**AI / LLM training data**
Structured JSON per record is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "restoran",
  "maxResults": 100,
  "includeDetails": true,
  "descriptionMaxLength": 0,
  "compact": false,
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "skipReposts": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5,
  "descriptionFormat": "all"
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | What to look up in the directory — a category, trade or company name, in Estonian (e.g. "restoran", "ehitus", "hambaravi"). Paste a JSON array for several searches in one run: ["restoran","kohvik"]. |
| `location` | string | — | Keep only companies whose address is in this city or area (e.g. "Tallinn", "Pärnu"). Leave empty for all of Estonia. JSON array for several. |
| `maxResults` | integer | `100` | Maximum total companies (0 = unlimited). |
| `includeDetails` | boolean | `true` | Fetch each company's profile for phone numbers, email, website, description, opening hours, gallery, registry code and social links. Turn off for a faster, address-only list. |
| `descriptionMaxLength` | integer | `0` | Truncate the company description to N chars. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only — name, registry code, address, phone, email, website (for AI-agent/MCP workflows). |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty-string, and empty-array fields from each record before push. Smaller payloads for AI agents and dashboards. |
| `incrementalMode` | boolean | `false` | Compare against previous run state. stateKey is optional — defaults to a value derived from search inputs (queries, locations) so different filter sets never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked search universe. Leave empty to auto-generate from search inputs. |
| `emitUnchanged` | boolean | `false` | When incremental, also emit businesses that have not changed since the last run. |
| `emitExpired` | boolean | `false` | When incremental, also emit businesses that disappeared from the search results since the last run. |
| `skipReposts` | boolean | `false` | When incremental, skip companies whose content matches a listing that disappeared in a prior run (same company back under a new listing id). |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED companies. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of companies included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |
| `descriptionFormat` | enum | `"all"` | Choose which representation of the listing description to include. `all` keeps every variant; the others keep only the selected one. |
| `startUrls` | array | — | 1182.ee search-results URLs, e.g. https://www.1182.ee/search/restoran or https://www.1182.ee/otsing/restoran. When set, the query and location fields are ignored. |
| `lat` | number | — | Latitude of the centre point for the radius filter. Pair with longitude and radius. |
| `lon` | number | — | Longitude of the centre point for the radius filter. Pair with latitude and radius. |
| `radiusKm` | integer | — | Keep only businesses within this many kilometres of the centre point. Businesses without coordinates are kept. |

---

## Output fields

Every record returns the same 46-field schema. Missing values are `null` — never omitted.

- `listingId`
- `companyId`
- `name`
- `legalName`
- `regCode`
- `isClaimed`
- `category`
- `categories`
- `address`
- `street`
- `postalCode`
- `city`
- `country`
- `location`
- `latitude`
- `longitude`
- `phone`
- `phones`
- `phoneDetails`
- `email`
- `emails`
- `website`
- `description`
- `descriptionMarkdown`
- `slogan`
- `keywords`
- `rating`
- `reviewCount`
- `hours`
- `temporarilyClosedUntil`
- `logo`
- `images`
- `social`
- `socialLinks`
- `reservationUrl`
- `menuUrl`
- `slug`
- `profileUrl`
- `portalUrl`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `scrapedAt`
- `source`
- `contentHash`
- `changeType`

---

## Sample output

One object per record. Here is a real example from a production run:

```json
{
  "listingId": "117a45afc423b208af7a766e5a8e286cbbc7d4d454321aa0eaad39bbfae0542f",
  "companyId": "417969",
  "name": "Arco Color AS",
  "legalName": "AS Arco Color",
  "regCode": "11307227",
  "isClaimed": false,
  "category": null,
  "categories": [],
  "address": "Tule 25, 76505 Saue",
  "street": "Tule 25",
  "postalCode": "76505",
  "city": "Saue"
}
```

*Truncated — full records contain 46 fields. See Output fields for the complete schema.*

**[Try 1182.ee Scraper - Estonian Business Directory now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/1182-ee-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.0045 |
| Result | $0.0045 |

See the [actor on Apify](https://apify.com/blackfalcondata/1182-ee-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape 1182.ee?**
Use this actor on Apify to extract structured data from 1182.ee. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get 1182.ee data as JSON, CSV, or Excel?**
The actor writes each record to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape 1182.ee?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check 1182.ee's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each record gets a content hash. On subsequent runs, only new or changed records are emitted — saving time, compute, and storage. Expired records can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [1182.ee Scraper - Estonian Business Directory](https://apify.com/blackfalcondata/1182-ee-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
