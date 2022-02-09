# Rocketpool

## Extremely High Level Overview

![Figure 1](https://miro.medium.com/max/875/0*_sJ3t7opc0wDcDDI.png)

- Community Owned.
- Base layer protocol for decentralized and trustless ETH2 staking.
- Designed for stakers of any capacity and size. Start with as little as 0.01 ETH.
- Decentralized Governance: Run by its users using a network DAO.
- RPL Token: used as a slashing insurance, for network governance, and as a reward token for node operators.
- Node Staking: Stake with as little as 16 ETH and increase ROI. Operators earn commission and rewards in a permissionless fashion.
- Smart Contracts: Trustless smart contracts connect the components together on Ethereum blockchain.
- Oracle DAO: A unique decentralized oracle DAO network for the protocol connecting the beacon chain the main ETH chain.
- rETH tokenised staking: A staked, interest earning wrapper of ETH that can be exchanged at any time.

## Tokenized (Liquid) Staking with rETH

![Figure 2](https://miro.medium.com/max/875/1*9xqyD0jgovV2z2YZIPUHhA.png)

- When you deposit ETH to RocketPool, you get rETH in return.
- rETH can be sold an trade just like regular ETH, while allowing you to earn interest on your staked ETH.
- Depositing and staking your ETH is a single transaction that RocketPool protocol handles.
- rETH can be used with dApps, exchanges, wallets, or anyone who wants to build upon RocketPool.
- RocketPool allows you to trade back your rETH for ETH, unlike the (current) state of staking without Rocketpool.
- RocketPool is a decentralized liquid staking platform.
- They follow all the traditional rules of a liquid staking platform, but have participants host their own RocketPool nodes rather than having a central node.
- Node hosts have to have 16 ETH plus 1.6 ETH equivalent of RPL token to run a node.
  - Anyone can join as long as they have the cash, hardware, and know-how.
  - 1.6 ETH is roughly 137 RPL token (as of 1/14/2022).
  - This RPL deposit acts as insurance to make sure the node operator behaves and properly participates.
  - This allowed them to participate in a DAO to vote on decisions.
    - This DAO is called the Protocol DAO.
- These nodes are used when a user wants to stake without a node. All ETH is distributed across all nodes.
- Node operators get more rewards, in the form of the RPL token as well as a return rate of 6.36% APR.
- Liquid stakers get a return rate of 4.33% APR.

## Protocol vs Staking as a Service

- Staking as a service is a well established business model.
- RocketPool sees itself as an extension to that service, not a competitor.
- This means that ETH staking companies, like Bison Trails or Gemini, can use RocketPool like a traditional user.
- RocketPool is designed for two users - those who want to use liquid staking and those who want to stake ETH via nodes.

## Staking

- User puts up `n` ether (minimum of 0.01 ETH) which is added to a pool (which is just a wallet address I think?).
- User gets rETH back in exchange for their ETH.
- They can either sell the rETH or keep it and exchange it back for ETH later.

## MiniPools

- Staking occurs via validators.
- When a user wants to run a node they need 16 ETH plus 1.6 ETH worth of RPL tokens.
  - The 16 ETH gets pooled with another 16 ETH from the staker’s pool.
    - This is called a **minipool**.
  - 1.6 ETH’s worth of RPL tokens acts like insurance.
    - If your node is slow and looses ETH, the RPL acts as insurance so that the other stakers don’t loose money.
    - This also allows you to participate DAO votes about smart contract changes (called the Prometheus DAO internally).
- To Ethereum’s chain, a minipool looks like a normal node.
- If a node operator wants to leave the minipool, the smart contracts handle moving the ETH around so the operator is not responsible.

## RPL

- RocketPool flags a checkpoint every 28 days.
- This checkpoint mints new RPL.
- Current inflation rate of RPL is 5% per year.
- For the first year of operation, with a total supply of 18,000,000 RPL, the protocol will mint **900,000 RPL.**
- 70% (630,000 tokens) gets distributed to node operators (about 48,300 tokens per 28 days).
- When operators set up a node, they can specify an address for the distributed rewards to go to.
- If you set up a Docker node, the reward should be automatically claimed and set to the wallet.
  - You have 28 days to claim the RPL before it disappears.
- You can choose to wait if it will cost you more to claim your RPL than RPL you have.
  - Gas fees apply to RPL.

## DAOs

### Why use DAOs?

- Permissioned Entry: New nodes can only enter the group after a consensus is reached within the existing group, only after providing they meet certain criteria.
- Transparent consensus: All decisions must go through an on-chain proposal. Members can collectively vote to kick nodes who aren't doing their job and the wider RP community can always stay up on a new upgrade to the node group.
- Permissionless incentives: Leveraging a DAO allows RPL to be directed to on-chain pool of node operators rather than having to distribute rewards earned from performing duties.

### Protocol DAO

- Responsible for RPL governance.
  - Inflation control, creates new RPL tokens.
  - Reward distribution to both DAOs and node operators.
  - RPL Auctions. Min/Max bids are configurable.
  - Node governance. Min/Max RPL staking.
  - Setting commission fees for node operators.
  - Setting min/max deposit amount of ETH for rETH.

### Oracle DAO

- The RocketPool Team has an OracleDAO which does a bunch of important sensitive stuff.
- Being a DAO member is a paid position, like a company chair member.
- Currently between 15 and 20 people.
- Members of OracleDAO have to be invited and put up a large amount of RPL tokens to buy in.
  - Steve thinks its around $500k worth of tokens.
- Members of the DAO vote on the status of other members. Majority vote must be met.
  - Members can be voted off.
  - Members have to be voted on after being invited.
  - You can only leave with approval.
  - Replacements have to be voted on.
- Member duties cost money per day.
- Members get paid 15% of the RPL inflation.
- Next year (2023), RocketPool will add 900k RPL tokens to the economy, OracleDAO gets 135k of that. Each DAO member gets 9600 tokens.
  - 9600 tokens is roughly $380k.
  - Spreadsheet Steve sent with inflation numbers [here](https://docs.google.com/spreadsheets/d/1Wl3EukDALcd8nBQQkMhzXr5WfwmEj264YPfch9AJN30/edit#gid=944682517).
- Responsible for
  - Calculates the exchange rate of ETH to rETH.
  - Calculates the RPL to ETH ratio.
    - Must be agreed upon by a majority of the DAO members.
  - Vote on contract upgrades.
  - Vote on changing settings.
  - Calculating rewards based on minipool validator performance.
  - Mark validators as exited/withdrawn when they perform these actions on the beacon chain.
  - Make sure the protocol is always lively and staking as much ETH from the deposit pool as it can. Oracle DAO members can create unbonded minipool validators that don't need the 16 ETH to be matched.

![Figure 3](https://miro.medium.com/max/1400/0*VtX5Q3POH8SPAODs.png)
