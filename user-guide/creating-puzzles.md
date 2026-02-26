# Creating Puzzles

Learn how to create your own puzzles on TreasureHunt and set rewards for solvers.

## Prerequisites

Before creating a puzzle, ensure you have:

- A connected Web3 wallet
- Enough BNB for deposit + tax (minimum 0.01 BNB)
- An interesting riddle with a clear answer

## Creating a Puzzle

### Step 1: Navigate to Create Page

Click "Create Puzzle" in the navigation bar.

### Step 2: Fill in Puzzle Details

Complete the following fields:

#### Riddle Content
- The puzzle prompt or question
- Can be text, a riddle, or a cryptogram
- Maximum length: unlimited (but keep it reasonable)

#### Answer
- The plaintext answer to your riddle
- Case-insensitive comparison
- Will be hashed on-chain for security

#### Deposit Amount
- The amount of BNB you're depositing
- Minimum: 0.01 BNB
- This forms part of the prize pool

#### Multiplier
- Determines how much solvers must deposit
- Range: 1x to 10x (system maximum)
- Higher multiplier = bigger prize pool, higher barrier to entry

#### Duration
- Timeout period in blocks
- Default: 1000 blocks (~2.5 hours on BSC)
- Longer duration gives solvers more time

### Step 3: Review and Confirm

Before submitting:

1. Review the total cost breakdown:
   - Your deposit
   - Protocol fee (5%)
   - Total cost

2. Ensure you have enough BNB in your wallet

### Step 4: Sign Transaction

1. Click "Create Puzzle"
2. Confirm the transaction in MetaMask
3. Wait for the transaction to be confirmed

## Cost Calculation Example

| Field | Value |
|-------|-------|
| Deposit | 1.0 BNB |
| Multiplier | 2x |
| Duration | 1000 blocks |
| Tax Rate | 5% |
| **Your Cost** | **1.05 BNB** |

- 1.0 BNB deposited as prize
- 0.05 BNB paid as tax
- Solver must deposit 2.0 BNB to participate

## After Creation

Once your puzzle is created:

- A Puzzle NFT is minted to your address
- The puzzle appears in the marketplace
- Other users can now attempt to solve it
- You can track it in "My Puzzles"

## Managing Your Puzzles

### Editing a Puzzle

You can modify certain parameters before anyone locks it:

- **Multiplier**: Change the solver deposit requirement
- **Duration**: Adjust the timeout period

You cannot change:
- Riddle content
- Answer
- Deposit amount (must destroy and recreate)

### Destroying a Puzzle

If you want to get your deposit back:

1. Go to "My Puzzles"
2. Find the puzzle (must be in "Joinable" state)
3. Click "Destroy"
4. Confirm the transaction

Your deposit (minus tax) will be returned.

### Collecting Timeout Winnings

If a solver locks your puzzle but times out:

1. The puzzle status changes to "Timeout"
2. You can withdraw the prize pool
3. The puzzle resets to "Joinable" state
