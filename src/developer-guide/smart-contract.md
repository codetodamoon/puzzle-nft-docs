# Smart Contract

This document describes the TreasureHunt smart contract architecture and core logic.

## Contract Overview

The main contract is `TreasureHunt.sol`, located in `contracts/`.

### Key Features

- Puzzle creation with BNB deposits
- Two-step solving process (lock → submit)
- Automatic NFT minting
- Block-based timeout mechanism
- Tax collection and withdrawal

## Contract Structure

### Contract Inheritance

```
TreasureHunt
├── ReentrancyGuard (from OpenZeppelin)
├── ERC721URIStorage (from OpenZeppelin)
└── Ownable (from OpenZeppelin)
```

### State Variables

```solidity
address public admin;              // System administrator
address public taxAccount;         // Tax collection address
uint256 public taxRate;            // Tax rate (per thousand)
uint256 public minDeposit;         // Minimum puzzle deposit
uint256 public maxMultiplier;     // Maximum multiplier
uint256 public defaultDuration;    // Default timeout duration

uint256 public riddleCounter;      // Total riddles created
uint256 public victoryCounter;     // Total victories minted

mapping(uint256 => Riddle) public riddles;      // Puzzle data
mapping(uint256 => SolveHistory[]) public history; // Solve attempts
mapping(address => uint256[]) public userCreatedRiddles; // User's puzzles
mapping(address => uint256[]) public userSolvedRiddles; // User's wins
```

## Puzzle Lifecycle

### 1. Creation (Created)

```
createRiddle(content, answer, multiplier, duration)
├── Validates inputs
├── Computes answerHash = keccak256(answer)
├── Stores Riddle struct
├── Mints Puzzle NFT (tokenId = riddleId)
├── Takes creation tax
└── Emits RiddleCreated event
```

### 2. Locking (Locked)

```
lockRiddle(riddleId)
├── Validates puzzle exists and is joinable
├── Accepts payment (deposit × multiplier)
├── Takes participation tax
├── Sets solver = msg.sender
├── Sets timeoutBlock = block.number + duration
└── Emits RiddleLocked event
```

### 3. Solving (Solved)

```
submitAnswer(riddleId, answer)
├── Validates caller is current solver
├── Checks timeout (block.number < timeoutBlock)
├── Verifies answerHash == keccak256(answer)
├── Calculates prize pool
├── Transfers prize to solver
├── Mints Victory NFT
├── Stores plaintext answer
└── Emits RiddleSolved event
```

### 4. Timeout

```
withdrawRiddle(riddleId)
├── Validates caller is creator
├── Checks timeout (block.number >= timeoutBlock)
├── Transfers prize pool to creator
└── Resets puzzle to Created state
```

## Data Structures

### Riddle

```solidity
struct Riddle {
    address creator;       // Puzzle creator
    uint256 deposit;      // Creator's deposit
    uint256 multiplier;   // Solver deposit multiplier
    uint256 duration;     // Timeout duration (blocks)
    uint256 timeoutBlock; // Timeout block number (0 = not locked)
    uint256 solverDeposit; // Solver's deposited amount
    address solver;       // Current solver (address(0) = not locked)
    bytes32 answerHash;  // Hash of the answer
    string riddleContent; // The puzzle prompt
    string answer;       // Plaintext answer (filled when solved)
    bool isActive;       // Whether puzzle is active
}
```

### VictoryMetadata

```solidity
struct VictoryMetadata {
    uint256 riddleId;       // Associated puzzle ID
    address riddleCreator;  // Puzzle creator
    uint256 createTime;     // Puzzle creation time
    string riddleContent;   // Puzzle prompt
    string answer;         // Correct answer
    address solver;        // Winner address
    uint256 solveTime;     // Solve timestamp
    uint256 duration;      // Time taken (blocks)
    uint256 reward;        // Prize won
}
```

## Security Mechanisms

### Reentrancy Protection

All state-changing functions use `nonReentrant` modifier from OpenZeppelin.

### Access Control

- `onlyAdmin`: System configuration
- `onlyCreator`: Puzzle management
- `onlySolver`: Answer submission

### Input Validation

- Minimum/maximum deposit amounts
- Multiplier limits
- Duration constraints
- Address validation

## Contract Size

The compiled contract should fit within the EVM bytecode size limit (24KB). If it approaches the limit, consider:
- Removing unused functions
- Using libraries for common operations
- Splitting into multiple contracts
