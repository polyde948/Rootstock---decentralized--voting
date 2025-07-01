*🗳️ Building a Decentralized Voting Smart Contract on Rootstock*

*Overview*  
This tutorial walks through building and deploying a simple decentralized voting system using Solidity on Rootstock (RSK). The contract allows users to create polls, vote transparently, and see results — all on-chain with RBTC.

We’ll cover:  
- Project architecture  
- Writing the smart contract  
- Deploying on Rootstock testnet  
- Testing functionality  
- How to adapt or expand the system

GitHub Repo: [Add your repo link here]

---

*⚙️ Architecture & Smart Contract Structure*

The system consists of:

- A *Poll struct* that stores:
  - The question
  - Options
  - Vote count for each option
  - Whether the poll is active
  - Creator’s address
- *Mappings* for polls by ID and for addresses that already voted
- Access control so only poll creators can close polls

```solidity
struct Poll {
    string question;
    string[] options;
    mapping(uint => uint) votes;
    mapping(address => bool) hasVoted;
    bool isActive;
    address creator;
}
```

---

*🔧 Key Functions Explained*

- `createPoll(string memory question, string[] memory options)`  
  Creates a new poll with multiple options.

- `vote(uint pollId, uint optionIndex)`  
  Lets users vote once per poll. Prevents double voting using address tracking.

- `getResults (uint pollId)`  
  Returns vote counts for each option.

- `closePoll(uint pollId)`  
  Only the creator can close the poll and prevent further votes.

- `getPoll(uint pollId)`  
  Fetches question and options for UI display.

---

*🚀 Deploying to Rootstock Testnet*

1. *Environment Setup*
   - Install Truffle: `npm install -g truffle`
   - Create a new Rootstock-compatible project.

2. *Compile Contract*
   ```bash
   truffle compile
   ```

3. *Deploy to Testnet*
   Configure `truffle-config.js` for Rootstock testnet, then:
   ```bash
   truffle migrate --network rootstock_testnet
   ```

4. *Fund Your Wallet*
   Use a Rootstock faucet to get RBTC testnet tokens.

---

*🧪 How to Test the Voting System*

1. *Create a Poll*
   ```solidity
   createPoll("Best web3 platform?", ["Rootstock", "Ethereum", "Solana"]);
   ```

2. *Vote*
   ```solidity
   vote(0, 1); // Votes for Ethereum
   ```

3. *Fetch Results*
   ```solidity
   getResults(0);
   ```

4. *Close Poll*
   ```solidity
   closePoll(0);
   ```

---

*📈 Expanding the Project*

You can extend the system by adding:

- Time-based voting (auto-close after X days)
-- Anonymous voting with zk-proofs
- Token-gated polls using ERC-20 or NFT ownership
- UI dashboard with web3.js or Ethers.js integration

---

*✅ Conclusion*

This decentralized voting smart contract shows how blockchain can power transparent, censorship-resistant governance. Built on Rootstock with RBTC, it’s a simple but powerful tool any developer can build on or adapt.

GitHub Repo: [https://github.com/polyde948/Rootstock---decentralized--voting]

---

!
