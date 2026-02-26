# Testing Guide

This guide explains how to run and extend tests for TreasureHunt.

## Test Structure

Tests are located in the `test/` directory:

```
test/
├── TreasureHunt.js      # Main contract tests
└── testFullFlow.js      # Integration tests
```

## Running Tests

### Run All Tests

```bash
npx hardhat test
```

### Run Specific Test File

```bash
npx hardhat test test/TreasureHunt.js
```

### Run Tests Matching Pattern

```bash
npx hardhat test --grep "createRiddle"
```

## Test Coverage

### Current Coverage

| Module | Tests | Status |
|--------|-------|--------|
| Deployment & Admin | 7 | ✅ |
| Create Riddle | 7 | ✅ |
| Lock Riddle | 4 | ✅ |
| Submit Answer | 5 | ✅ |
| Timeout & Withdraw | 4 | ✅ |
| Destroy Riddle | 3 | ✅ |
| Status Queries | 4 | ✅ |
| View Functions | 2 | ✅ |
| Edge Cases | 2 | ✅ |
| **Total** | **38** | **✅** |

## Writing Tests

### Test Structure

```javascript
describe("FunctionName", function () {
  before(async function () {
    // Setup - deploy contracts, get signers
  });

  it("should do something", async function () {
    // Test implementation
  });

  it("should revert on invalid input", async function () {
    // Expect revert
    await expect(contract.function()).to.be.revertedWith("ErrorMessage");
  });
});
```

### Test Helpers

The test suite uses Hardhat's ethers.js wrapper:

```javascript
const { ethers } = require("hardhat");
const { expect } = require("chai");
```

### Common Patterns

#### Get Signers

```javascript
const [admin, creator, solver, user] = await ethers.getSigners();
```

#### Call as Different Users

```javascript
await contract.connect(creator).createRiddle(...);
await contract.connect(solver).lockRiddle(riddleId, { value: ... });
```

#### Check Events

```javascript
await expect(tx)
  .to.emit(contract, "RiddleCreated")
  .withArgs(riddleId, creator.address, deposit, multiplier);
```

#### Check Balances

```javascript
expect(await ethers.provider.getBalance(contract.address)).to.equal(expected);
```

## Integration Testing

### Full Flow Test

The `testFullFlow.js` file contains end-to-end scenarios:

1. Create puzzle
2. Lock puzzle
3. Submit correct answer
4. Verify Victory NFT minted

### Running Integration Tests

```bash
npx hardhat test test/testFullFlow.js
```

## Test Networks

Tests run against the Hardhat network by default, which:
- Is a local in-memory blockchain
- Has 20 test accounts with 10000 ETH each
- Instant block confirmation
- No real money at risk

## Continuous Integration

To add tests to CI:

```yaml
# .github/workflows/test.yml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm install
      - run: npx hardhat compile
      - run: npx hardhat test
```

## Debugging Failed Tests

### Increase Verbosity

```bash
npx hardhat test --verbose
```

### Use console.log

```javascript
console.log("Current state:", await contract.getRiddle(riddleId));
```

### Check Revert Reasons

```javascript
await expect(contract.function()).to.be.revertedWith("ExpectedError");
```
