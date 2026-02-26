# Overview

## What is TreasureHunt?

TreasureHunt is a decentralized puzzle marketplace built on EVM-compatible blockchain networks. It allows users to create cryptographic puzzles with BNB prizes, and other users can solve these puzzles to win the prize pool and earn unique Victory NFTs.

## Core Concept

The platform operates on a simple yet engaging premise:

1. **Puzzle Creators** deposit BNB to create puzzles with riddles and set multipliers
2. **Solvers** lock puzzles by depositing BNB (deposit × multiplier), then attempt to solve the riddle
3. **Successful solvers** win the entire prize pool and receive a Victory NFT
4. **Timeout scenarios** allow creators to claim the solver's deposit

## Supported Networks

TreasureHunt is deployed on the following networks:

| Network | Chain ID | Status |
|---------|----------|--------|
| BSC Mainnet | 56 | Active |
| opBNB Mainnet | 204 | Active |
| BSC Testnet | 97 | Test |
| opBNB Testnet | 5611 | Test |

## Technology Stack

- **Blockchain**: EVM-compatible chains (BSC, opBNB, Ethereum)
- **Smart Contracts**: Solidity with Hardhat
- **NFT Standard**: ERC-721 (OpenZeppelin)
- **Frontend**: React + Vite + Tailwind CSS
- **Web3**: ethers.js

## Why Use TreasureHunt?

### For Puzzle Creators
- Earn BNB by creating engaging riddles
- Set custom difficulty through multipliers
- Control puzzle duration with block-based timeouts

### For Solvers
- Test your cryptographic skills
- Win BNB prizes by solving puzzles
- Collect unique Victory NFTs as achievements
- Track your PnL performance

### For Everyone
- Fully decentralized and transparent
- All transactions secured by smart contracts
- No middleman - peer-to-peer gameplay
- Unique NFT collectibles to show off
