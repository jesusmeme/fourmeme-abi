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

| **Type**       | **Name**                       | **Inputs**                                                                                   | **Outputs**                                                                 | **Description**                                                                                              | **State Mutability** |
|----------------|--------------------------------|---------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|----------------------|
| **Error**      | `OwnableInvalidOwner`          | `owner` (address)                                                                           | -                                                                           | Thrown when an invalid owner address (e.g., zero address) is provided.                                      | -                    |
| **Error**      | `OwnableUnauthorizedAccount`   | `account` (address)                                                                         | -                                                                           | Thrown when an account lacks permission to perform an action (e.g., not owner or authorized role).          | -                    |
| **Event**      | `AdminChanged`                 | `previousAdmin` (address), `newAdmin` (address)                                             | -                                                                           | Emitted when the admin address changes.                                                                     | -                    |
| **Event**      | `OwnershipTransferred`         | `previousOwner` (address, indexed), `newOwner` (address, indexed)                           | -                                                                           | Emitted when contract ownership is transferred.                                                             | -                    |
| **Event**      | `TokenCreate`                  | `creator` (address), `token` (address), `requestId` (uint256), `name` (string), etc.        | -                                                                           | Emitted when a new token is created with specified parameters.                                              | -                    |
| **Event**      | `TokenPurchase`                | `token` (address), `account` (address), `tokenAmount` (uint256), `etherAmount` (uint256)    | -                                                                           | Emitted when tokens are purchased.                                                                          | -                    |
| **Event**      | `TradeStop`                    | `token` (address)                                                                           | -                                                                           | Emitted when trading is halted for a specific token.                                                        | -                    |
| **Function**   | `createToken`                  | `requestId` (uint256), `name` (string), `symbol` (string), `totalSupply` (uint256), etc.    | -                                                                           | Creates a new token with specified parameters; payable with a launch fee.                                   | Payable             |
| **Function**   | `purchaseToken`                | `tokenAddress` (address), `amount` (uint256), `maxFunds` (uint256)                          | -                                                                           | Purchases a specified amount of tokens, payable with Ether.                                                 | Payable             |
| **Function**   | `saleToken`                    | `tokenAddress` (address), `amount` (uint256)                                                | -                                                                           | Sells a specified amount of tokens back to the contract.                                                    | Nonpayable          |
| **Function**   | `_calcBuyCost`                 | `ti` (TokenInfo struct), `amount` (uint256)                                                 | `uint256`                                                                   | Calculates the Ether cost to buy a given token amount (pure function).                                      | Pure                |
| **Function**   | `lastPrice`                    | `tokenAddress` (address)                                                                    | `uint256`                                                                   | Returns the last trading price of a token.                                                                  | View                |
| **Function**   | `owner`                        | -                                                                                           | `address`                                                                   | Returns the current contract owner.                                                                         | View                |
| **Function**   | `transferOwnership`            | `newOwner` (address)                                                                        | -                                                                           | Transfers ownership to a new address.                                                                       | Nonpayable          |
| **Function**   | `grantRole`                    | `role` (bytes32), `account` (address)                                                       | -                                                                           | Grants a specific role to an account.                                                                       | Nonpayable          |
| **Function**   | `hasRole`                      | `role` (bytes32), `account` (address)                                                       | `bool`                                                                      | Checks if an account has a specific role.                                                                   | View                |
| **Function**   | `setFeeRecipient`              | `v` (address)                                                                               | -                                                                           | Sets the address that receives trading and launch fees.                                                     | Nonpayable          |
| **Function**   | `stopTrade`                    | `tokenAddress` (address)                                                                    | -                                                                           | Halts trading for a specific token.                                                                         | Nonpayable          |
| **Function**   | `withdrawEth`                  | `to` (address), `amount` (uint256)                                                          | -                                                                           | Withdraws Ether from the contract to a specified address.                                                   | Nonpayable          |
| **Function**   | `PANCAKE_ROUTER`               | -                                                                                           | `address`                                                                   | Returns the address of the PancakeSwap router (constant).                                                   | View                |
| **Function**   | `_tokenInfos`                  | `tokenAddress` (address)                                                                    | `TokenInfo` struct (bool, uint256, etc.)                                    | Returns metadata about a token (e.g., launch time, offers, trading status).                                 | View                |

## Usage
### Prerequisites
- A BSC-compatible wallet (e.g., MetaMask) with BNB for gas and transactions.
- A Web3 library (e.g., [Web3.js](https://web3js.readthedocs.io/) or [ethers.js](https://docs.ethers.io/)).
- Node.js or a similar environment for scripting.

### Example: Interacting with the Contract
Using ethers.js to call `createToken`:

```javascript
const wallet = new ethers.Wallet('YOUR_PRIVATE_KEY', provider);
const contractWithSigner = contract.connect(wallet);

async function createNewToken() {
  const tx = await contractWithSigner.createToken(
    123, // requestId
    "MyToken", // name
    "MTK", // symbol
    ethers.utils.parseEther("1000000"), // totalSupply
    ethers.utils.parseEther("1000"), // maxOffer
    ethers.utils.parseEther("100"), // presale
    Math.floor(Date.now() / 1000) + 3600, // launchTime (1 hour from now)
    { value: ethers.utils.parseEther("0.1") } // launchFee in ETH
  );
  await tx.wait();
  console.log('Token Created:', tx.hash);
}

createNewToken();
```

### Deploying a Test Version
To test this ABI locally:
1. Copy the ABI into a Solidity project (e.g., Hardhat or Truffle).
2. Implement dummy logic matching the ABI in a contract.
3. Deploy to BSC Testnet (`https://data-seed-prebsc-1-s1.binance.org:8545/`).

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
