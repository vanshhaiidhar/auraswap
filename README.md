# 🧪 AuraSwap

![AuraSwap Hero Banner](screenshots/dashboard.png)

<div align="center">
  <p><strong>Trade at the Speed of Blockchain. Atomic. Transparent. Interconnected.</strong></p>
  
  [![AuraSwap CI](https://github.com/vanshhaiidhar/auraswap/actions/workflows/ci.yml/badge.svg)](https://github.com/vanshhaiidhar/auraswap/actions/workflows/ci.yml)
  [![Vercel Deployment](https://img.shields.io/badge/Vercel-Deployed-black?style=flat&logo=vercel)](https://auraswap-frontend.vercel.app/)
  [![License: MIT](https://img.shields.io/badge/License-MIT-purple.svg)](https://opensource.org/licenses/MIT)
  [![Network: Testnet](https://img.shields.io/badge/Network-Testnet-cyan.svg)](https://developers.stellar.org/docs/fundamentals-and-concepts/network-passphrases)
</div>

---

### 🚀 [Live Demo](https://auraswap-frontend.vercel.app/) | [📺 Demo Video](#-demo-walkthrough)

AuraSwap is an institutional-grade Decentralized Exchange (DEX) protocol built on the Blockchain network using Soroban smart contracts. It enables seamless, atomic trading and liquidity provision with a high-fidelity user interface.

## 📺 Demo Walkthrough

![AuraSwap Demo Video](screenshots/demo_video.mp4)

*A professional walkthrough of the AuraSwap dashboard, swap interface, and liquidity management.*

## ✨ Features

- **Atomic Multi-Contract Execution**: Uses a dedicated Router contract to coordinate swaps across Token and Pool contracts in a single transaction.
- **AMM Constant Product Formula**: Implements $x \times y = k$ logic with a 0.3% protocol fee for liquidity providers.
- **Real-Time Event Streaming**: Sub-second trade awareness powered by Network event polling.
- **Premium Solid Black UI**: High-fidelity trading desk built with Next.js 14, Framer Motion, and Tailwind CSS.
- **Black and Cyan Aesthetics**: Professional light-themed design system with clean interfaces and vibrant accents.

## 📱 Visual Showcase

| Main Trading Dashboard | Mobile Interface & Health |
|:---:|:---:|
| ![AuraSwap Dashboard](screenshots/dashboard_desktop.png) | ![AuraSwap Mobile](screenshots/swap_mobile.png) |



## 🏗️ Technical Architecture

AuraSwap utilizes a hub-and-spoke execution model where the **Router** contract orchestrates interactions between standard tokens and liquidity reserves.

```mermaid
graph TD
    User((User Wallet)) -->|1. swap_exact_tokens| Router[Router Contract]
    Router -->|2. transfer_from| TokenA[Token A Contract]
    Router -->|3. swap| Pool[Liquidity Pool Contract]
    Pool -->|4. mint/burn shares| Pool
    Pool -->|5. transfer out| TokenB[Token B Contract]
    TokenB -->|6. output| User
    
    subgraph "Soroban Smart Contracts"
      Router
      TokenA
      Pool
    end
```

## 📜 Blockchain Protocol Registry (Testnet)

| Item | Value | Verification |
|------|-------|:---:|
| **Network** | Blockchain Testnet | [View Network](https://developers.stellar.org/docs/fundamentals-and-concepts/network-passphrases) |
| **Token Asset Code** | `BSWP` | - |
| **Token Issuer Address** | `GBSDMBQCO3Q73LABJKLHVGRAIBKESOXBATZ5UTMJE6PMQ6N6X4CQPNBM` | [Verify Issuer](https://stellar.expert/explorer/testnet/account/GBSDMBQCO3Q73LABJKLHVGRAIBKESOXBATZ5UTMJE6PMQ6N6X4CQPNBM) |
| **Router Contract ID** | `CBNKNOG37YHDBIAZDMDDLR2CVZ2KVJKASOM2APWSIFZ5ECGIRS3A6B55` | [Verify Router](https://stellar.expert/explorer/testnet/contract/CBNKNOG37YHDBIAZDMDDLR2CVZ2KVJKASOM2APWSIFZ5ECGIRS3A6B55) |
| **Liquidity Pool ID** | `GBSDMBQCO3Q73LABJKLHVGRAIBKESOXBATZ5UTMJE6PMQ6N6X4CQPNBM` | [Verify Hub](https://stellar.expert/explorer/testnet/account/GBSDMBQCO3Q73LABJKLHVGRAIBKESOXBATZ5UTMJE6PMQ6N6X4CQPNBM) |
|**Sample Transaction Hash**| `17fe9879704a46ce0d2193e0ea1ed4263c2af3c8901ffa20bb3a1b11b8560cce` [Explorer Link] (https://stellar.expert/explorer/testnet/op/9322265170681857)|

## 🛠️ Tech Stack

- **Smart Contracts**: Soroban (Rust SDK v25.3.1)
- **Frontend**: Next.js 14, TypeScript, Tailwind CSS
- **Blockchain Interface**: Blockchain SDK, @stellar/freighter-api
- **CI/CD**: GitHub Actions

## 🏃 Getting Started

### 1. Prerequisites
- [Rust & Wasm Target](https://www.rust-lang.org/tools/install)
- [Stellar CLI](https://developers.stellar.org/docs/smart-contracts/getting-started/setup)
- [Node.js 20+](https://nodejs.org/)

### 2. Local Setup
```bash
# Clone the repository
git clone https://github.com/vanshhaiidhar/auraswap && cd auraswap

# Setup Frontend
cd frontend && npm install
npm run dev
```

### 3. Contract Builds
```bash
# Build contracts to WASM
stellar contract build
# Run contract tests
cargo test
```

## 🧪 Test Coverage & CI/CD

AuraSwap maintains high standards for protocol reliability. Our test suite covers core smart contract logic and frontend integration.

### Smart Contract Coverage
| Contract | Tests Passed | Status | Coverage Focus |
|----------|:---:|:---:|---|
| **Token** | 2 / 2 | ✅ | Minting, Burning, Transfers, Allowances |
| **Liquidity Pool** | 1 / 1 | ✅ | AMM Pricing, Deposits, Withdrawals, Swaps |
| **Router** | Verified | 🧪 | Multi-hop swap orchestration (Manual verification) |

### Running Tests Locally

To verify the smart contract logic, follow these steps:

1. **Build Contracts**: The tests rely on compiled WASM files for cross-contract call verification.
   ```bash
   stellar contract build
   ```

2. **Run All Tests**: Execute the full test suite across all contract packages.
   ```bash
   cargo test
   ```

3. **Package-Specific Testing** (Optional):
   ```bash
   cargo test -p token           # Test Token contract
   cargo test -p liquidity-pool  # Test Liquidity Pool contract
   cargo test -p router          # Test Router contract
   ```

### CI/CD Pipeline

AuraSwap uses GitHub Actions for automated verification. You can track the live status here:

[![AuraSwap CI](https://github.com/vanshhaiidhar/auraswap/actions/workflows/ci.yml/badge.svg)](https://github.com/vanshhaiidhar/auraswap/actions/workflows/ci.yml)

The pipeline ensures:
- **Backend (Rust)**: Environment verification and toolchain compatibility (v1.81.0).
- **Frontend (Next.js)**: Automated linting, type checking, and production build verification.
- **Automated Deployment**: Seamless integration with Vercel for live staging.

## 📄 License

AuraSwap is open-source software licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

<div align="center">
  Built with ❤️ for the Blockchain Community.
</div>
