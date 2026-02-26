# Configuration

This guide explains how to configure the TreasureHunt system parameters as an administrator.

## Accessing Admin Panel

### Requirements

Only the contract admin can access the admin panel.

1. Connect your wallet
2. Ensure your address matches the admin address in the contract
3. Look for "Admin" link in the navigation

### Current Admin

The admin address is set during deployment and stored in the contract.

## Configuration Parameters

### Tax Rate

- **Variable**: `taxRate`
- **Unit**: Per thousand (e.g., 50 = 5%)
- **Default**: 50 (5%)
- **Purpose**: Fee taken from all deposits

### Tax Account

- **Variable**: `taxAccount`
- **Type**: Address
- **Purpose**: Where collected taxes are sent

### Minimum Deposit

- **Variable**: `minDeposit`
- **Unit**: Wei (BNB × 10^18)
- **Default**: 0.01 BNB
- **Purpose**: Lowest amount a creator can deposit

### Maximum Multiplier

- **Variable**: `maxMultiplier`
- **Type**: uint256
- **Default**: 10
- **Purpose**: Highest multiplier creators can set

### Default Duration

- **Variable**: `defaultDuration`
- **Unit**: Blocks
- **Default**: 1000 blocks (~2.5 hours on BSC)
- **Purpose**: Default timeout period for new puzzles

## Updating Configuration

### Via Admin Panel

1. Navigate to Admin page
2. Enter new value for the parameter
3. Click "Update"
4. Confirm transaction in wallet

### Via Smart Contract

You can also update directly via the contract:

```solidity
// Set tax rate to 5%
await contract.setTaxRate(50);

// Set minimum deposit to 0.05 BNB
await contract.setMinDeposit(ethers.parseEther("0.05"));

// Set max multiplier to 20
await contract.setMaxMultiplier(20);

// Set default duration to 2000 blocks
await contract.setDefaultDuration(2000);

// Change tax account
await contract.setTaxAccount("0x...");
```

### Withdrawing Taxes

To withdraw accumulated taxes:

```javascript
await contract.withdrawTax();
```

This transfers all collected taxes to the tax account.

## Recommended Settings

### For Production (BSC Mainnet)

| Parameter | Recommended Value | Rationale |
|-----------|------------------|-----------|
| Tax Rate | 50 (5%) | Industry standard |
| Min Deposit | 0.01 BNB | Low barrier to entry |
| Max Multiplier | 10 | Reasonable risk |
| Default Duration | 1000 | ~2.5 hours is reasonable |

### For Testing (Testnet)

| Parameter | Recommended Value | Rationale |
|-----------|------------------|-----------|
| Tax Rate | 0 | Free testing |
| Min Deposit | 0.001 BNB | Easier testing |
| Max Multiplier | 100 | More experimentation |
| Default Duration | 100 | Faster testing |

## Security Considerations

### Admin Key Management

- Store admin private key securely
- Use multisig for production
- Consider timelock for parameter changes

### Parameter Limits

Be careful when adjusting parameters:

- **Too high tax rate**: Discourages usage
- **Too low min deposit**: May attract spam
- **Too high multiplier**: High risk for solvers
- **Too short duration**: May frustrate users
