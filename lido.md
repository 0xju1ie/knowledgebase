# Lido

- Most of this information is sourced from [here](https://lido.fi/static/Lido:Ethereum-Liquid-Staking.pdf).
- Community operated liquid staking service.
- Maintains infrastructure for its users.
- Does not lock user assets.
- Started when Phase 0 of ETH2 launched.
- DAO controlled.
  - DAO selects node operators.
  - DAO controls the smart contracts.
- Node operators never directly interact with user's tokens.
- Uses stETH as its liquid token.
- 10% of the stake return is taken and distributed to node operators, the DAO members, and the insurance pool.

## Architecture

- Managed by the DAO.
  - Members govern Lido to ensure efficiency and stability.
  - DAO also responsible for recruiting new users, node operators, and validators.
  - DAO is responsible for how Lido is marketed.
    - Promotional campaigns.
    - Educational content.
    - Affiliate Marketing.
  - DAO updates parameters (fees, rates, etc).
  - Approve incentives for parties that contribute towards DAO goals.
  - Propose and update Lido's implementation for incoming ETH2 features using DAO treasury funds.
  - Assign oracles who deliver rewards and slash rates to establish stETH balances.
  - Scout and recruit new node operators.
  - Boot badly performing node operators.
  - Manage DAO insurance and developer funds.
  - Manage withdrawals (once available on ETH2).
  - Response to emergencies.
- Lido is, at its core, a trust minimized set of ETH1 smart contracts.
- Lido consists of several parts.
  - stETH token.
  - Deposit and stETH minting.
  - Node operator registry.
  - Beacon chain oracles and stETH token balance updates.
  - Withdrawals (disabled until ETH2).
- When you deposit ETH, the contract gives you the equivalent amount of stETH.
- stETH can be held, trade, and sold like a normal token.
- Deposits are delineated by 32 ETH groupings (the minimum to stake).
- Funds are deposited to the Lido smart contract and then locked into the ETH Beacon chain.
  - RocketPool does the same.
- Since DAO chosen operators are considered trustworthy, they don't need to deposit collateral.
  - This is supplemented with slashing insurance.
  - This is more capital efficient.
- DAO appointed oracles handle cross chain communication.
  - The oracles monitor node operators' beacon chain staking accounts and submit data to the Lido's ETH 1.0 contracts.
  - When the oracles update, the system recalculates the amount of stETH. If the overall staking rewards are greater than the slashing penalties, the system registers profit.
    - When profit is registered, stETH balance is increased and Lido takes a 10% fee.
    - That 10% gets split between node operators and the DAO treasury.

## Incomplete. More coming soon.
