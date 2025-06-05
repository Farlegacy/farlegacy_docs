# About The Game

## Project Architecture

### Component Overview

* **Frontend**: Next.js + React + TailwindCSS
* **Backend / API Layer**: Node.js + tRPC (type-safe API)
* **Blockchain**: Base (L2 on Ethereum), Solidity
* **Storage**: IPFS (art, metadata), custom cache for match replays
* **Integrations**: Farcaster (via custom casts), Farcaster ID
* **Gasless UX**: Account abstraction (ERC-4337, Bundler + Paymaster)

***

## Frontend

### Stack and Features

The frontend is built using **Next.js**, **React**, and **TailwindCSS** for rapid and modular UI development. The app functions as a full SPA, allowing instant transitions between views (lobby, battle, collection, etc.).

#### Technologies:

* **React** — declarative UI with component-driven architecture
* **Next.js (App Router)** — supports SSR for SEO and routing
* **tRPC** — type-safe API communication between frontend and Node.js
* **Ethers.js** — blockchain interaction library
* **Wagmi + RainbowKit** — wallet integration and management
* **Zustand** — lightweight state management for client-side storage

***

## Game Access (NFT Gate)

### NFT-Based Access

Access to the game is restricted to holders of a specific NFT “Player Passport.” When a wallet is connected, the system checks whether the address owns a valid NFT.

#### Standard Used:

* **ERC-721** — for NFT-based player identification
* **Batch-check** (via multicall) supported during login
* Access managed by custom smart contract PlayerPass.sol

#### Process:

1. User connects their wallet.
2. The DApp calls balanceOf() on the PlayerPass contract.
3. Upon successful validation, the UI is unlocked and an on-chain player profile is created.

***

## On-Chain Logic and Account Abstraction

### Standards and Approach

All core gameplay actions — from match initiation to move submission — are **recorded on-chain**. This differentiates FarLegacy from typical Web3 games, which often rely on off-chain logic with occasional sync to the blockchain.

#### Standards Used:

* **ERC-4337**: Account Abstraction
* **Smart Accounts**: custom contracts replacing EOAs
* **Bundler & Paymaster**: enabling gasless transactions for users

***

## On-Chain Gameplay

### **How Data is Stored**

Each match is recorded in the smart contract: match ID, participants, moves, and result. The system uses:

* **Event Logging** (GameStarted, MoveMade, GameEnded)
* **IPFS Integration** for storing visual replays
* A **Replay Server** renders the match based on the event sequence

### Sample Contract:&#x20;

```solidity
event GameStarted(uint256 matchId, address player1, address player2);
event MoveMade(uint256 matchId, address player, bytes moveData);
event GameEnded(uint256 matchId, address winner);
```
