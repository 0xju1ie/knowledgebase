---
description: Chandler's Crypto Crash Course
---

# Crypto Crash Course

## BlockChain

- A blockchain is effectively a public database that is synced across multiple nodes.
  - Also could be thought of as a public record of transactions like the movement of money, movement of assets, and the exchange of information.
- A “node” is a computer running node server software.
- A “block” is some data that has been grouped together.
- The “chain” is the history of all blocks.
  - The chain is persistent and shared across all nodes.
    - In simpler terms, the all data is the same on all computers running on the blockchain.
- The nodes on the blockchain decide if the block of data is valid.
  - If yes, as in the network agrees that all the data in the block is valid, then it gets added to the chain.
  - If not, the next block gets checked and the current block gets thrown out.
- When a new block gets added to the chain, some cryptographic function (usually RSA) verify that the chain history has not been altered.
  - A majority of the nodes on the network have to agree on the chain. If a majority is met, the nodes are forced to use the new chain.
  - Changing the chain history is how people cheat, as someone with more nodes can cheat the history and block out all other nodes on the chain with the modified history that they are trying to pass on as the correct and valid blockchain. This is called a 51% attack.
- Blockchains use a “consensus protocol” to keep all the nodes in sync. They assume no trust to each node (trustless), and require the rest of the nodes to agree on a state for the blockchain history.
  - There are different consensus protocols.
    - Proof-of-work (GPU and CPU power)
      - Uses lots of computing power since computers are competing to create blocks.
      - Ethereum 1.0
      - Bitcoin
    - Proof-of-stake (validators)
      - The one we care about.
      - Avalanche
      - Ethereum 2.0
    - Proof-of-storage
      - Chia
    - Proof-of-authority

## Proof of Stake

- Type of consensus mechanism that uses distributed consensus.
- Users have to stake a specified amount of currency to run a node and earn more currency.
  - Currently you need 32 ETH ($104k as of 01/14/2022) to stake on Ethereum.
  - Currently you need 2000 AVAX ($181k as of 01/14/2022) to stake on Avalanche.
- Nodes validate transactions and create new blocks to agree on the state of the network.
- Validators (nodes) are chosen at random to create new blocks.
  - Are responsible for checking and confirming the blocks they don’t create.
- If a user’s node goes offline or slows down, the user can loose some of their staked currency for failing to validate.
  - On Ethereum 2.0, if a user deliberately pushes or successfully validates a bad block, they loose all their stake.
  - On Avalanche, you just don’t get a reward.
- More currency is earned by correctly validating blocks as well as creating new blocks.
  - More on how validation works [here](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/#how-does-validation-work).

## Ethereum

- Ethereum is the blockchain technology that is most popular as of 2022.
- Has a cryptocurrency attached, known as “ether” or ETH.
- Was built to be a “world computer”, as in all nodes have to agree on state like a normal blockchain, but code can be run on the blockchain.
  - This code is called a “smart contract”.
- New tokens can be minted on the Ethereum blockchain, called ERC-20 tokens.
  - For example, USDC, which is a token where 1 USDC roughly equals $1.
  - Two other examples are RPL and rETH, which RocketPool uses for liquid staking (more on that later).
- Also know for NFTs, which are effectively certificates of ownership for specific digital (or physical) goods.
- Currently using Proof of Work to create new ether.
- Will be moving to a Proof of stake system (like how Avalanche uses now) with the move to Ethereum 2.0.
  - If you move your coins to ETH2, you can’t move them back to ETH 1.
- Introduced the concept of a Digital Autonomous Organization, which is a fully democratized company that uses smart contracts and the blockchain to make decisions.

## Smart Contracts

- Code that automatically executes when contract terms are met on the blockchain.
- Written in [Solidity](https://soliditylang.org/).
  - Frameworks like [Truffle](https://trufflesuite.com/index.html) and [Hardhat](https://hardhat.org/) exist to assist development and testing.
- Basically they are programs that run on the blockchain that cannot be changed.
- Require vigorous testing before deployment.
- They will always run when the conditions are met.
- There is no one computer they run on. They run on the entire blockchain network.
- All inputs and outputs are public.
- You input currency into the smart contract and they create an output.
- Running a smart contract cost currency, usually referred to as “gas”.
  - This applies to all transactions, not just ones done by a smart contract.
  - Gas fee gets burned on Avalanche.
  - On Ethereum, you can add a tip to the gas fee to make your transaction faster.
- Smart contracts can only interact with data within the blockchain.
  - There is a concept of an [oracle](https://ethereum.org/en/developers/docs/oracles/) on Ethereum that allow you to get data outside the blockchain via smart contracts. Not sure if this exists on Avalanche (yet).

## Digital Autonomous Organizations (DAOs)

- A company/organization who’s decisions are managed by a group of individuals democratically via stake in a cryptocurrency or other blockchain asset.
- Smart contracts are used to manage the DAO.
- “An online community with a shared crypto wallet.” - [Aragon](https://blog.aragon.org/what-is-a-dao/)
- Decisions are voted on by DAO members.
- Votes are tallied and outcome is done automatically by smart contracts.
  - Trustless.
- Funds are distributed and moved automatically.
- All activity is transparent and kept on the blockchain.
- Examples from [Ethereum’s docs](https://ethereum.org/en/dao/#dao-examples).
  - A charity – you can accept membership and donations from anyone in the world and the group can decide how they want to spend donations.
  - A freelancer network – you could create a network of contractors who pool their funds for office spaces and software subscriptions.
  - Ventures and grants – you could create a venture fund that pools investment capital and votes on ventures to back. Repaid money could later be redistributed amongst DAO-members.

## [UTXO](https://www.investopedia.com/terms/u/utxo.asp)

- Amount of currency remaining in an account after a transaction is complete.
  - Think of it like change someone receives after conducting a cash transaction.
- The amount in your wallet is actually a sum of multiple UTXOs.
- Processed continuously.
- Responsible for both the beginning and end of a transaction.
- When a transaction is completed, any unspent outputs are deposited back into a database as inputs which can be used later for another transaction.
- Specific type database is used.
  - UTXO Database.
- Database is set to zero to start.
- As transactions occur, the database becomes populated with change records from transactions.
- When the transaction finishes and there is leftover currency, the value gets added back to the database as an input.
- Here is a primitive functional explanation.
  - Say Kyle has 2000 AVAX, and he wants to buy a car that costs roughly 300 AVAX.
  - His AVAX is (probably) not a single UTXO. For example, let’s say its four UTXOs worth 500 AVAX each.
  - When Kyle says he wants to buy the car for 300 AVAX, 500 AVAX gets sent to the car dealer.
  - The chain then mints a new UTXO and sends it back to Kyle. That new UTXO would be worth 200 AVAX to make up the difference.
- The above example does not account for transactions fees.
- The blockchain accounts for transaction fees when minting new UTXOs.
- Here is the formula for a new UTXO mint.
  - **New UTXO** = (Sum of UTXOs in the transaction) – (Transaction amount) – (Transaction fee)
  - For the above example: **New UTXO** = (500) - 300 - 0 = 200, assuming no transaction fee.

## Staking

### Self Staking

- Run your own staking node with your own currency.
- Requires the node to have a lot of currency deposited to it.
  - Currently you need 32 ETH ($104k as of 01/14/2022) to stake on Ethereum.
  - Currently you need 2000 AVAX ($181k as of 01/14/2022) to stake on Avalanche.
- Locks your currency until the staking period is up.
  - On Ethereum, you can’t pull out your money yet because the functionality hasn’t been added yet. Could be weeks or years, no one knows.
  - For Avalanche, the minimum time is 2 weeks and the maximum time is 1 year.

### Exchange Staking (Staking Pool)

- You put your currency into a staking pool via a centralized service.
- You can withdraw your money at any time.
  - Exchange pool can only stake 60% of the deposited ETH so that users can still pull out their currency when they want. This causes the return rate to be lower than liquid staking or self staking.
- Lacks transparency and requires you to trust the service.
- Is not decentralized.

### Liquid Staking

- Allows user to stake any amount in exchange for a tokenized version of the staked funds that can be traded as a normal token.
- Users deposit to a third party application, they receive a derivative ERC-20 token.
  - RocketPool has rETH.
  - Lido has stETH.
- Users can exchange their derivative token back for currency whenever they want.
- The value of the derivative token goes up over time.
  - This is because the amount of currency they deposited goes up over time.
  - Say Julie deposits 1 ETH into RocketPool and she gets back 1 rETH. Say that after a few months she now has 1.1 ETH staked into RocketPool. Her 1 rETH would be equivalent to that 1.1 ETH.
    - This is a gross oversimplification of the market.
  - As of 1/14/2022, 1 ETH equal to 0.98 rETH.
- Users outside the pool can buy derivative tokens on exchanges to indirectly participate in the pool.
- Rewards are given out in the form of a reward token.
  - RocketPool has RPL.
  - This token can be traded on markets and has value as well.
  - As of 1/14/2022, 1 RPL is about $38.36.
- This is still has the issue of being centralized.
  - RocketPool solves this.
