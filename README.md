# x402 Preflight

A machine-payable API that audits whether a public HTTPS endpoint exposes a valid unpaid x402 challenge.

## Live service

- Endpoint: `POST https://x402-preflight-mainnet.ipdoctor961051.workers.dev/v1/audit`
- Protocol: x402 v2
- Network: Base Mainnet
- Asset: USDC
- Price: 0.01 USDC per successful audit
- Health: `GET /health`
- Machine discovery: `GET /.well-known/x402`
- OpenAPI: `GET /openapi.json`
- Agent skill: `GET /skill.md`

## What it returns

The paid audit probes a public HTTPS target **without forwarding payment credentials** and reports:

- HTTP status
- whether a `PAYMENT-REQUIRED` header is present
- whether the challenge decodes as x402
- decoded challenge metadata
- response content type / redirect location
- bounded response preview
- audit timestamp

Invalid or private/local targets are rejected before payment.

## Unpaid discovery example

```bash
curl -i -X POST \
  https://x402-preflight-mainnet.ipdoctor961051.workers.dev/v1/audit \
  -H 'content-type: application/json' \
  -d '{"url":"https://x402.quicknode.com/base-sepolia","method":"POST","headers":{"content-type":"application/json"},"body":{"jsonrpc":"2.0","id":1,"method":"eth_blockNumber","params":[]}}'
```

A valid unpaid request returns HTTP `402 Payment Required` with a standard x402 v2 challenge.

## Agent discovery

This repository mirrors the live machine-readable metadata so crawlers and agents can discover the service without account creation or API keys:

- [SKILL.md](./SKILL.md)
- [openapi.json](./openapi.json)
- [x402-manifest.json](./x402-manifest.json)

## Status

Live seller running on Base Mainnet. Payments settle in Circle USDC through a gas-sponsored x402 facilitator.
