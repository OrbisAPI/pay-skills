---
name: marketplace
title: "Orbis API Marketplace"
description: "8,000+ APIs accessible via x402 USDC micropayments on Base and Solana mainnet. Covers AI/LLM inference, DeFi data, weather, geolocation, web scraping, image generation, and more — no API keys required, pay per request from any USDC wallet."
use_case: "Use for AI inference (LLMs, embeddings, image generation), DeFi and crypto market data, geolocation and IP intelligence, weather forecasts, web scraping, pizza ordering, fake/test data generation, and 8,000+ other APIs — all billable per-call with Solana or Base USDC."
category: developer-tools
service_url: https://orbisapi.com
openapi:
  path: openapi.json
---

Orbis is an x402-native API marketplace. Every endpoint behind `/proxy/{slug}/` returns a 402 Payment Required with dual payment options:

- **Base USDC** (`eip155:8453`) — standard EVM x402 flow via Coinbase CDP facilitator.
- **Solana USDC** (`solana`) — SPL token transfer, feePayer sponsored by the Orbis platform wallet so callers only need USDC (no SOL for gas).

Price per call is $0.005 USDC (5000 atomic units) for most endpoints. Browse the full catalog at [orbisapi.com](https://orbisapi.com) or via the [well-known discovery endpoint](https://orbisapi.com/.well-known/x402).

## Spend-aware usage

- Query the [Bazaar discovery API](https://orbisapi.com/api/bazaar/discover) to find the cheapest API for a given task before calling it.
- Reuse blockhashes — payment headers created within the `maxTimeoutSeconds` window are valid without re-fetching a blockhash.
- For Solana callers: the platform's feePayer wallet (`GX6SKV6NahzGAocGs1uiAjFATUsdeEqT4dsEjwU6UrUE`) co-signs and covers SOL transaction fees — your wallet only needs USDC.
- Use the `X-PAYMENT-RESPONSE` header on 200 responses to extract the on-chain transaction hash for receipts.
