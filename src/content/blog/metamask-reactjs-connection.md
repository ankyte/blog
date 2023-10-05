---
author: Ankit Sahu
pubDatetime: 2023-06-23T00:00:00Z
title: A Step-by-Step Guide of using Ethers v6 library connect Metamask 🦊 to Your React JS Website
postSlug: metamask-reactjs-connection
featured: false
draft: false
tags:
  - react
  - javascript
  - blockchain
  - metamask
description: Metamask is a well-known browser extension that allows users to interact with the Ethereum blockchain effortlessly. In this step-by-step guide, we'll explore how to connect Metamask to your React JS website using the ethers.js library.
---

Metamask is a well-known browser extension that allows users to interact with the Ethereum blockchain effortlessly. In this step-by-step guide, we'll explore how to connect Metamask to your React JS website using the ethers.js library.

By the end of this tutorial, you'll be able to
<br> ✅ check if Metamask is installed </br>
<br> ✅ connect to users' wallets </br>
<br> ✅ add custom networks </br>

## Table of contents

## 🚀 Step 1: Install the Ethers Library 📦

Let's install the ethers library, which will be our primary tool for interacting with the Ethereum blockchain. Open your terminal and run the following command:

```
npm install ethers
```

## 🔍 Step 2: Checking Metamask Installation 🦊

The first step in connecting Metamask to your React JS website is to check whether the user has Metamask installed. In case it's not installed, we'll prompt the user to install Metamask for a smooth experience.

```javascript
const checkMetamaskInstallation = () => {
  if (window.ethereum == undefined) {
    alert("Metamask wallet is not installed");
    return;
  }
};
```

## 💼 Step 3: Initiating Wallet Connection 💳

Once we've ensured that Metamask is present, the next step is to establish a connection between the user's wallet and our DApp. With the connection established, we'll have the user's account address available for further interactions.

```javascript
const [account, setAccount] = useState(null);
const [provider, setProvider] = useState(null);

const initiateWalletConnection = async () => {
  try {
    const provider = new ethers.BrowserProvider(window.ethereum);
    const accounts = await provider.send("eth_requestAccounts", []);
    const account = accounts[0];
    setProvider(provider);
    setAccount(account);
  } catch (error) {
    console.log(error);
  }
};
```

## ⚙️ Step 4: Adding a Custom Network (Optional) 🌐

In some cases, your DApp might be deployed on a specific network, such as the Polygon Mumbai Testnet. To ensure users can interact with your DApp seamlessly you need to add custom networks to the user's Metamask. I'll illustrate this with the example of adding the Polygon Mumbai Testnet.

```javascript
const addPolygonMumbaiTestnet = async () => {
  const provider = new ethers.BrowserProvider(window.ethereum);
  await provider.send("wallet_addEthereumChain", [
    {
      chainId: "0x13881",
      chainName: "Mumbai Testnet",
      nativeCurrency: {
        name: "MATIC",
        symbol: "MATIC",
        decimals: 18,
      },
      rpcUrls: ["https://rpc-mumbai.maticvigil.com"],
      blockExplorerUrls: ["https://mumbai.polygonscan.com/"],
    },
  ]);
};
```

## 🌐 Step 5: Switching to the Custom Network 🔄

After adding the custom network (if needed), it's essential to switch the user's Metamask to the desired network for proper DApp functioning. If the user is already on the desired network, the function does nothing. Otherwise, it switches to the Polygon Mumbai Testnet.

```javascript
const switchToMumbaiTestnet = async () => {
  try {
    const provider = new ethers.BrowserProvider(window.ethereum);
    await provider.send("wallet_switchEthereumChain", [{ chainId: "0x13881" }]);
  } catch (error) {
    if (error.code === 4902) {
      await addPolygonMumbaiTestnet();
    } else {
      console.log(error);
    }
  }
};
```

## 🎉 Conclusion: 🌟

By following this comprehensive guide, you've learned how to integrate Metamask with your React JS website using the powerful ethers.js library. You now have the ability to check if Metamask is installed, connect to users' wallets, and even add custom networks for an enhanced user experience. With this knowledge, you can create feature-rich DApps that leverage the full potential of blockchain technology. 🚀💎
