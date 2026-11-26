---
name: fmf-pick
description: Picks the live paid API endpoint to call for a plain-words need and returns up to 5 x402 or MPP endpoints, each with its price, rail, network, an input example and a live HTTP 402 check from the last 24 hours. Use when an agent with a wallet must choose which paid endpoint to call for a task.
---

# fmf-pick: `GET /mpp/pick`

Origin: https://agent-recipes.fmf-x402.workers.dev. Price: $0.005 (5000 USDC base units) per call, paid by MPP (Tempo) or x402 (Base USDC). You need no account or API key.

## When to use it

- Your agent has a wallet and a task ("transcribe audio", "search tweets") but no endpoint chosen.
- You want only endpoints that answered an unpaid request with a 402 in the last 24 hours, priced from that live 402.
- You want to filter by rail (`mpp`, `x402`, `any`) and `max_price` in USD.

## When not to use it

- You already know the endpoint. Call it directly; its own 402 states the price.
- You want to browse. PayAI's discovery list (facilitator.payai.network/discovery/resources) and mpp.dev/api/services are free.

## The one call

Tempo Wallet (syntax from mpp.dev/tools/wallet.md):

```bash
tempo request 'https://agent-recipes.fmf-x402.workers.dev/mpp/pick?need=transcribe%20audio&rail=any'
```

AgentCash (syntax from the Merit-Systems/agentcash-skills README):

```bash
npx agentcash@latest fetch 'https://agent-recipes.fmf-x402.workers.dev/mpp/pick?need=transcribe%20audio&rail=any'
```

To check the price before paying: `npx agentcash@latest check https://agent-recipes.fmf-x402.workers.dev/mpp/pick`

Free sample (runs the built-in example and ignores your input, no charge):

```bash
curl -s 'https://agent-recipes.fmf-x402.workers.dev/mpp/pick?test=1'
```

Discover the route and price: `npx agentcash@latest discover https://agent-recipes.fmf-x402.workers.dev`

## What comes back

`catalog_asof, catalog_age_hours, sources, missing, picks` (up to 5). Each pick has `url, method, price_usd, network, rail, description, input_example, wallets_30d, calls_30d, calls_per_wallet, last_called_at, live_402_checked_at, price_matches_listing, own, flags`.

`wallets_30d`, `calls_30d`, `calls_per_wallet` and `last_called_at` are `missing`, and `missing.tried` lists the sources tried: the one catalog that has these counts may not be republished. FMF Tools endpoints appear only when they match, always with `own: true`. When nothing matches, you get `no_coverage` and are not charged.

## On a 402 when you have no wallet tool

The 402 is the price, not an error. Do not retry it unpaid in a loop. Either:

- Run the free sample (`?test=1`) to see the output shape, or
- Have a wallet set up. The setup lines below are copied from mpp.dev/tools/wallet.md. Paste one into your agent:
  - Tempo Wallet: `Read https://tempo.xyz/SKILL.md and set up tempo`
  - AgentCash: `Set up agentcash.dev/skill.md`
- Or tell your human that this call costs $0.005 (5000 USDC base units) and needs an MPP or x402 wallet.

Docs: https://agent-recipes.fmf-x402.workers.dev/docs · https://agent-recipes.fmf-x402.workers.dev/llms.txt · https://agent-recipes.fmf-x402.workers.dev/openapi.json

Operated by FMF Tools (fmf-tools@agentmail.to).
