---
name: fmf-package-check
description: Checks whether an npm or PyPI package is safe to install right now in one paid call, covering existence, typo-squatting, age, install scripts, deprecation, maintainer changes and OSV advisories. Use when a coding agent is about to install a dependency.
---

# fmf-package-check: `POST /mpp/package/check`

Origin: https://npm-pre-install-report.fmf-x402.workers.dev. Price: $0.005 (5000 USDC base units) per call, paid by MPP (Tempo) or x402 (Base USDC). You need no account or API key.

## When to use it

- A coding agent is about to run `npm install` or `pip install` on a name it was given or guessed.
- You want one verdict (`ok`, `caution` or `block`) with reasons: the name does not exist, it is a one-letter typo of a popular package, it was published in the last 7 days, it has install scripts, or it has a known advisory.

## When not to use it

- You only need the advisories for one version. The free way is the OSV API (`POST https://api.osv.dev/v1/query`), or `npm audit` and `npm view <name>` for npm.
- Your packages come from private registries or other ecosystems (crates, Go, Maven). Those are not covered.

## The one call

Tempo Wallet (syntax from mpp.dev/tools/wallet.md):

```bash
tempo request -X POST \
  --json '{"ecosystem":"npm","name":"ms","version":"2.1.3"}' \
  https://npm-pre-install-report.fmf-x402.workers.dev/mpp/package/check
```

AgentCash (syntax from the Merit-Systems/agentcash-skills README):

```bash
npx agentcash@latest fetch https://npm-pre-install-report.fmf-x402.workers.dev/mpp/package/check -m POST -b '{"ecosystem":"npm","name":"ms","version":"2.1.3"}'
```

To check the price before paying: `npx agentcash@latest check https://npm-pre-install-report.fmf-x402.workers.dev/mpp/package/check`

Free sample (runs the built-in example and ignores your input, no charge):

```bash
curl -s -X POST 'https://npm-pre-install-report.fmf-x402.workers.dev/mpp/package/check?test=1' -H 'content-type: application/json' -d '{}'
```

Discover the route and price: `npx agentcash@latest discover https://npm-pre-install-report.fmf-x402.workers.dev`

## What comes back

`exists, verdict (ok|caution|block), reasons, latest, published_at, age_days, weekly_downloads, maintainers_count, maintainer_changed_recently, has_install_scripts, deprecated, advisories [{id, severity, fixed_in}], typosquat_of, license, sources, fetched_at`.

`sources` carries the attribution for registry.npmjs.org, pypi.org, api.osv.dev and api.deps.dev. Invalid input or a registry outage is not charged.

## On a 402 when you have no wallet tool

The 402 is the price, not an error. Do not retry it unpaid in a loop. Either:

- Run the free sample (`?test=1`) to see the output shape, or
- Have a wallet set up. The setup lines below are copied from mpp.dev/tools/wallet.md. Paste one into your agent:
  - Tempo Wallet: `Read https://tempo.xyz/SKILL.md and set up tempo`
  - AgentCash: `Set up agentcash.dev/skill.md`
- Or tell your human that this call costs $0.005 (5000 USDC base units) and needs an MPP or x402 wallet.

Docs: https://npm-pre-install-report.fmf-x402.workers.dev/docs · https://npm-pre-install-report.fmf-x402.workers.dev/llms.txt · https://npm-pre-install-report.fmf-x402.workers.dev/openapi.json

Operated by FMF Tools (fmf-tools@agentmail.to).
