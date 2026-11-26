---
name: fmf-domain-report
description: Reports whether a domain is healthy and what is wrong with it in one paid call, covering registration, DNS, email authentication (SPF, DMARC, DKIM), TLS expiry and HTTP security headers. Use when an agent is setting up or auditing a domain, email sending, or a site.
---

# fmf-domain-report: `POST /mpp/domain/report`

Origin: https://mpp-domain.fmf-x402.workers.dev. Price: $0.005 (5000 USDC base units) per call, paid by MPP (Tempo) or x402 (Base USDC). You need no account or API key.

## When to use it

- Your agent is setting up or auditing a domain, its email sending or its site, and wants one verdict with the reasons.
- You want registration, DNS, email authentication, certificate and header checks in a single call, with `flags` naming what is wrong.

## When not to use it

- You need one record. The free way is the standard CLI tools on your own machine: `dig`, `whois`, and `openssl s_client`.
- You need only a single lookup over HTTP. The cheaper one-step routes are on https://mpp-tools.fmf-x402.workers.dev (`/mpp/dns/lookup`, `/mpp/dns/email-auth`, `/mpp/domain/rdap`, `/mpp/ssl/cert`, `/mpp/http/headers`).

## The one call

Tempo Wallet (syntax from mpp.dev/tools/wallet.md):

```bash
tempo request -X POST \
  --json '{"domain":"example.com"}' \
  https://mpp-domain.fmf-x402.workers.dev/mpp/domain/report
```

AgentCash (syntax from the Merit-Systems/agentcash-skills README):

```bash
npx agentcash@latest fetch https://mpp-domain.fmf-x402.workers.dev/mpp/domain/report -m POST -b '{"domain":"example.com"}'
```

To check the price before paying: `npx agentcash@latest check https://mpp-domain.fmf-x402.workers.dev/mpp/domain/report`

Free sample (runs the built-in example and ignores your input, no charge):

```bash
curl -s -X POST 'https://mpp-domain.fmf-x402.workers.dev/mpp/domain/report?test=1' -H 'content-type: application/json' -d '{}'
```

Discover the route and price: `npx agentcash@latest discover https://mpp-domain.fmf-x402.workers.dev`

## What comes back

`registered, registrar, created, expires, days_to_expiry, nameservers, dns {a, aaaa, mx, txt, caa}, email {mx_ok, spf {record, verdict}, dmarc {policy, verdict}, dkim_selectors_found, grade}, tls {issuer, not_after, days_left}, http {status, final_url, security_headers_grade}, flags, sources, fetched_at`.

A field with no answer is `null`, and `field_reasons` gives the reason. IDN domains are accepted. Invalid input is refused and not charged.

## On a 402 when you have no wallet tool

The 402 is the price, not an error. Do not retry it unpaid in a loop. Either:

- Run the free sample (`?test=1`) to see the output shape, or
- Have a wallet set up. The setup lines below are copied from mpp.dev/tools/wallet.md. Paste one into your agent:
  - Tempo Wallet: `Read https://tempo.xyz/SKILL.md and set up tempo`
  - AgentCash: `Set up agentcash.dev/skill.md`
- Or tell your human that this call costs $0.005 (5000 USDC base units) and needs an MPP or x402 wallet.

Docs: https://mpp-domain.fmf-x402.workers.dev/docs · https://mpp-domain.fmf-x402.workers.dev/llms.txt · https://mpp-domain.fmf-x402.workers.dev/openapi.json

Operated by FMF Tools (fmf-tools@agentmail.to).
