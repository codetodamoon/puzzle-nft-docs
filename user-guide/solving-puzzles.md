# Solving Puzzles

Learn how to participate in puzzles and win BNB rewards by solving riddles.

## Understanding the Process

Solving a puzzle involves two steps:

1. **Lock the puzzle** - Deposit your stake and become the current solver
2. **Submit answer** - Provide the correct answer before timeout

## Step 1: Find a Puzzle

1. Browse the homepage to see available puzzles
2. Click on any puzzle card to view details
3. Review the puzzle information:
   - Riddle content
   - Deposit amount
   - Multiplier
   - Prize pool (deposit × multiplier)

## Step 2: Lock the Puzzle

Before you can see the riddle content or submit an answer, you must lock the puzzle:

### Requirements

- Puzzle must be in "Joinable" status
- You must have enough BNB for deposit × multiplier + tax
- You cannot lock your own puzzle

### Process

1. Click "Participate & Decrypt"
2. Review the cost breakdown:
   - Entry amount: deposit × multiplier
   - Protocol fee (5%)
   - Total cost
3. Confirm the transaction in MetaMask
4. Wait for confirmation

### After Locking

Once locked:
- You become the current solver
- You can now see the riddle content
- You must submit your answer before timeout
- The timer starts counting down

## Step 3: Submit Your Answer

### Before Timeout

You have until the timeout block to submit your answer:

1. Enter your answer in the input field
2. Click "Submit Answer"
3. Confirm the transaction in MetaMask
4. Wait for confirmation

### If Answer is Correct

- You receive the full prize pool (creator deposit + your deposit - taxes)
- A Victory NFT is minted to your address
- Puzzle status changes to "Solved"

### If Answer is Wrong

- Transaction reverts (fails)
- You remain the current solver
- You can try again (just pay gas fees)
- No additional penalty

### After Timeout

If you fail to submit before the timeout block:

- Submit button is disabled
- You cannot submit any answer
- Your deposit is forfeited
- Creator can withdraw the prize pool
- Puzzle resets to "Joinable" state

## Understanding the Economics

### Your Potential Win

If you solve correctly:
```
Prize = Creator Deposit + Your Deposit - Taxes
```

Example:
- Creator deposit: 1.0 BNB
- Multiplier: 2x
- Your deposit: 2.0 BNB
- Prize pool: 3.0 BNB (minus small tax)
- Your net profit: ~1.0 BNB

### Your Risk

If you timeout or fail:
- You lose your deposited amount
- Creator keeps your deposit
- No Victory NFT is minted

## Tips for Success

### Choose Puzzles Wisely

- Start with lower multipliers (1x-2x)
- Look for riddles you think you can solve
- Check the timeout duration

### Manage Your Time

- Note the timeout block number
- Submit well before the deadline
- Don't wait until the last minute

### Verify Your Answer

- Double-check your answer before submitting
- Remember: case-insensitive
- Watch for typos or extra spaces
