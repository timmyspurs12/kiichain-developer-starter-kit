# 🔗 KiiChain Developer Starter Kit

> A community-contributed developer resource for building on KiiChain — the EVM-compatible, Cosmos SDK-based Layer 1 blockchain purpose-built for stablecoins, RWAs, and emerging markets.

[![KiiChain](https://img.shields.io/badge/Network-KiiChain-blue)](https://kiichain.io)
[![Testnet](https://img.shields.io/badge/Testnet-Oro-gold)](https://explorer.kiichain.io)
[![EVM Compatible](https://img.shields.io/badge/EVM-Compatible-green)](https://docs.kiiglobal.io/docs/build-on-kiichain/developer-hub)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📖 Table of Contents

- [What is KiiChain?](#what-is-kiichain)
- [Why Build on KiiChain?](#why-build-on-kiichain)
- [Prerequisites](#prerequisites)
- [Testnet Oro — Network Details](#testnet-oro--network-details)
- [Wallet Setup](#wallet-setup)
- [Get Testnet Tokens (Faucet)](#get-testnet-tokens-faucet)
- [Environment Setup](#environment-setup)
- [Deploy Your First Smart Contract](#deploy-your-first-smart-contract)
- [Interact with the Chain](#interact-with-the-chain)
- [KiiChain Modules Overview](#kiichain-modules-overview)
- [SDKs](#sdks)
- [Useful Endpoints](#useful-endpoints)
- [Explorer & Tools](#explorer--tools)
- [Contributing](#contributing)
- [Resources](#resources)

---

## What is KiiChain?

KiiChain is a **Layer 1 AppChain** built with the [Cosmos SDK](https://docs.cosmos.network/) and [CometBFT](https://cometbft.com/) consensus. It serves as a unified on-chain **FX settlement layer** for stablecoins and Real World Assets (RWAs), targeting emerging markets.

Key properties:

- **100% EVM Compatible** — deploy Solidity contracts just like on Ethereum
- **Cosmos SDK Based** — supports CosmWasm smart contracts in Rust
- **High Performance** — up to 12,000 TPS with ~1 second block times
- **Interoperable** — connects with 100+ blockchain ecosystems via IBC
- **Custom Modules** — Oracle, Gas Abstraction, Token Factory, PayFi, and more
- **Dual Address System** — supports both `0x...` EVM addresses and `kii1...` Bech32 Cosmos addresses

---

## Why Build on KiiChain?

| Feature | KiiChain |
|---|---|
| EVM Compatibility | ✅ Full |
| CosmWasm Support | ✅ Yes |
| Block Time | ~1 second |
| TPS | Up to 12,000 |
| Gas Fees | Sub-cent (akii denom) |
| IBC Interop | ✅ 100+ chains |
| RWA Infrastructure | ✅ T-REX Protocol |
| PayFi Module | ✅ Built-in |

---

## Prerequisites

Before you start, ensure you have the following installed:

- [Node.js](https://nodejs.org/) v18+ and npm
- [Go](https://golang.org/dl/) v1.24.11+
- [Git](https://git-scm.com/)
- [Foundry](https://book.getfoundry.sh/getting-started/installation) (optional)
- A browser wallet: [MetaMask](https://metamask.io/) or [Keplr](https://www.keplr.app/)

Verify your Go version:
```bash
go version
# Expected: go version go1.24.x or higher
```

---

## Testnet Oro — Network Details

**Testnet Oro** is KiiChain's permanent public testnet with full smart contract and EVM support. All development, hackathon builds, and test deployments should target this network.

### Chain Info

| Property | Value |
|---|---|
| Chain Name | KiiChain Testnet Oro |
| Chain ID (Cosmos) | `oro_1336-1` |
| EVM Chain ID | `1336` |
| Token Denom | `akii` |
| Bech32 Prefix | `kii` |
| Total Supply | 1.8B KII |

### RPC Endpoints

**Sentry Node #1**

| Protocol | URL |
|---|---|
| RPC | `https://rpc.uno.sentry.testnet.v3.kiivalidator.com` |
| REST (LCD) | `https://lcd.uno.sentry.testnet.v3.kiivalidator.com` |
| gRPC | `grpc.uno.sentry.testnet.v3.kiivalidator.com:443` |
| JSON-RPC (EVM) | `https://json-rpc.uno.sentry.testnet.v3.kiivalidator.com` |
| Peer | `5b6aa55124c0fd28e47d7da091a69973964a9fe1@uno.sentry.testnet.v3.kiivalidator.com:26656` |

**Sentry Node #2**

| Protocol | URL |
|---|---|
| RPC | `https://rpc.dos.sentry.testnet.v3.kiivalidator.com` |
| REST (LCD) | `https://lcd.dos.sentry.testnet.v3.kiivalidator.com` |
| gRPC | `grpc.dos.sentry.testnet.v3.kiivalidator.com:443` |
| JSON-RPC (EVM) | `https://json-rpc.dos.sentry.testnet.v3.kiivalidator.com` |
| Peer | `5e6b283c8879e8d1b0866bda20949f9886aff967@dos.sentry.testnet.v3.kiivalidator.com:26656` |

---

## Wallet Setup

### MetaMask (EVM)

1. Open MetaMask → **Settings** → **Networks** → **Add Network**
2. Fill in:
```
Network Name:    KiiChain Testnet Oro
RPC URL:         https://json-rpc.uno.sentry.testnet.v3.kiivalidator.com
Chain ID:        1336
Currency Symbol: KII
Explorer URL:    https://explorer.kiichain.io
```

3. Click **Save** and switch to the new network.

### Keplr (Cosmos)

1. Install [Keplr](https://www.keplr.app/) browser extension.
2. Open Keplr → **Add Chain** → fill in:
```
Chain ID:        oro_1336-1
Chain Name:      KiiChain Testnet Oro
RPC Endpoint:    https://rpc.uno.sentry.testnet.v3.kiivalidator.com
REST Endpoint:   https://lcd.uno.sentry.testnet.v3.kiivalidator.com
Denom:           akii
Bech32 Prefix:   kii
```

> **Tip:** Your EVM address (`0x...`) and Cosmos address (`kii1...`) are two representations of the same keypair — KiiChain mirrors both automatically.

---

## Get Testnet Tokens (Faucet)

You need testnet KII (`akii`) to pay for gas. Two methods:

**Option 1 — Explorer Faucet (easiest):**

1. Go to [https://explorer.kiichain.io/faucet](https://explorer.kiichain.io/faucet)
2. Paste your wallet address and request tokens.

**Option 2 — Discord Faucet:**

1. Join [KiiChain Discord](https://discord.com/invite/kiichain)
2. Navigate to the `#faucet` channel
3. Use the faucet bot command with your address

---

## Environment Setup

### Install kiichaind (Node Binary)
```bash
git clone https://github.com/KiiChain/kiichain
cd kiichain
make install
export PATH="$HOME/go/bin:$PATH"
which kiichaind
kiichaind version
```

**Troubleshooting:**

| Error | Fix |
|---|---|
| `Minimum Go version 1.24 required` | Upgrade Go to 1.24.11+ |
| `command not found: kiichaind` | Ensure `$HOME/go/bin` is in your `$PATH` |
| Gas price error | `sed -i.bak -e '/minimum-gas-prices =/ s^= .*^= "1000000000akii"^' ~/.kiichain/config/app.toml` |

---

### Hardhat Setup
```bash
mkdir my-kiichain-dapp && cd my-kiichain-dapp
npm init -y
npm install --save-dev hardhat @nomicfoundation/hardhat-toolbox dotenv
npx hardhat init
```

Update `hardhat.config.js`:
```js
require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config();

module.exports = {
  solidity: "0.8.24",
  networks: {
    kiichain_testnet: {
      url: "https://json-rpc.uno.sentry.testnet.v3.kiivalidator.com",
      chainId: 1336,
      accounts: [process.env.PRIVATE_KEY],
    },
  },
};
```

Create `.env` (never commit this file):
```
PRIVATE_KEY=your_wallet_private_key_here
```

---

### Foundry Setup
```bash
curl -L https://foundry.paradigm.xyz | bash
foundryup
forge init my-kiichain-project
cd my-kiichain-project
```

Add to `foundry.toml`:
```toml
[rpc_endpoints]
kiichain_testnet = "https://json-rpc.uno.sentry.testnet.v3.kiivalidator.com"
```

---

## Deploy Your First Smart Contract

### Sample Contract — `HelloKii.sol`
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract HelloKii {
    string public message;

    constructor(string memory _message) {
        message = _message;
    }

    function setMessage(string memory _newMessage) public {
        message = _newMessage;
    }

    function getMessage() public view returns (string memory) {
        return message;
    }
}
```

### Deploy with Hardhat
```js
const { ethers } = require("hardhat");

async function main() {
  const HelloKii = await ethers.getContractFactory("HelloKii");
  const contract = await HelloKii.deploy("Hello from KiiChain!");
  await contract.waitForDeployment();
  console.log("HelloKii deployed to:", await contract.getAddress());
}

main().catch((err) => {
  console.error(err);
  process.exit(1);
});
```
```bash
npx hardhat run scripts/deploy.js --network kiichain_testnet
```

### Deploy with Foundry
```bash
forge create \
  --rpc-url https://json-rpc.uno.sentry.testnet.v3.kiivalidator.com \
  --private-key $PRIVATE_KEY \
  src/HelloKii.sol:HelloKii \
  --constructor-args "Hello from KiiChain!"
```

---

## Interact with the Chain

### Using ethers.js
```js
const { ethers } = require("ethers");

const provider = new ethers.JsonRpcProvider(
  "https://json-rpc.uno.sentry.testnet.v3.kiivalidator.com"
);

async function main() {
  const block = await provider.getBlockNumber();
  console.log("Latest block:", block);

  const address = "0xYourAddressHere";
  const balance = await provider.getBalance(address);
  console.log("Balance:", ethers.formatEther(balance), "KII");
}

main();
```

### Using CosmJS
```bash
npm install @cosmjs/stargate @cosmjs/proto-signing
```
```js
const { StargateClient } = require("@cosmjs/stargate");

async function main() {
  const client = await StargateClient.connect(
    "https://rpc.uno.sentry.testnet.v3.kiivalidator.com"
  );
  const balance = await client.getAllBalances("kii1youraddresshere");
  console.log("Balances:", balance);
  const chainId = await client.getChainId();
  console.log("Chain ID:", chainId);
}

main();
```

---

## KiiChain Modules Overview

| Module | Description |
|---|---|
| **Oracle** | On-chain price feeds for FX and asset pairs |
| **Token Factory** | Permissionless token creation without a smart contract |
| **Gas Abstraction** | Pay gas fees in tokens other than KII |
| **Utility Rewards** | Incentive system for ecosystem participants |
| **PayFi Module** | Gas-optimized payment system for merchants with Paymaster support |
| **RWA Protocol** | T-REX standard for compliant RWA tokenization with on-chain KYC/KYB |

---

## SDKs

| SDK | Language | Docs |
|---|---|---|
| KiiChain JS/TS SDK | JavaScript / TypeScript | [View Docs](https://docs.kiiglobal.io/docs/build-on-kiichain/developer-tools/js-ts-sdk) |
| KiiChain Rust SDK | Rust | [View Docs](https://docs.kiiglobal.io/docs/build-on-kiichain/developer-tools/rust-sdk) |

---

## Useful Endpoints

| Type | URL |
|---|---|
| EVM JSON-RPC | `https://json-rpc.uno.sentry.testnet.v3.kiivalidator.com` |
| Cosmos RPC | `https://rpc.uno.sentry.testnet.v3.kiivalidator.com` |
| REST / LCD | `https://lcd.uno.sentry.testnet.v3.kiivalidator.com` |
| gRPC | `grpc.uno.sentry.testnet.v3.kiivalidator.com:443` |

---

## Explorer & Tools

| Tool | URL |
|---|---|
| Testnet Explorer | [https://explorer.kiichain.io](https://explorer.kiichain.io) |
| Faucet | [https://explorer.kiichain.io/faucet](https://explorer.kiichain.io/faucet) |
| Official Docs | [https://docs.kiiglobal.io](https://docs.kiiglobal.io) |
| GitHub | [https://github.com/KiiChain](https://github.com/KiiChain) |
| Discord | [https://discord.com/invite/kiichain](https://discord.com/invite/kiichain) |

---

## Contributing

1. Fork this repo
2. Create a branch: `git checkout -b feature/your-improvement`
3. Commit: `git commit -m "Add: your description"`
4. Push and open a Pull Request

---

## Resources

- [KiiChain Official Docs](https://docs.kiiglobal.io)
- [KiiChain GitHub](https://github.com/KiiChain/kiichain)
- [Testnet Oro Info](https://docs.kiiglobal.io/docs/build-on-kiichain/testnet-oro)
- [Smart Contract Deployment Guide](https://docs.kiiglobal.io/docs/build-on-kiichain/developer-tools/deploy-a-smart-contract)
- [Deploy a dApp](https://docs.kiiglobal.io/docs/build-on-kiichain/developer-tools/deploy-a-dapp)
- [RWA Protocol](https://docs.kiiglobal.io/docs/build-on-kiichain/developer-tools/rwa-protocol)
- [Cosmos SDK Docs](https://docs.cosmos.network/)
- [KiiChain Discord](https://discord.com/invite/kiichain)

---

> **Disclaimer:** This is a community-contributed resource, not official KiiChain documentation. Always refer to (https://docs.kiiglobal.io) for the most authoritative and up-to-date information.

---

*Built with ❤️ for the KiiChain ecosystem. Contributions welcome!*
