# Four.meme Bundler Launchpad & Contract ABI

## Overview
I developed Fourmeme Bundler Launch Script.
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

## Usage
### Prerequisites
- A BSC-compatible wallet (e.g., MetaMask) with BNB for gas and transactions.
- A Web3 library (e.g., [Web3.js](https://web3js.readthedocs.io/) or [ethers.js](https://docs.ethers.io/)).
- Node.js or a similar environment for scripting.

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
If you need bundler script, please contact me [here](https://t.me/memelordcrypto) if you have any questions.

## Disclaimer
This ABI is provided "as is" for educational and developmental purposes. Use at your own risk, especially for live transactions. Always verify with the official Four.meme contract at `0x5c952063c7fc8610FFDB798152D69F0B9550762b` before interacting with real funds.
