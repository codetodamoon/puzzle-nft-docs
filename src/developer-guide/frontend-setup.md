# Frontend Setup

This guide explains how to set up and run the TreasureHunt frontend locally.

## Prerequisites

- Node.js 18+
- npm or yarn
- A Web3 wallet (MetaMask recommended)

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-repo/puzzle-nft.git
cd puzzle-nft
```

### 2. Install Dependencies

```bash
cd code
npm install
```

### 3. Environment Configuration

Create a `.env` file in the `code/` directory:

```env
# Contract Addresses
VITE_CONTRACT_ADDRESS_BSC_MAINNET=0x...
VITE_CONTRACT_ADDRESS_OPBNB_MAINNET=0x...
VITE_CONTRACT_ADDRESS_BSC_TESTNET=0x...
VITE_CONTRACT_ADDRESS_OPBNB_TESTNET=0x...
VITE_CONTRACT_ADDRESS_HARDHAT=0x...

# Admin Address
VITE_ADMIN_ADDRESS=0x...
```

### 4. Start Development Server

```bash
npm run dev
```

The app will be available at `http://localhost:3000`.

## Project Structure

```
code/
├── src/
│   ├── pages/           # Page components
│   │   ├── HomePage.tsx
│   │   ├── CreatePuzzlePage.tsx
│   │   ├── PuzzleDetailsPage.tsx
│   │   ├── ProfilePage.tsx
│   │   └── AdminPage.tsx
│   ├── components/      # Reusable components
│   │   ├── Navbar.tsx
│   │   ├── Footer.tsx
│   │   ├── PuzzleCard.tsx
│   │   └── StatsOverview.tsx
│   ├── lib/            # Utilities
│   │   ├── contract.ts # Contract interaction
│   │   └── wallet.ts   # Wallet connection
│   ├── App.tsx         # Main app component
│   └── main.tsx        # Entry point
├── public/             # Static assets
├── index.html          # HTML template
└── vite.config.ts     # Vite configuration
```

## Key Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| react | ^18.x | UI framework |
| react-router-dom | ^6.x | Routing |
| ethers | ^6.x | Blockchain interaction |
| tailwindcss | ^3.x | Styling |
| vite | ^5.x | Build tool |
| lucide-react | ^0.x | Icons |

## Building for Production

```bash
npm run build
```

Output will be in the `dist/` directory.

## Testing

The frontend can be tested against:

1. **Local Hardhat Node**: `npx hardhat node`
2. **Testnet**: BSC Testnet or opBNB Testnet
3. **Mainnet**: BSC Mainnet or opBNB Mainnet

## Common Issues

### "Contract is not defined"

**Solution**: Ensure the contract ABI is up to date in `TreasureHunt.json`.

### "MetaMask not detected"

**Solution**: Install MetaMask browser extension and refresh the page.

### Network mismatch errors

**Solution**: Switch MetaMask to the correct network (BSC Mainnet, etc.).

## Connecting to Local Node

To test with a local Hardhat node:

1. Start Hardhat node: `npx hardhat node`
2. Deploy contract: `npx hardhat run scripts/deploy.js --network localhost`
3. Update `.env` with local contract address
4. Add Hardhat network to MetaMask:
   - Network Name: Hardhat Local
   - RPC URL: http://127.0.0.1:8545
   - Chain ID: 31337
