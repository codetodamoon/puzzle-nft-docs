# Architecture

This document provides an overview of the TreasureHunt system architecture.

## System Overview

TreasureHunt follows a standard Web3 dApp architecture:

```
┌─────────────────────────────────────────────────────────────┐
│                        Frontend                              │
│  (React + Vite + Tailwind CSS + ethers.js)                 │
└─────────────────────┬───────────────────────────────────────┘
                      │ JSON-RPC
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                    Smart Contracts                           │
│  (TreasureHunt.sol - Core Logic)                            │
│  (ERC-721 - NFT Standard)                                   │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                    Blockchain Network                        │
│  (BSC / opBNB / Ethereum)                                  │
└─────────────────────────────────────────────────────────────┘
```

## Component Details

### Smart Contracts

#### TreasureHunt.sol
The main contract containing all puzzle logic:
- Puzzle creation and management
- Locking and solving mechanisms
- NFT minting (both puzzle and victory NFTs)
- Fee management
- Access control

#### ERC-721 Implementation
Uses OpenZeppelin's ERC-721URIStorage for:
- Puzzle NFTs (tokenId = riddleId)
- Victory NFTs (tokenId = 1,000,000,000 + riddleId)

### Frontend

Built with modern web technologies:
- **React**: UI framework
- **Vite**: Build tool
- **Tailwind CSS**: Styling
- **ethers.js**: Blockchain interaction
- **React Router**: Navigation

### Data Flow

1. **User Action** → Frontend validates input
2. **Transaction** → Signed by user's wallet
3. **Smart Contract** → Validates and executes logic
4. **State Change** → Updated on blockchain
5. **Event Emission** → Frontend listens and updates UI

## Design Decisions

### Two-Step Solving Process

The puzzle-solving process is split into two transactions:

1. `lockRiddle()` - Become the current solver
2. `submitAnswer()` - Attempt to solve

This prevents front-running and gives solvers time to work on the puzzle.

### Block-Based Timeout

Timeouts are measured in blocks rather than timestamps because:
- More predictable on blockchain
- Cannot be manipulated by miners
- Directly verifiable on-chain

### NFT Token ID Scheme

- Puzzle NFTs: 0, 1, 2, ...
- Victory NFTs: 1,000,000,000, 1,000,000,001, ...

This separation prevents ID collisions and makes it easy to distinguish between puzzle and victory NFTs.

### Answer Hashing

Answers are hashed using `keccak256` before storage:
- Answer is never stored in plaintext
- Only the solver who knows the answer can prove it
- The hash serves as commitment

## Security Considerations

1. **Reentrancy Guard**: All state-changing functions use ReentrancyGuard
2. **Access Control**: Only authorized addresses can perform certain actions
3. **Input Validation**: All inputs are validated in the contract
4. **Safe Math**: Using Solidity 0.8+ built-in overflow checks

## Upgradability

The current version does not use proxy patterns. Future versions may implement:
- UUPS proxy pattern
- Diamond standard for modular upgrades
