# Frequently Asked Questions

## General Questions

### What is TreasureHunt?

TreasureHunt is a decentralized puzzle marketplace where users can create cryptographic puzzles with BNB prizes. Solvers who successfully answer the riddles win the prize pool and receive a unique Victory NFT.

### Which networks does TreasureHunt support?

Currently supported:
- BSC Mainnet (Chain ID: 56)
- opBNB Mainnet (Chain ID: 204)
- BSC Testnet (Chain ID: 97)
- opBNB Testnet (Chain ID: 5611)

### Is TreasureHunt safe?

Yes, TreasureHunt uses:
- Industry-standard smart contracts (OpenZeppelin)
- On-chain answer hashing (answers never stored in plaintext)
- Reentrancy protection
- Comprehensive test coverage

## Puzzles

### How do I create a puzzle?

1. Connect your wallet
2. Click "Create Puzzle"
3. Fill in riddle content, answer, deposit, multiplier, duration
4. Confirm the transaction

### What's the minimum deposit?

0.01 BNB is the minimum deposit amount.

### Can I change my puzzle after creating it?

You can edit the multiplier and duration while the puzzle is in "Joinable" status. You cannot change the riddle content, answer, or deposit amount.

### What happens if my puzzle is never solved?

Your puzzle remains active until solved. You can destroy it at any time while it's in "Joinable" status to recover your deposit (minus tax).

### Can I create multiple puzzles?

Yes! There's no limit to how many puzzles you can create.

## Solving Puzzles

### Why do I need to lock a puzzle first?

Locking a puzzle serves two purposes:
1. It proves your commitment by depositing BNB
2. It gives you exclusive rights to solve that puzzle

### What happens if I submit the wrong answer?

The transaction will revert, but you remain the current solver. You can try again (paying gas fees each time) until you timeout or succeed.

### What happens if I timeout?

Your deposited BNB is forfeited to the puzzle creator. You cannot submit any answer after timeout.

### Can I solve my own puzzle?

No, you cannot lock or solve your own puzzle.

## Victory NFT

### What is a Victory NFT?

A Victory NFT is a unique token minted to solvers who successfully solve puzzles. It serves as permanent proof of your achievement.

### How do I view my Victory NFTs?

Visit your Profile page and look for the "Victory NFT Gallery" section.

### Can I transfer my Victory NFT?

Yes, Victory NFTs are standard ERC-721 tokens and can be transferred to any address.

## Fees and Costs

### What fees does TreasureHunt charge?

- **Creation Tax**: 5% of your deposit
- **Participation Tax**: 5% of solver's payment

### Do I need BNB for gas?

Yes, every transaction requires BNB to pay for gas fees.

### Why do I need more BNB than the deposit amount?

You need BNB for:
- The deposit itself
- Protocol fees (5%)
- Gas fees for transactions
