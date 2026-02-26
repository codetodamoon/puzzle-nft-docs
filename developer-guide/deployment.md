# Deployment Guide

This guide covers how to deploy TreasureHunt to different networks.

## Prerequisites

- Node.js 18+
- npm or yarn
- A wallet with sufficient BNB for deployment costs
- For testnet: Get test BNB from faucets

## Deployment Checklist

- [ ] Compile contracts: `npx hardhat compile`
- [ ] Run tests: `npx hardhat test`
- [ ] Configure network settings
- [ ] Deploy contracts
- [ ] Verify contracts on BscScan
- [ ] Update frontend configuration
- [ ] Deploy frontend

## Smart Contract Deployment

### Configuration

Edit `hardhat.config.js` to add or configure networks:

```javascript
module.exports = {
  networks: {
    hardhat: {
      chainId: 31337,
    },
    'bsc-testnet': {
      url: 'https://data-seed-prebsc-1-s1.bnbchain.org:8545',
      chainId: 97,
      accounts: ['YOUR_PRIVATE_KEY'],
    },
    'bsc-mainnet': {
      url: 'https://bsc-dataseed.binance.org',
      chainId: 56,
      accounts: ['YOUR_PRIVATE_KEY'],
    },
  },
};
```

### Deploy Commands

#### Local Hardhat Network

```bash
npx hardhat node
npx hardhat run scripts/deploy.js --network hardhat
```

#### BSC Testnet

```bash
# Get test BNB from faucet first
npx hardhat run scripts/deploy.js --network bsc-testnet
```

#### BSC Mainnet

```bash
# WARNING: This costs real BNB
npx hardhat run scripts/deploy.js --network bsc-mainnet
```

### Deployment Output

After deployment, you'll see output like:

```
Deploying TreasureHunt...
TreasureHunt deployed to: 0x...
Tax account set to: 0x...
Transaction confirmed
```

Save the deployed contract address.

## Contract Verification

### Verify on BscScan

After deploying to mainnet/testnet:

1. Go to BscScan
2. Find your contract
3. Click "Verify and Publish"
4. Select "Solidity (Single File)"
5. Paste the contract code
6. Match compiler settings:
   - Compiler version: 0.8.20
   - EVM version: Paris
   - Optimization: Yes (200 runs)

## Frontend Deployment

### Update Configuration

After contract deployment, update `code/.env`:

```
VITE_CONTRACT_ADDRESS_BSC_MAINNET=0xYOUR_NEW_ADDRESS
```

### Build

```bash
cd code
npm run build
```

### Deploy Options

#### GitHub Pages

1. Enable GitHub Pages in repository settings
2. Deploy the `dist/` folder
3. Set custom domain (optional)

#### Vercel

```bash
npm i -g vercel
vercel --prod
```

#### Netlify

```bash
npm i -g netlify-cli
netlify deploy --prod --dir=code/dist
```

## Network-Specific Addresses

| Network | Contract Address | BSCScan |
|---------|------------------|---------|
| BSC Mainnet | TBD | TBD |
| BSC Testnet | TBD | TBD |
| opBNB Mainnet | TBD | TBD |
| opBNB Testnet | TBD | TBD |

## Post-Deployment

1. **Verify functionality**
   - Create a test puzzle
   - Attempt to solve it
   - Test timeout withdrawal

2. **Update documentation**
   - Record contract addresses
   - Update this documentation

3. **Set admin configuration**
   - Configure tax rate
   - Set tax account
   - Adjust parameters as needed
