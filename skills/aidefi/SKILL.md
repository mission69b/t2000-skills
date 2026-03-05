---
name: aidefi
description: >
  Access Sui DeFi yields, prices, and swap data from Aidefi aggregator.
  Use when user asks about:
  - DeFi yields on Sui
  - Best yield for SUI/USDC/etc
  - Swap estimates
  - Sui TVL
  - Protocol TVL (Navi, Suilend, Cetus, Turbos, Bluefin)
triggers:
  - "aidefi"
  - "defi yields"
  - "sui yields"
  - "swap estimate"
  - "best yield"
  - "sui tvl"
license: MIT
metadata:
  author: Aida
  version: "1.0"
  requires: t2000 CLI
---

# Aidefi - Sui DeFi Aggregator

Aidefi aggregates yields and data from 5 Sui DeFi protocols: Navi, Suilend, Cetus, Turbos, Bluefin.

## API

Base URL: `https://revised-come-final-metadata.trycloudflare.com`

Or use local: `http://localhost:3002`

## Commands

### Get Token Prices
```bash
curl -s https://revised-come-final-metadata.trycloudflare.com/api/prices
```

Example output:
```json
{"success":true,"data":{"SUI":0.96,"BTC":71000,"ETH":2080,"SOL":89,"USDC":1}}
```

### Get Best Yield for Asset
```bash
curl -s https://revised-come-final-metadata.trycloudflare.com/api/yields/best/SUI
```

Example output:
```json
{"success":true,"data":{"protocol":"navi","asset":"SUI","apy":0.05,"TVL":141000000}}
```

### Get All Yields
```bash
curl -s https://revised-come-final-metadata.trycloudflare.com/api/yields
```

### Get Market Overview (includes TVL)
```bash
curl -s https://revised-come-final-metadata.trycloudflare.com/api/market
```

Example output:
```json
{
  "success":true,
  "data":{
    "prices":{"SUI":0.96,"BTC":71000},
    "protocolTVL":{"navi":141000000,"suilend":170000000},
    "totalTVL":386000000
  }
}
```

### Get Swap Quote
```bash
curl -s -X POST https://revised-come-final-metadata.trycloudflare.com/api/swap \
  -H "Content-Type: application/json" \
  -d '{"from":"SUI","to":"USDC","amount":100}'
```

## Protocols Supported

- **Navi** - Lending (5% APY on SUI)
- **Suilend** - Lending (4% APY on SUI)
- **Cetus** - DEX
- **Turbos** - DEX
- **Bluefin** - Perpetuals

## Example Usage

When user asks "What's the best yield on SUI?":
1. Call `/api/yields/best/SUI`
2. Return protocol name and APY percentage
3. Optionally explain the protocol

## Error Handling

If API returns error, try the local endpoint:
```
http://localhost:3002/api/yields/best/SUI
```

If both fail, respond with "Unable to fetch yields - try again later"
