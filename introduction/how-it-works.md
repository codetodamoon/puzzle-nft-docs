# How It Works

## The TreasureHunt Lifecycle

Understanding how TreasureHunt works involves knowing the complete lifecycle of a puzzle from creation to resolution.

### 1. Puzzle Creation

When a user creates a puzzle, the following happens:

```
Creator Actions:
├── Deposits BNB (minimum 0.01 BNB)
├── Sets a multiplier (1-10x)
├── Provides riddle content
├── Provides answer (plaintext)
└── Sets duration in blocks

System Actions:
├── Computes keccak256 hash of answer
├── Stores hash on-chain (not the answer!)
├── Mints Puzzle NFT (tokenId = riddleId)
├── Deducts tax from deposit
└── Locks remaining deposit in contract
```

### 2. Puzzle Locking (Solving Attempt)

When a solver wants to attempt a puzzle:

```
Solver Actions:
├── Calls lockRiddle() with payment
└── Payment = deposit × multiplier

System Actions:
├── Accepts payment (minus tax)
├── Records solver address
├── Sets timeoutBlock = currentBlock + duration
├── Updates puzzle status to LOCKED
└── Solver becomes the current解题者
```

### 3. Answer Submission

The solver now has until `timeoutBlock` to submit an answer:

```
If Answer is CORRECT:
├── Solver receives full prize pool
├── Victory NFT is minted (tokenId = 1,000,000,000 + riddleId)
├── Answer is stored on-chain
└── Puzzle status becomes SOLVED

If Answer is WRONG:
├── Transaction reverts
├── Puzzle remains LOCKED
├── Solver can try again
└── No penalty except gas fees

If TIMEOUT occurs:
├── Solver cannot submit answer
├── Creator can withdraw prize pool
└── Puzzle resets to CREATED state
```

### 4. Timeout and Withdrawal

If the solver fails to answer before timeout:

```
Creator Actions:
├── Detects timeout (currentBlock >= timeoutBlock)
└── Calls withdrawRiddle()

System Actions:
├── Transfers prize pool to creator
├── Resets puzzle to CREATED state
├── Clears solver address
└── Puzzle can be attempted again
```

## Puzzle States

A puzzle can be in one of the following states:

| State | Description | Can Be Solved | Can Be Edited |
|-------|-------------|---------------|---------------|
| CREATED | Initial state, awaiting solvers | Yes | Yes |
| LOCKED | A solver is currently attempting | No | No |
| SOLVED | Successfully solved | No | No |
| TIMEOUT | Solver failed to answer in time | No | No |

## Economic Model

### Fee Structure

- **Creation Tax**: 5% of deposit
- **Participation Tax**: 5% of solver's payment

### Prize Pool Calculation

```
Prize Pool = Creator Deposit + Solver Deposit - Taxes
```

Example:
- Creator deposits: 1 BNB
- Multiplier: 2x
- Solver pays: 2 BNB
- Creator tax: 0.05 BNB
- Solver tax: 0.1 BNB
- Prize Pool: 1 + 2 - 0.15 = 2.85 BNB
