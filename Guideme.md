
📄 ROOTSTOCK DECENTRALIZED VOTING — FULL TUTORIAL SUBMISSION

🗳️ BUILDING A DECENTRALIZED VOTING SYSTEM ON ROOTSTOCK
By Nkanyiso Moyo | GitHub: https://github.com/polyde948/Rootstock-Decentralized-Voting

---

## 🚀 Overview & Motivation

**What problem does this solve?**

Centralized voting systems are often opaque, prone to manipulation, and require trust in a central authority. This project introduces a simple yet powerful **decentralized voting smart contract** built on the **Rootstock (RSK)** blockchain, enabling transparent, censorship-resistant voting — without middlemen.

**Who is this for?**

This guide is for:
- Web3 developers with basic Solidity knowledge
- DAO builders and governance tool creators
- Blockchain learners exploring Rootstock
- Hackathon participants and Ethereum devs interested in Bitcoin sidechains

**Prerequisites:**
- Node.js (v16+)
- Truffle Framework
- Metamask wallet or RSK wallet
- Familiarity with Solidity and JavaScript
- Basic understanding of smart contracts and Web3

---

## ⚙️ Architecture & Core Components

### 🧠 How the System Works

Each voting session (poll) is stored as a `struct` in Solidity containing:
- A **question** (e.g. “Who should be the next DAO leader?”)
- **Options** (list of candidates)
- A mapping of **votes per option**
- A mapping to **prevent double voting**
- Creator's address and active status

### 📊 Architecture Flow

User 🧑 │ ▼ Create Poll ➡️ Smart Contract 🛠 (on RSK) │ ▼ Voters Cast Votes (1 address = 1 vote) ➡️ Blockchain Storage 🗳 │ ▼ Get Live Results ✔️ or Close Poll 🚫 (Only creator)

There’s no backend — everything is **on-chain** on the **RSK testnet** for transparency and immutability.

---

## 🛠️ Step-by-Step Guide

### ✅ 1. Environment Setup

#### A. Clone the repo

```bash
git clone https://github.com/polyde948/Rootstock-Decentralized-Voting.git
cd Rootstock-Decentralized-Voting

B. Install dependencies

npm install

C. Install Truffle globally (if not already)

npm install -g truffle


---

🌐 2. Configure for Rootstock Testnet

Open truffle-config.js and add:

const HDWalletProvider = require('@truffle/hdwallet-provider');
const mnemonic = "YOUR WALLET MNEMONIC HERE";

module.exports = {
  networks: {
    rootstock_testnet: {
      provider: () => new HDWalletProvider(mnemonic, `https://public-node.testnet.rsk.co`),
      network_id: 31,
      gas: 2500000,
      gasPrice: 60000000
    }
  },
  compilers: {
    solc: {
      version: "^0.8.0"
    }
  }
};

📌 Replace the mnemonic with your RSK wallet’s seed phrase (testnet wallet).


---

🔧 3. Smart Contract Code

Here’s a simplified version of the smart contract (Voting.sol):

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Voting {
    struct Poll {
        string question;
        string[] options;
        mapping(uint => uint) votes;
        mapping(address => bool) hasVoted;
        bool isActive;
        address creator;
    }

    Poll[] public polls;

    function createPoll(string memory _question, string[] memory _options) public {
        Poll storage newPoll = polls.push();
        newPoll.question = _question;
        newPoll.options = _options;
        newPoll.isActive = true;
        newPoll.creator = msg.sender;
    }

    function vote(uint _pollId, uint _optionId) public {
        Poll storage poll = polls[_pollId];
        require(poll.isActive, "Poll is closed");
        require(!poll.hasVoted[msg.sender], "Already voted");
        poll.votes[_optionId]++;
        poll.hasVoted[msg.sender] = true;
    }

    function closePoll(uint _pollId) public {
        require(polls[_pollId].creator == msg.sender, "Only creator can close");
        polls[_pollId].isActive = false;
    }

    function getResults(uint _pollId) public view returns (uint[] memory) {
        Poll storage poll = polls[_pollId];
        uint[] memory results = new uint[](poll.options.length);
        for (uint i = 0; i < poll.options.length; i++) {
            results[i] = poll.votes[i];
        }
        return results;
    }

    function getPoll(uint _pollId) public view returns (string memory, string[] memory) {
        Poll storage poll = polls[_pollId];
        return (poll.question, poll.options);
    }
}


---

🔄 4. Compile & Deploy the Contract

truffle compile
truffle migrate --network rootstock_testnet

If successful, the terminal will output something like:

Deploying 'Voting'
------------------
> contract address: 0x123abc...def
> blocks: 2
> gas used: 1,234,567
> Saving migration...
> Saving artifacts...

🎉 Your contract is now live on Rootstock Testnet!


---

💻 Usage: Interacting With the Contract

Use Truffle console:

truffle console --network rootstock_testnet

Then interact:

let instance = await Voting.deployed()

// Create a poll
await instance.createPoll("Best blockchain?", ["Rootstock", "Ethereum", "Solana"])

// Vote (e.g., vote for Ethereum = index 1)
await instance.vote(0, 1)

// Check results
let res = await instance.getResults(0)
res.toString()  // e.g., [0,1,0]

// Close poll
await instance.closePoll(0)


---

📷 Optional UI (Bonus Step)

You can build a front-end using React + ethers.js. Sample:

npm install ethers

Then use:

const provider = new ethers.providers.JsonRpcProvider("https://public-node.testnet.rsk.co");
const contract = new ethers.Contract(contractAddress, abi, provider);


---

🧠 Advanced Features to Add

1. Time-based polls

Add a uint deadline to each poll and auto-close after a time.



2. Token-gated voting

Require holding a specific token to vote.



3. Anonymous voting

Use zk-SNARKs or off-chain commitments.



4. Result visualization

Display bar charts using Chart.js in your React app.



5. Multi-language support

Add i18n for global reach.





---

🧰 Troubleshooting & Tips

Issue	Solution

Gas estimation error	Try reducing gas value in truffle-config.js
Wallet not funded	Use RSK Faucet
HDWalletProvider not found	Run npm install @truffle/hdwallet-provider
Contract not found	Ensure correct network and contract name
Vote not updating	Ensure you haven’t voted already in that poll



---

🤝 Contribution Guidelines

We welcome contributors!

1. Fork the repo


2. Create a feature branch: git checkout -b feature/add-timers


3. Make your changes


4. Submit a PR with a clear description



Follow Solidity Style Guide and test your changes using Truffle.


---

📚 References & Resources

GitHub Repo: https://github.com/polyde948/Rootstock-Decentralized-Voting

Rootstock Docs: https://developers.rsk.co

RSK Faucet: https://faucet.testnet.rsk.co/

Truffle Framework: https://trufflesuite.com

Web3 Intro: https://ethereum.org/en/developers/docs/web2-vs-web3/

OpenZeppelin Contracts: https://docs.openzeppelin.com/contracts



---

✅ Conclusion

By leveraging Rootstock’s secure and low-cost smart contracts, we’ve built a censorship-resistant voting system that is fully decentralized. This project shows how governance tools can operate without trusting any third party — a step toward truly decentralized decision-making.


---

Built with 💛 on Bitcoin’s smart contract platform, Rootstock.

Nkanyiso Moyo
GitHub: https://github.com/polyde948/Rootstock-Decentralized-Voting
