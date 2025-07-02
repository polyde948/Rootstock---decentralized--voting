
# 🗳️ Rootstock Decentralized Voting

**A Transparent, Tamper-Proof On-Chain Voting System Powered by Bitcoin via Rootstock (RSK)**

![Rootstock Voting Banner](https://user-images.githubusercontent.com/placeholder/banner.png) <!-- Optional: Replace with your own hosted image -->

---

## 🔍 What Is This?

**Rootstock Decentralized Voting** is a smart contract-based system that allows anyone to create polls, cast votes, and view results on-chain — powered by the Rootstock blockchain and settled in RBTC.

This project brings **governance to the blockchain**, making it easy for DAOs, communities, and organizations to implement **secure, censorship-resistant decision-making** with no third-party interference.

---

## 🌟 Features

- ✅ Create polls with multiple options
- ✅ Transparent vote tracking on-chain
- ✅ One vote per wallet per poll (prevents abuse)
- ✅ Real-time results anytime, anywhere
- ✅ Poll creator can close voting at will
- ✅ Low gas fees thanks to Rootstock
- ✅ Built with clean, readable Solidity

---

## 🧠 Why Rootstock?

Rootstock (RSK) is a Bitcoin sidechain that supports **EVM-compatible smart contracts**. By building on Rootstock, you get:

- 🟡 Bitcoin's security model  
- 💸 Very low transaction fees  
- 🔐 Full transparency on a decentralized ledger  
- 💡 Solidity development with the power of Bitcoin  

---

## 🛠️ Getting Started

### 🔧 Installation

1. **Clone the repo**
```bash
git clone https://github.com/polyde948/Rootstock-Decentralized-Voting.git
cd Rootstock-Decentralized-Voting

2. Install dependencies



npm install

3. Install Truffle globally (if you haven't already)



npm install -g truffle


---

⚙️ Configure for Rootstock Testnet

In truffle-config.js, add this:

const HDWalletProvider = require('@truffle/hdwallet-provider');
const mnemonic = "YOUR_WALLET_MNEMONIC";

module.exports = {
  networks: {
    rootstock_testnet: {
      provider: () =>
        new HDWalletProvider(mnemonic, "https://public-node.testnet.rsk.co"),
      network_id: 31,
      gas: 2500000,
      gasPrice: 60000000,
    },
  },
  compilers: {
    solc: {
      version: "^0.8.0",
    },
  },
};

🪙 Use the RSK Testnet Faucet to get free RBTC.


---

🚀 Deploy to RSK Testnet

truffle compile
truffle migrate --network rootstock_testnet


---

🔎 Usage (Basic Contract Interactions)

Enter the Truffle console:

truffle console --network rootstock_testnet

Then interact:

let instance = await Voting.deployed();

// Create a poll
await instance.createPoll("Favorite Layer 1?", ["Rootstock", "Ethereum", "Solana"]);

// Vote (e.g., vote for Ethereum which is index 1)
await instance.vote(0, 1);

// View results
let results = await instance.getResults(0);
console.log(results.toString());

// Close poll
await instance.closePoll(0);


---

🔄 Functions Overview

Function	Description

createPoll(string, string[])	Starts a new poll
vote(uint pollId, uint optionId)	Casts a vote (one vote per address)
getResults(uint pollId)	Returns current vote counts
closePoll(uint pollId)	Closes the poll (creator only)
getPoll(uint pollId)	Returns the question and options



---

🧠 Ideas for Expansion

⏰ Auto-close polls after a time period

🛡️ Token-gated voting (ERC-20 or NFTs)

🔒 Anonymous voting with zk-proofs

🧮 Voting weight by token balance

🌐 Front-end DApp integration using ethers.js or web3.js

📊 Visual result dashboards with Chart.js or D3.js



---

🧪 Testing & Debugging

Run automated test scripts with:

truffle test

Or manually interact via the Truffle console.


---

📚 Resources

🧾 Full Technical Guide (Google Docs link you’ll share with Rootstock team)

📘 Rootstock Developer Docs

🧪 RSK Testnet Faucet

🧰 Truffle Documentation



---

🤝 Contributing

We welcome pull requests and feature suggestions!

To contribute:

1. Fork the repo


2. Create a branch (git checkout -b feature/xyz)


3. Commit your changes


4. Push and create a PR



Follow the Solidity Style Guide.


---

📄 License

This project is licensed under the MIT License — free to use, adapt, and build upon.


---

🙌 Acknowledgments

This project was built as part of the Rootstock Hacktivate program to showcase practical use of smart contracts for decentralized governance.

Built with 💛 on Rootstock by Nkanyiso Moyo


---
