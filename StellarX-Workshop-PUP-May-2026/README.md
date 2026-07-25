# PredictX PH

A community prediction market for the Philippines — create markets on PH elections, PBA games, PSE stocks, crypto prices, and more. Trade Yes/No shares using USDC and get paid when you're right.

## Problem

Filipinos love to make predictions — who will win the barangay elections, which PBA team takes the championship, where the PSE index closes, or whether BSP will cut rates. But existing options are limited: illegal jueteng, unregulated Facebook group bets, or international platforms with KYC requirements and no PH-specific markets.

56% of Filipino adults are unbanked (BSP 2023) — they can't access traditional betting or prediction platforms that require bank accounts or credit cards. PredictX PH solves this by building on Stellar: anyone with a Freighter wallet and an internet connection can create and trade prediction markets. No KYC, no bank account, no censorship. Low fees mean even small bets (₱10–₱100) are practical.

## How It Works

1. **Create a market** — Anyone creates a binary market on a PH topic. Examples: "Will BSP cut rates by 50bps in June?", "Will PSEi close above 7,500 this quarter?", "Will Ginebra win PBA Commissioner's Cup?". The creator sets a resolution date and a verifiable source (govt website, news article, official league site).
2. **Buy shares** — Users buy "Yes" or "No" shares using USDC. If the crowd thinks an event is 70% likely, "Yes" costs ₱0.70 and "No" costs ₱0.30. Users can trade out before resolution at the current market price.
3. **Resolve & claim** — The creator submits an on-chain resolution with a link to the outcome source. Winners claim their share of the payout pool. Losers' shares become worthless — that's how winners get paid.

## How It Uses Stellar

- **Soroban contracts** — Market creation, share tracking, and resolution logic live in a Rust Soroban contract. Each market is a contract instance, making markets trustless and transparent.
- **Classic assets (USDC)** — Users deposit and withdraw USDC via trustlines. In production, this could be a PHP-anchored stablecoin (via a Stellar anchor like Coins.ph) for a truly peso-denominated experience.
- **Freighter wallet** — Users sign transactions (deposit, buy shares, resolve, claim) directly from the browser. Self-custodial — no server stores user funds.
- **Horizon** — Balances and trustline status are read from Horizon. No database needed.
- **Stellar testnet** — All activity runs on testnet for the workshop. Mainnet deployment would use real USDC or PHP-pegged assets.

Why Stellar? Ultra-low fees (~0.00001 XLM per tx) make micro-bets (₱10–₱50) economically viable — impossible on Ethereum. Finality in 3–5 seconds means a smooth UX. Stellar's built-in asset support lets us plug into the existing Philippine Stellar ecosystem (Coins.ph, PesoX, etc.). Soroban gives us programmable contracts without the gas waste of EVM chains.

## Track

**Soroban Smart Contract** — StellarX Workshop PUP May 2026

## Tech Stack

- Framework: Next.js 16 + TypeScript + Tailwind CSS v4
- Stellar SDK: @stellar/stellar-sdk v15.1.0
- Freighter API: @stellar/freighter-api v6
- Contract: Rust + soroban-sdk 22
- Network: testnet
- Oracle: Market creator manually resolves (trust-based for demo)

## Setup & Run

```bash
git clone https://github.com/your-org/predictx
cd StellarX-Workshop-PUP-May-2026
cd web
npm install
# No environment variables needed for testnet defaults
npm run dev
```

Open http://localhost:3000, connect Freighter (Test Net), and fund with Friendbot.

To deploy the prediction market contract:

```bash
cargo test
./scripts/deploy.sh
# or .\scripts\deploy.ps1 on Windows
```

## Network Details

- Network: testnet
- RPC URL: https://soroban-testnet.stellar.org
- Horizon: https://horizon-testnet.stellar.org
- USDC issuer (testnet): GBBD47IF6LWK7P7MDEVSCWR7DPUWV3NY3DTQEVFL4NAT4AQH3ZLLFLA5
- Contract IDs: Dynamically deployed via deploy script

## Team

- [Your Name] — @yourgithub

## License

MIT
