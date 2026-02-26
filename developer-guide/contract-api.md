# Contract API Reference

This document provides a complete reference for all smart contract functions.

## Configuration Functions

### setTaxRate

```solidity
function setTaxRate(uint256 _rate) external onlyAdmin
```

Sets the tax rate for all transactions.

| Parameter | Type | Description |
|-----------|------|-------------|
| _rate | uint256 | Tax rate in per thousand (e.g., 50 = 5%) |

### setTaxAccount

```solidity
function setTaxAccount(address _account) external onlyAdmin
```

Sets the address where collected taxes are sent.

| Parameter | Type | Description |
|-----------|------|-------------|
| _account | address | New tax account address |

### setMinDeposit

```solidity
function setMinDeposit(uint256 _amount) external onlyAdmin
```

Sets the minimum deposit amount for puzzle creation.

| Parameter | Type | Description |
|-----------|------|-------------|
| _amount | uint256 | Minimum deposit in wei |

### setMaxMultiplier

```solidity
function setMaxMultiplier(uint256 _multiplier) external onlyAdmin
```

Sets the maximum multiplier allowed for puzzles.

| Parameter | Type | Description |
|-----------|------|-------------|
| _multiplier | uint256 | Maximum multiplier value |

### setDefaultDuration

```solidity
function setDefaultDuration(uint256 _blocks) external onlyAdmin
```

Sets the default timeout duration for new puzzles.

| Parameter | Type | Description |
|-----------|------|-------------|
| _blocks | uint256 | Default duration in blocks |

## Puzzle Management

### createRiddle

```solidity
function createRiddle(
    string memory content,
    string memory answer,
    uint256 multiplier,
    uint256 duration
) external payable
```

Creates a new puzzle with a BNB deposit.

| Parameter | Type | Description |
|-----------|------|-------------|
| content | string | Riddle prompt text |
| answer | string | Plaintext answer (will be hashed) |
| multiplier | uint256 | Deposit multiplier for solvers |
| duration | uint256 | Timeout duration in blocks |

**Requirements:**
- Must send value >= minDeposit
- multiplier <= maxMultiplier
- duration > 0

### updateRiddle

```solidity
function updateRiddle(
    uint256 riddleId,
    uint256 multiplier,
    uint256 duration
) external
```

Updates puzzle parameters (only before locking).

| Parameter | Type | Description |
|-----------|------|-------------|
| riddleId | uint256 | ID of the puzzle |
| multiplier | uint256 | New multiplier |
| duration | uint256 | New duration |

**Requirements:**
- Caller must be creator
- Puzzle must not be locked

### withdrawRiddle

```solidity
function withdrawRiddle(uint256 riddleId) external
```

Withdraws prize pool after solver times out.

| Parameter | Type | Description |
|-----------|------|-------------|
| riddleId | uint256 | ID of the puzzle |

**Requirements:**
- Caller must be creator
- Puzzle must be locked and timed out

### destroyRiddle

```solidity
function destroyRiddle(uint256 riddleId) external
```

Destroys a puzzle and recovers deposit.

| Parameter | Type | Description |
|-----------|------|-------------|
| riddleId | uint256 | ID of the puzzle |

**Requirements:**
- Caller must be creator
- Puzzle must not be locked

### withdrawTax

```solidity
function withdrawTax() external onlyAdmin
```

Withdraws accumulated taxes to tax account.

## Solving Puzzles

### lockRiddle

```solidity
function lockRiddle(uint256 riddleId) external payable
```

Locks a puzzle and becomes the current solver.

| Parameter | Type | Description |
|-----------|------|-------------|
| riddleId | uint256 | ID of the puzzle |

**Requirements:**
- Puzzle must be in Created state
- Must send value = deposit × multiplier
- Cannot lock own puzzle

### submitAnswer

```solidity
function submitAnswer(uint256 riddleId, string memory answer) external
```

Submits an answer to solve the puzzle.

| Parameter | Type | Description |
|-----------|------|-------------|
| riddleId | uint256 | ID of the puzzle |
| answer | string | Plaintext answer |

**Requirements:**
- Caller must be current solver
- Must be before timeout
- Answer must be correct

## Read Functions

### getRiddle

```solidity
function getRiddle(uint256 riddleId) external view returns (Riddle memory)
```

Returns the full puzzle data.

### getRiddleStatus

```solidity
function getRiddleStatus(uint256 riddleId) external view returns (RiddleStatus)
```

Returns the puzzle status:
- 0: Created
- 1: Locked
- 2: Solved
- 3: Timeout

### getRiddleIds

```solidity
function getRiddleIds() external view returns (uint256[])
```

Returns all puzzle IDs.

### getUserCreatedRiddles

```solidity
function getUserCreatedRiddles(address user) external view returns (uint256[])
```

Returns all puzzles created by a user.

### getUserSolvedRiddles

```solidity
function getUserSolvedRiddles(address user) external view returns (uint256[])
```

Returns all puzzles solved by a user.

### getRiddleHistory

```solidity
function getRiddleHistory(uint256 riddleId) external view returns (SolveHistory[] memory)
```

Returns solve history for a puzzle.

### getVictoryTokenCount

```solidity
function getVictoryTokenCount() external view returns (uint256)
```

Returns total number of Victory NFTs minted.

### getVictoryMetadata

```solidity
function getVictoryMetadata(uint256 tokenId) external view returns (VictoryMetadata memory)
```

Returns Victory NFT metadata.

### tokenURI

```solidity
function tokenURI(uint256 tokenId) public view returns (string memory)
```

Returns URI for any NFT (puzzle or victory).

## View Variables

| Variable | Type | Description |
|----------|------|-------------|
| admin | address | Contract administrator |
| taxAccount | address | Tax collection address |
| taxRate | uint256 | Tax rate (per thousand) |
| minDeposit | uint256 | Minimum deposit amount |
| maxMultiplier | uint256 | Maximum multiplier |
| defaultDuration | uint256 | Default timeout blocks |
| riddleCounter | uint256 | Total riddles created |
| victoryCounter | uint256 | Total victories minted |
