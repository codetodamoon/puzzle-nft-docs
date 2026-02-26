# Events

Events are emitted by the smart contract to track important actions on-chain.

## Puzzle Events

### RiddleCreated

Emitted when a new puzzle is created.

```solidity
event RiddleCreated(
    uint256 indexed riddleId,
    address indexed creator,
    uint256 deposit,
    uint256 multiplier
);
```

**Parameters:**
- `riddleId`: Unique identifier of the puzzle
- `creator`: Address of the puzzle creator
- `deposit`: Amount of BNB deposited
- `multiplier`: Solver deposit multiplier

### RiddleLocked

Emitted when a solver locks a puzzle.

```solidity
event RiddleLocked(
    uint256 indexed riddleId,
    address indexed solver,
    uint256 deposit,
    uint256 timeoutBlock
);
```

**Parameters:**
- `riddleId`: Unique identifier of the puzzle
- `solver`: Address of the solver
- `deposit`: Amount deposited by solver
- `timeoutBlock`: Block number when timeout occurs

### RiddleSolved

Emitted when a puzzle is successfully solved.

```solidity
event RiddleSolved(
    uint256 indexed riddleId,
    address indexed solver,
    uint256 reward,
    uint256 tokenId
);
```

**Parameters:**
- `riddleId`: Unique identifier of the puzzle
- `solver`: Address of the winning solver
- `reward`: Amount won as prize
- `tokenId`: Token ID of minted Victory NFT

### RiddleWithdrawn

Emitted when creator withdraws after timeout.

```solidity
event RiddleWithdrawn(
    uint256 indexed riddleId,
    address indexed creator,
    uint256 amount
);
```

**Parameters:**
- `riddleId`: Unique identifier of the puzzle
- `creator`: Address of the creator
- `amount`: Amount withdrawn

### RiddleDestroyed

Emitted when a puzzle is destroyed.

```solidity
event RiddleDestroyed(
    uint256 indexed riddleId,
    address indexed creator
);
```

**Parameters:**
- `riddleId`: Unique identifier of the puzzle
- `creator`: Address of the creator

### RiddleUpdated

Emitted when puzzle parameters are updated.

```solidity
event RiddleUpdated(
    uint256 indexed riddleId,
    uint256 multiplier,
    uint256 duration
);
```

**Parameters:**
- `riddleId`: Unique identifier of the puzzle
- `multiplier`: New multiplier value
- `duration`: New duration value

## Configuration Events

### ConfigUpdated

Emitted when system parameters are changed.

```solidity
event ConfigUpdated(
    string configKey,
    uint256 value
);
```

**Parameters:**
- `configKey`: Name of the parameter
- `value`: New value

## Listening to Events

### Using ethers.js

```javascript
const contract = new ethers.Contract(address, abi, provider);

// Listen for new puzzles
contract.on("RiddleCreated", (riddleId, creator, deposit, multiplier) => {
    console.log(`New puzzle #${riddleId} created by ${creator}`);
});

// Listen for solves
contract.on("RiddleSolved", (riddleId, solver, reward, tokenId) => {
    console.log(`Puzzle #${riddleId} solved by ${solver}`);
});
```

### Using Web3.js

```javascript
const contract = new web3.eth.Contract(abi, address);

contract.events.RiddleCreated({
    fromBlock: 'latest'
}, function(error, event) {
    console.log(event);
});
```

## Indexing Events

Events are indexed for efficient querying:

- `indexed` parameters can be filtered
- Non-indexed parameters require scanning all events

Indexed parameters:
- `riddleId` in all events
- `creator` in creation/destruction events
- `solver` in locking/solving events
