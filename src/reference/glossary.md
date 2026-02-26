# Glossary

This glossary defines key terms used throughout TreasureHunt.

## A

### Admin
The contract administrator with special privileges to modify system parameters.

### Answer Hash
The cryptographic hash (`keccak256`) of a puzzle answer, stored on-chain to verify answers without revealing them.

## B

### BNB
The native cryptocurrency of BNB Chain (formerly Binance Smart Chain).

### Blocks
The basic unit of time in blockchain. On BSC, approximately 3 seconds per block.

## C

### Creator
A user who creates puzzles by depositing BNB.

### Chain ID
A unique identifier for different blockchain networks (BSC Mainnet: 56, BSC Testnet: 97).

## D

### Deposit
The amount of BNB a puzzle creator locks when creating a puzzle.

### Duration
The number of blocks allocated for solving a puzzle before timeout.

## E

### ERC-721
The Ethereum standard for non-fungible tokens (NFTs).

## G

### Gas
The fee required to execute transactions on the blockchain.

## H

### Hash
A cryptographic fingerprint of data. TreasureHunt uses `keccak256` for answer hashing.

## L

### Lock
The action of a solver depositing BNB to attempt a puzzle, becoming the current solver.

## M

### Multiplier
A factor that determines how much a solver must deposit relative to the creator's deposit.

## N

### NFT (Non-Fungible Token)
A unique digital token that represents ownership of a specific asset. TreasureHunt has two types:
- Puzzle NFTs
- Victory NFTs

## P

### Prize Pool
The total BNB that can be won from solving a puzzle (creator deposit + solver deposit - taxes).

## R

### Reentrancy
A type of smart contract vulnerability. TreasureHunt uses ReentrancyGuard to prevent it.

### RPC (Remote Procedure Call)
A way to communicate with a blockchain node.

## S

### Solver
A user who attempts to solve a puzzle by locking it and submitting an answer.

### Status
The current state of a puzzle:
- Created: Available to be solved
- Locked: A solver is working on it
- Solved: Successfully answered
- Timeout: Solver ran out of time

## T

### Tax
The percentage fee collected by the protocol on deposits.

### Timeout Block
The block number by which a solver must submit their answer.

## V

### Victory NFT
A special NFT minted to a solver who successfully solves a puzzle.
