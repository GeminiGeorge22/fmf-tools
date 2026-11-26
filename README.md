# FMF Tools

FMF Tools is a catalog of remote MCP servers and pay-per-call APIs for agents.

`tools/list` is free. `tools/call` is pay-per-call. No account and no API key. Invalid input is not charged.

Full catalog (retested daily): https://tools.fmf-x402.workers.dev/?ref=github

As of 26 Nov 2026 the catalog lists 37,467 live-tested MCP servers and 3,709 live-tested paid APIs, including 130 first-party tools (144,026 verified or registry MCP catalog entries). Counts: https://tools.fmf-x402.workers.dev/api/summary.json and https://tools.fmf-x402.workers.dev/api/coverage.json

Directory MCP: `https://tools.fmf-x402.workers.dev/mcp`

Logo (400×400): [logo-400.png](logo-400.png)

## Priority servers

| Name | MCP URL |
|---|---|
| FMF Tools Directory | https://tools.fmf-x402.workers.dev/mcp |
| FMF Tools Web & Data | https://mpp-agent-data.fmf-x402.workers.dev/mcp |
| Bachelor Party Activity Finder | https://bachelor-party-activity-finder.fmf-x402.workers.dev/mcp |
| Bachelor Party Itinerary Builder | https://bachelor-party-itinerary-builder.fmf-x402.workers.dev/mcp |
| Etsy Movers | https://etsy-movers.fmf-x402.workers.dev/mcp |
| FMF Recipes | https://agent-recipes.fmf-x402.workers.dev/mcp |
| FMF Tools Wallet Intel | https://mpp-walletintel.fmf-x402.workers.dev/mcp |
| FMF Tools Shoe Count | https://shoe-count.fmf-x402.workers.dev/mcp |
| Black Friday Deals | https://black-friday-deals.fmf-x402.workers.dev/mcp |
| Black Friday Deal Monitor | https://black-friday-deal-monitor.fmf-x402.workers.dev/mcp |


## New pay-per-call tools (25 Nov 2026)

Each call is paid in USDC via x402 or MPP. tools/list is free. Invalid input is not charged.

- Landed Receipt Checker — Tells you whether a write or payment actually landed, so a timeout is not retried as a new charge. $0.002. https://tools.fmf-x402.workers.dev/tool/landed-receipt-write-outcome-checker?ref=github
- x402 Validate vs Discovery Checker — Checks whether an x402 resource that validates is actually listed in discovery. $0.002. https://tools.fmf-x402.workers.dev/tool/x402-validate-vs-discovery-checker?ref=github
- Symbol at Version Lookup — Looks up whether a function or export exists in an exact package version. $0.005. https://tools.fmf-x402.workers.dev/tool/symbol-at-version-lookup?ref=github
- npm Pre-Install Report — Reports what an npm package version will install and fetch, before you give it network or token access. $0.005. https://tools.fmf-x402.workers.dev/tool/npm-pre-install-report?ref=github
- Order Export Reconciler — Reconciles two order or sales exports and shows the mismatches. $0.001. https://tools.fmf-x402.workers.dev/tool/order-export-reconciler?ref=github
- Honest Price Checker — Checks whether a sale price, was-price, and in-stock flag are honest. $0.002. https://tools.fmf-x402.workers.dev/tool/honest-price-was-price-checker?ref=github
- ETag Contract Tester — Checks whether ETag / If-None-Match caching behaves as the docs say. $0.002. https://tools.fmf-x402.workers.dev/tool/etag-contract-tester?ref=github
- Public URL Vantage Report — Fetches a public URL from a second network and returns status and content hash, as evidence when an agent is blocked. $0.002. https://tools.fmf-x402.workers.dev/tool/public-url-vantage-report?ref=github
- Persistent Auditable Memory — Stores decision rules in durable memory so compaction cannot turn a guess into a fact. $0.002. https://tools.fmf-x402.workers.dev/tool/persistent-auditable-memory-compaction-constraint?ref=github
- Verifiable Handoff Receipt — Stores a receipt for a handoff between agents so a later reader can tell a side effect from a recomputed check. $0.002. https://tools.fmf-x402.workers.dev/tool/verifiable-handoff-receipt?ref=github
- Idempotency Replay Checker — Checks whether an idempotency key actually prevents a double charge on retry. $0.002. https://tools.fmf-x402.workers.dev/tool/idempotency-replay-double-charge-checker?ref=github
- Consent Revocation Checker — Checks whether a revoked permission is actually treated as revoked, not only on one machine. $0.002. https://tools.fmf-x402.workers.dev/tool/consent-revocation-checker?ref=github
- Source Freshness Checker — Checks whether a cited source is still fresh enough to quote. $0.001. https://tools.fmf-x402.workers.dev/tool/source-freshness-checker?ref=github
- Webhook Delivery Receipt — Records whether a webhook's side effect actually applied, not just that HTTP succeeded. $0.002. https://tools.fmf-x402.workers.dev/tool/webhook-delivery-receipt?ref=github
- Retry Budget Guard — Caps retry spend so unbounded retries cannot run up a bill. $0.002. https://tools.fmf-x402.workers.dev/tool/retry-budget-guard?ref=github

The directory lists the rest of the fleet. To install, add a server URL as a Streamable HTTP MCP connector in Cline, Cursor, Claude, or VS Code. There is nothing to run locally.

## Raise the default x402 spend cap

`@x402/fetch` (and the `@x402/core` client it wraps) caps each payment at **$1** of recognized USD-pegged assets by default. That default covers the live $0.001–$0.01 USDC-on-Base routes below. It does **not** cover [THE $1,000 FLEX](https://fmf-flex-crown.fmf-x402.workers.dev/?ref=github) at `https://fmf-flex-crown.fmf-x402.workers.dev/v1/flex`, which quotes **$1,000 USDC on Base**, or **$500** when the settled payer wallet currently holds the crown.

FMF Genesis is the 3-call founding boss on that board (4 calls dethrone it). A settled flex returns a numbered Proof-of-Flex trophy with dynamic ERC-721 metadata and a live SVG; if another caller later climbs past the rank you minted at, the artwork is marked `DEAD · OVERTAKEN`.

Copy this snippet, attach your own Base signer (never commit a private key), and raise the cap:

```ts
import { wrapFetchWithPayment, x402Client } from "@x402/fetch";
import { ExactEvmScheme } from "@x402/evm/exact/client";

const client = new x402Client()
  .register("eip155:8453", new ExactEvmScheme(signer))
  .setSpendControls({ maxAmountPerPayment: "$1000" }); // default is "$1"

const fetchWithPayment = wrapFetchWithPayment(fetch, client);
const res = await fetchWithPayment("https://fmf-flex-crown.fmf-x402.workers.dev/v1/flex");
```

Spend-control reference: [x402 Quickstart for Buyers](https://docs.x402.org/getting-started/quickstart-for-buyers). `tools/list` on our MCP endpoints is free; unpaid paid-routes return HTTP 402 and are not charged.

### Live paid routes

Prices checked live on 26 Nov 2026 (unpaid 402). Amounts are USDC on Base.

| Route | Price | URL |
|---|---|---|
| Control-plane snapshot | $0.01 | https://controlplane-x402.fmf-x402.workers.dev/v1/controlplane |
| Black Friday Deals Finder | $0.003 | https://black-friday-deals.fmf-x402.workers.dev/deals |
| Black Friday Deal Monitor | $0.01 | https://black-friday-deal-monitor.fmf-x402.workers.dev/watch |
| JSON Schema (pro) | $0.001 | https://mpp-tools.fmf-x402.workers.dev/mpp/pro/data/json-schema |
| Soft-404 / link-rot | $0.002 | https://soft-404-link-classifier.fmf-x402.workers.dev/v1/link-rot |
| Geocode (OpenWeather-compatible) | $0.001 | https://mpp-compat.fmf-x402.workers.dev/openweather/geocode |
| Domain age | $0.001 | https://mpp-domain.fmf-x402.workers.dev/domain/age |
| UUID | $0.001 | https://mpp-utils.fmf-x402.workers.dev/id/uuid |
| EVM selector | $0.001 | https://mpp-chain.fmf-x402.workers.dev/mpp/evm/selector |
| THE $1,000 FLEX | $1,000 ($500 if the settled payer holds the crown) | https://fmf-flex-crown.fmf-x402.workers.dev/v1/flex |

## Agent skills

One skill per parent tool, under [skills/](skills/). Install with the skills CLI, or add the origin to AgentCash:

| Skill | Call | Price | Install |
|---|---|---|---|
| [fmf-read](skills/fmf-read/SKILL.md) | `POST https://fmf-read.fmf-x402.workers.dev/mpp/read` | $0.003 | `npx skills add GeminiGeorge22/fmf-tools --skill fmf-read` |
| [fmf-pick](skills/fmf-pick/SKILL.md) | `GET https://agent-recipes.fmf-x402.workers.dev/mpp/pick` | $0.005 | `npx skills add GeminiGeorge22/fmf-tools --skill fmf-pick` |
| [fmf-domain-report](skills/fmf-domain-report/SKILL.md) | `POST https://mpp-domain.fmf-x402.workers.dev/mpp/domain/report` | $0.005 | `npx skills add GeminiGeorge22/fmf-tools --skill fmf-domain-report` |
| [fmf-package-check](skills/fmf-package-check/SKILL.md) | `POST https://npm-pre-install-report.fmf-x402.workers.dev/mpp/package/check` | $0.005 | `npx skills add GeminiGeorge22/fmf-tools --skill fmf-package-check` |

AgentCash:

```bash
npx agentcash add https://fmf-read.fmf-x402.workers.dev
npx agentcash add https://agent-recipes.fmf-x402.workers.dev
npx agentcash add https://mpp-domain.fmf-x402.workers.dev
npx agentcash add https://npm-pre-install-report.fmf-x402.workers.dev
```

Contact: fmf-tools@agentmail.to
