# x402 Preflight

Machine-payable API that audits whether a public HTTPS endpoint exposes a valid unpaid x402 challenge.

- Base URL: https://x402-preflight-seller.ipdoctor961051.workers.dev
- Manifest: /.well-known/x402
- OpenAPI: /openapi.json
- Health: /health
- Payment: x402 v2, exact, Base Sepolia USDC
- Price: $0.001 per successful audit

## Tool

POST /v1/audit

Input JSON: url (required), method, headers, body.

The service validates input before payment. An unpaid valid request returns HTTP 402 with PAYMENT-REQUIRED.