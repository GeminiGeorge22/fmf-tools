# FMF Tools

**FMF Tools** is a set of pay-per-call MCP servers for agents (Streamable HTTP). `tools/list` is free. Paid tools settle with MPP on Tempo or x402 on Base (USDC). No account and no API key. Bad input is refused and is not charged.

Logo (400×400): [logo-400.png](logo-400.png)

## Install in Cline, Claude, Cursor, or VS Code

Each server is a remote Streamable HTTP MCP endpoint. There is nothing to run locally.

Cline / Claude Desktop / Cursor: add a custom MCP connector with the server URL. Claude Code:

```bash
claude mcp add --transport http mtg-sim https://mtg-sim.fmf-x402.workers.dev/mcp
```

Or drop the matching block from `.mcp.json` into your client config.

## Servers

| Name | What it does | MCP URL | Docs |
|---|---|---|---|
| FMF Tools Doc Tools | PDF, Office, audio, OCR and text tools | `https://mpp-docs.fmf-x402.workers.dev/mcp` | [docs](https://mpp-docs.fmf-x402.workers.dev/docs) |
| FMF Tools Utilities | Tempo chain helpers, QR, DNS, email, IP, math | `https://mpp-tools.fmf-x402.workers.dev/mcp` | [docs](https://mpp-tools.fmf-x402.workers.dev/docs) |
| FMF Tools AI | Chat, translation, embeddings, rerank | `https://mpp-ai.fmf-x402.workers.dev/mcp` | [docs](https://mpp-ai.fmf-x402.workers.dev/docs) |
| FMF Tools Web & Data | Scrape, SEC filings, weather, FX | `https://mpp-agent-data.fmf-x402.workers.dev/mcp` | [docs](https://mpp-agent-data.fmf-x402.workers.dev/docs) |
| FMF Tools Research | Papers, FDA, trials, LEI | `https://mpp-research.fmf-x402.workers.dev/mcp` | [docs](https://mpp-research.fmf-x402.workers.dev/docs) |
| FMF Tools Browser | Screenshots, JS render, page-to-PDF | `https://mpp-browser.fmf-x402.workers.dev/mcp` | [docs](https://mpp-browser.fmf-x402.workers.dev/docs) |
| FMF Tools EVM Decoder | Calldata and logs, any chain, no RPC | `https://mpp-chain.fmf-x402.workers.dev/mcp` | [docs](https://mpp-chain.fmf-x402.workers.dev/docs) |
| FMF Tools STT | Deepgram-compatible /v1/listen | `https://mpp-stt.fmf-x402.workers.dev/mcp` | [docs](https://mpp-stt.fmf-x402.workers.dev/docs) |
| FMF Tools Control-plane | Who-controls-this-contract snapshots | `https://controlplane-x402.fmf-x402.workers.dev/mcp` | [docs](https://controlplane-x402.fmf-x402.workers.dev/docs) |
| FMF Tools Compat APIs | OpenWeather-, Mapbox- and EDGAR-compatible routes | `https://mpp-compat.fmf-x402.workers.dev/mcp` | [docs](https://mpp-compat.fmf-x402.workers.dev/docs) |
| FMF Tools Domain Checks | RDAP WHOIS, domain age, HTTP status, headers, SPF/DMARC | `https://mpp-domain.fmf-x402.workers.dev/mcp` | [docs](https://mpp-domain.fmf-x402.workers.dev/docs) |
| FMF Tools Dev Utils | IBAN, JWT, hashes, cron, RRULE, CSV | `https://mpp-utils.fmf-x402.workers.dev/mcp` | [docs](https://mpp-utils.fmf-x402.workers.dev/docs) |
| FMF Tools Crypto Tax | Gains, Form 8949, Schedule 3, tax-loss harvest | `https://mpp-cryptotax.fmf-x402.workers.dev/mcp` | [docs](https://mpp-cryptotax.fmf-x402.workers.dev/docs) |
| FMF Tools Business Docs | Invoice/receipt PDFs, payment URIs, phone, barcodes | `https://mpp-biz.fmf-x402.workers.dev/mcp` | [docs](https://mpp-biz.fmf-x402.workers.dev/docs) |
| MTG Sim | Magic: The Gathering goldfish and draw odds, free deck check | `https://mtg-sim.fmf-x402.workers.dev/mcp` | [docs](https://mtg-sim.fmf-x402.workers.dev/docs) · [repo](https://github.com/GeminiGeorge22/mtg-sim) |
| Pokémon TCG Sim | Goldfish, prize and draw odds, free Standard/Expanded deck check | `https://pokemon-tcg-sim.fmf-x402.workers.dev/mcp` | [docs](https://pokemon-tcg-sim.fmf-x402.workers.dev/docs) · [repo](https://github.com/GeminiGeorge22/pokemon-tcg-sim) |
| Yu-Gi-Oh Sim | Goldfish, combo and hand-trap odds, free TCG/OCG/GOAT deck check | `https://yugioh-sim.fmf-x402.workers.dev/mcp` | [docs](https://yugioh-sim.fmf-x402.workers.dev/docs) · [repo](https://github.com/GeminiGeorge22/yugioh-sim) |
| Lorcana Sim | Goldfish, ink and draw sims, free Core/Infinity deck check | `https://lorcana-sim.fmf-x402.workers.dev/mcp` | [docs](https://lorcana-sim.fmf-x402.workers.dev/docs) · [repo](https://github.com/GeminiGeorge22/lorcana-sim) |
| One Piece Sim | Goldfish, DON!! and Life odds, free Leader/50-card deck check | `https://onepiece-sim.fmf-x402.workers.dev/mcp` | [docs](https://onepiece-sim.fmf-x402.workers.dev/docs) · [repo](https://github.com/GeminiGeorge22/onepiece-sim) |
| Hearthstone Sim | Mulligan odds, curve goldfish, draw odds, free deck check | `https://hearthstone-sim.fmf-x402.workers.dev/mcp` | [docs](https://hearthstone-sim.fmf-x402.workers.dev/docs) · [repo](https://github.com/GeminiGeorge22/hearthstone-sim) |
| Chess Sim | Forced-mate finder, best move, free opening names and position check | `https://chess-sim.fmf-x402.workers.dev/mcp` | [docs](https://chess-sim.fmf-x402.workers.dev/docs) · [repo](https://github.com/GeminiGeorge22/chess-sim) |
| Dota 2 Sim | Right-click duel sim, build stats, EHP and DPS calculator | `https://dota2-sim.fmf-x402.workers.dev/mcp` | [docs](https://dota2-sim.fmf-x402.workers.dev/docs) · [repo](https://github.com/GeminiGeorge22/dota2-sim) |
| CS2 Sim | CS2 economy simulator: loss bonus, buy or eco, half simulation | `https://cs2-sim.fmf-x402.workers.dev/mcp` | [docs](https://cs2-sim.fmf-x402.workers.dev/docs) · [repo](https://github.com/GeminiGeorge22/cs2-sim) |

Contact: fmf-tools@agentmail.to
