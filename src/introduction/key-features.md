# Key Features

## Puzzle NFT System

### Puzzle NFTs

Every puzzle created on TreasureHunt is represented as an ERC-721 NFT. These NFTs:

- Are minted when a puzzle is created
- Have token IDs matching the riddle ID
- Store the puzzle metadata on-chain
- Remain in existence even after the puzzle is solved or destroyed

### Victory NFTs

When a puzzle is successfully solved, a Victory NFT is minted to the solver's address. Victory NFTs contain:

- **Riddle ID**: The associated puzzle ID
- **Creator**: Puzzle creator's address
- **Riddle Content**: The puzzle prompt
- **Answer**: The correct answer
- **Solver**: The winner's address
- **Solve Time**: When the puzzle was solved
- **Duration**: How long it took to solve (in blocks)
- **Reward**: The prize amount won

Victory NFT token IDs start from 1,000,000,000 to avoid conflicts with puzzle NFTs.

## PNL Tracking

The platform provides comprehensive profit and loss tracking:

### For Puzzle Creators

- **Total Created**: Number of puzzles created
- **Successful Solves**: How many were solved by others
- **Timeouts Won**: How many times solvers timed out
- **Total Earned**: Sum of all prizes won
- **Net PnL**: Total earnings minus total deposits

### For Solvers

- **Total Attempts**: Number of puzzles attempted
- **Successful Solves**: Number of puzzles solved
- **Failed Attempts**: Number of puzzles failed or timed out
- **Total Won**: Sum of all prizes won
- **Net PnL**: Total winnings minus total deposits

## Flexible Configuration

### For Creators

- **Deposit Amount**: Minimum 0.01 BNB
- **Multiplier**: 1x to 10x
- **Duration**: Customizable timeout in blocks (default: 1000 blocks)

### For Administrators

The system admin can configure:

- **Tax Rate**: Percentage taken from deposits
- **Tax Account**: Where collected taxes are sent
- **Minimum Deposit**: Lower bound for puzzle deposits
- **Maximum Multiplier**: Upper limit for multipliers
- **Default Duration**: Default timeout period

## Security Features

### On-Chain Answer Hashing

Answers are never stored in plaintext. Instead:

1. Creator provides plaintext answer when creating puzzle
2. System computes `keccak256(answer)`
3. Only the hash is stored on-chain
4. Answer is revealed only when solved

### Access Control

- Only puzzle creators can modify or withdraw from their puzzles
- Only the current solver can submit answers
- Only admins can modify system parameters

### Reentrancy Protection

All state-changing functions use OpenZeppelin's ReentrancyGuard to prevent reentrancy attacks.

### Timeout Mechanism

- Block-based timeouts are enforced on-chain
- Frontend provides additional timeout warnings
- No party can extend or bypass timeouts
