# Four.meme Launchpad Contract ABI

## Overview
This repository contains the Application Binary Interface (ABI) for the Four.meme launchpad smart contract deployed on Binance Smart Chain (BSC). Four.meme is a decentralized platform for creating and launching meme coins, featuring a bonding curve mechanism, low-cost token deployment (0.005 BNB), and automatic liquidity seeding to PancakeSwap V3 at 24 BNB. This ABI enables developers to interact with the contract programmatically using tools like Web3.js, ethers.js, or other BSC-compatible libraries.

**Note**: The ABI provided here is a reconstructed approximation based on Four.meme’s public documentation and typical BSC launchpad patterns as of March 21, 2025. It has not been directly sourced from the live contract at `0x5c952063c7fc8610FFDB798152D69F0B9550762b`. For the exact ABI, visit [BSCScan](https://bscscan.com/address/0x5c952063c7fc8610FFDB798152D69F0B9550762b#code) to check if the contract is verified or analyze its transaction logs.

## Features
- **Token Creation**: Deploy meme coins with a name, symbol, and total supply for 0.005 BNB.
- **Bonding Curve**: Buy and sell tokens with dynamic pricing via a bonding curve.
- **Liquidity Integration**: Automatically adds liquidity to PancakeSwap V3 when the bonding curve reaches 24 BNB.
- **Admin Controls**: Fee management, pausing/unpausing, and fee withdrawal for contract maintainers.
- **Transparency**: Events for tracking token creation, trades, and liquidity events.

## Contract Details
- **Network**: Binance Smart Chain (BSC)
- **Contract Address**: `0x5c952063c7fc8610FFDB798152D69F0B9550762b`
- **Status**: Reconstructed (unverified against live contract)
- **Last Updated**: March 21, 2025

## ABI
The full ABI is provided in [`abi.json`](./abi.json). Below is a summary of the key functions and events based on the reconstructed ABI:

### Functions
| Function Name                | Inputs                                      | Outputs         | Description                                      |
 |------------------------------|---------------------------------------------|-----------------|--------------------------------------------------|
 | `createToken`                | `string name, string symbol, uint256 totalSupply` | `address`       | Creates a new meme token (payable: 0.005 BNB).   |
 | `buyToken`                   | `address token, uint256 amount`             | -               | Buys tokens via bonding curve (payable).         |
 | `sellToken`                  | `address token, uint256 amount`             | -               | Sells tokens back to the contract.               |
 | `addLiquidityToPancakeSwap`  | `address token`                             | -               | Adds liquidity to PancakeSwap at 24 BNB.         |
 | `getTokenPrice`              | `address token`                             | `uint256`       | Returns current token price (view).              |
 | `withdrawFees`               | `address recipient`                         | -               | Withdraws collected fees (admin only).           |
 | `setFee`                     | `uint256 newFee`                            | -               | Updates trading fee (admin only).                |
 | `pause`                      | -                                           | -               | Pauses contract operations (admin only).         |
 | `unpause`                    | -                                           | -               | Resumes contract operations (admin only).        |
 | `getBondingCurveProgress`    | `address token`                             | `uint256`       | Returns BNB in bonding curve (view).             |
 
 ### Events
 | Event Name          | Parameters                                              | Description                              |
 |---------------------|--------------------------------------------------------|------------------------------------------|
 | `TokenCreated`      | `address indexed creator, address indexed token, string name` | Emitted when a new token is created.     |
 | `TokenPurchased`    | `address indexed buyer, address indexed token, uint256 amount, uint256 cost` | Logs a token purchase.                   |
 | `TokenSold`         | `address indexed seller, address indexed token, uint256 amount, uint256 refund` | Logs a token sale.                       |
 | `LiquidityAdded`    | `address indexed token, uint256 bnbAmount, uint256 tokenAmount` | Logs liquidity addition to PancakeSwap.  |

## Usage
### Prerequisites
- A BSC-compatible wallet (e.g., MetaMask) with BNB for gas and transactions.
- A Web3 library (e.g., [Web3.js](https://web3js.readthedocs.io/) or [ethers.js](https://docs.ethers.io/)).
- Node.js or a similar environment for scripting.

### Example: Interacting with the Contract
Using ethers.js to call `createToken`:

```javascript
const ethers = require('ethers');
 const abi = require('./abi.json');
 
 // Connect to BSC
 const provider = new ethers.providers.JsonRpcProvider('https://bsc-dataseed.binance.org/');
 const wallet = new ethers.Wallet('YOUR_PRIVATE_KEY', provider);
 
 // Contract setup
 const contractAddress = '0x5c952063c7fc8610FFDB798152D69F0B9550762b';
 const contract = new ethers.Contract(contractAddress, abi, wallet);
 
 // Create a new token
 async function createMemeToken() {
   const tx = await contract.createToken(
     "TestMemeCoin",   // Name
     "TMC",          // Symbol
     ethers.utils.parseUnits("1000000000", 18), // Total supply (1 billion)
     { value: ethers.utils.parseEther("0.005") } // 0.005 BNB fee
  );
  await tx.wait();
  console.log('Token Created:', tx.hash);
}

createMemeToken();
```

## Verification
This ABI is a best-effort reconstruction and may not match the live contract exactly. To verify:
1. Visit [BSCScan](https://bscscan.com/address/0x5c952063c7fc8610FFDB798152D69F0B9550762b#code) to check if the contract is verified and retrieve the official ABI.
2. Analyze transaction logs on BSCScan (e.g., function signatures like `0x0e3ddcb9`) to confirm the functions match this ABI.
3. If discrepancies exist, update this repository with the verified ABI.

## Contributing
Contributions are welcome! If you have the official ABI, updates (e.g., post-audit changes after the February 2025 exploit), or additional details:
1. Fork this repository.
2. Update `abi.json` or this README.
3. Submit a pull request.

## **☕ Buy Me a Coffee ☕**
If you find this repository helpful, consider supporting me with a coffee or some crypto! Your support keeps me fueled to create more resources like this.  
👉 **Buy Me a Coffee** 👈  
- **Ethereum (ETH)**: `0x7777746B8E28059676bd053D8B86Cd60B6872eec`  
- **Solana (SOL)**: `tipRJZ4AKbWV6WFN9sVaJtDsrfQKg2bF3YfPrLUxSVi`  
*Every little bit helps—thank you!*
Contact me [here](https://t.me/memelordcrypto) if you have any questions.

## License
This project is licensed under the MIT License. See [LICENSE](./LICENSE) for details.

## Disclaimer
This ABI is provided "as is" for educational and developmental purposes. Use at your own risk, especially for live transactions. Always verify with the official Four.meme contract at `0x5c952063c7fc8610FFDB798152D69F0B9550762b` before interacting with real funds.
