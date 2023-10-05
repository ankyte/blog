---
author: Ankit Sahu
pubDatetime: 2023-06-23T00:00:00Z
title: Create and deploy your own token using hardhat in just 2 mins
postSlug: hardhat-blockchain-token
featured: false
draft: false
tags:
  - blockchain
  - hardhat
  - solidity
description: In this tutorial, I will guide you through the process of creating and deploying your own ERC20 token using the Hardhat development environment.
---

In this tutorial, I will guide you through the process of creating and deploying your own ERC20 token using the Hardhat development environment.

## Table of contents

## Prerequisites:

Before we get started, make sure you have the following set up on your machine:

- Node.js and npm (Node Package Manager) installed
- Basic knowledge of Solidity programming language
- Familiarity with the Ethereum ecosystem and ERC20 tokens

## Step 1: Setting Up the Project

1. Create a new directory for your project and navigate to it in your terminal.
2. Initialize a new Node.js project by running the command: `npm init -y`.
3. Install Hardhat as a development dependency by running: `npm install --save-dev hardhat`.
4. Open the project in your preferred code editor.

## Step 2: Writing the ERC20 Token Contract

1. Install the OpenZeppelin Contracts library, which provides pre-audited and secure contract implementations: `npm install @openzeppelin/contracts`.
2. Create a new file named `Zen.sol` in the `contracts` directory.
3. Add the following code to the `Zen.sol` file:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract Zen is ERC20 {
    uint256 constant initialSupply = 1000000 * (10 ** 18);

    constructor() ERC20("Zen", "ZEN") {
        _mint(msg.sender, initialSupply);
    }

    function decimals() public pure override returns (uint8) {
        return 18;
    }
}
```

## Step 3: Writing the Deployment Script

1. Create a new directory named `scripts` in the project root.
2. Inside the `scripts` directory, create a new file named `deploy.js`.
3. Add the following code to the `deploy.js` file:

```javascript
const hre = require("hardhat");
const fs = require("fs");

async function main() {
  const [deployer] = await hre.ethers.getSigners();
  console.log("Deployer address:", deployer.address);
  const zen = await hre.ethers.deployContract("Zen");
  await zen.waitForDeployment();
  const contractAddress = zen.target;
  console.log("Contract Address:", contractAddress);
  const zenArtifact = require("../artifacts/contracts/Zen.sol/Zen.json");
  const zenAbi = zenArtifact.abi;
  const contractData = {
    address: contractAddress,
    abi: zenAbi,
  };
  fs.writeFileSync("./abi/zen.json", JSON.stringify(contractData, null, 2));
}

main()
  .then(() => process.exit(0))
  .catch(error => {
    console.error(error);
    process.exit(1);
  });
```

## Step 4: Configuring Hardhat

1. Open the `hardhat.config.js` file in the project root directory.
2. Update the file with the following configuration:

```javascript
require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config();
const { POLYGON_MUMBAI_RPC_PROVIDER, PRIVATE_KEY, POLYGONSCAN_API_KEY } = process.env;

module.exports = {
    defaultNetwork: "hardhat",
    networks: {
        hardhat: {
            chainId: 1337,
        },
        mumbai: {
            url: POLYGON

_MUMBAI_RPC_PROVIDER,
            accounts: [`0x${PRIVATE_KEY}`],
        },
    },
    solidity: {
        version: "0.8.9",
        settings: {
            optimizer: {
                enabled: true,
                runs: 200,
            },
        },
    },
    etherscan: {
        apiKey: POLYGONSCAN_API_KEY,
    },
};
```

## Step 5: Deploying the ERC20 Token

1. Run the deployment script by executing the command: `npx hardhat run scripts/deploy.js --network <network>`.
   Replace `<network>` with the desired network, such as `mumbai` for the Polygon Mumbai testnet.
2. The script will deploy the `Zen` contract and output the deployer's address and the deployed contract address.
3. The contract's ABI will be saved to the `./abi/zen.json` file.

## Conclusion:

Congratulations! You have successfully created and deployed your own ERC20 token using Hardhat. You can now use the contract address and ABI to interact with the token on the Ethereum network. ERC20 tokens are the building blocks for decentralized applications, enabling various use cases such as digital currencies, loyalty points, and more. Experiment with your token and explore the endless possibilities of decentralized finance.

Feel free to customize and extend the functionality of your ERC20 token contract according to your specific requirements. Happy coding!
