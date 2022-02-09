# Rocketpool Smart Nodes

## Nodes and Node Operators

* A single node can run multiple minipools (if you have the coin).
  * RocketPool claims that beta testers were able to run hundreds of minipools on a single node.
* Nodes can either be a VM or a physical computer.
* Node operators manually set up minipools.
* Node operators must make sure their nodes are secure and cannot be easily hacked into.
* Node operators have to make sure their node doesn’t go offline for a long period of time (else get their insurance coin taken).
  * If you end up loosing ETH by the time you exit the minipool, all of the lost ETH comes out of your share.
    * If you try to exit the pool when there is only 30 ETH, the staking pool will be given 16 ETH and you will be given 14 ETH.
    * If you somehow go below 16 ETH, all of it is given to the staking pool, and your RPL is taken.
* Nodes earn half of the minipool staking rewards (makes sense, you put up half the coin).
* Nodes also earn extra commission in the form of RPL token.
* You can stake RPL like Ethereum to make more RPL.
* You can vote on Rocket Pool’s upcoming changes via the Prometheus DAO.
* The Prometheus DAO is also how they distribute RPL.

## Requirements

* Linux or macOS
  * Their installer page says they have a Windows client which is missing from their documentation.
* ETH1 and ETH2 Node clients.
  * Can be either local clients or nodes-as-a-service.
* 10Mbps internet (up and down).
* No data cap (uses upwards of 1.4TB / mo).
* 8GB of RAM.
* 2 CPU cores minimum, 4+ cores recommended.
* 1TB SSD storage minimum, 2 TB recommended.

## Installation and Configuration

* This is all automated via the [RocketPool CLI](https://github.com/rocket-pool/smartnode/tree/master/rocketpool-cli).
* All installation files can be found in their [`smartnode-install` repo](https://github.com/rocket-pool/smartnode-install).
* Docker and Docker Compose are required.
  * Docker simplifies installation.
  * Docker-Compose simplifies communication between programs.
    * There are different compose build files for arm64 and amd64 builds, but they look identical.
* All of the settings for both the [Prater testnet](https://github.com/rocket-pool/smartnode-install/blob/master/amd64/rp-smartnode-install/network/prater/config.yml) and the [mainnet](https://github.com/rocket-pool/smartnode-install/blob/master/amd64/rp-smartnode-install/network/mainnet/config.yml) are stored in the repo as YAML files.
* Separate compose files exist for both the [testnet](https://github.com/rocket-pool/smartnode-install/blob/master/amd64/rp-smartnode-install/network/prater/config.yml) and the [mainnet](https://github.com/rocket-pool/smartnode-install/blob/master/amd64/rp-smartnode-install/network/mainnet/docker-compose.yml).
  * There’s a [fallback compose file](https://github.com/rocket-pool/smartnode-install/blob/master/amd64/rp-smartnode-install/network/mainnet/docker-compose-fallback.yml) for the mainnet.
  * Both [testnet](https://github.com/rocket-pool/smartnode-install/blob/master/amd64/rp-smartnode-install/network/prater/docker-compose-metrics.yml) and [mainnet](https://github.com/rocket-pool/smartnode-install/blob/master/amd64/rp-smartnode-install/network/mainnet/docker-compose-metrics.yml) have metric compose files for a grafana dashboard.

## Operation Modes

Nodes can run in Docker, Hybrid, or Native mode.

### Docker Mode

Uses Docker containers to run duties of the node. Runs the following containers on your system.

* `rocketpool_api` - This holds the actual functionality that the Smartnode provides when you interact with it via Rocket Pool's command-line interface (CLI).
* `rocketpool_node` - This is a background process that will periodically check for and claim RPL rewards after a reward checkpoint (if you have auto-claim enabled, more on this later), and is responsible for actually staking new validators when you create a minipool.
* `rocketpool_watchtower` - This is used by Oracle Nodes to perform oracle-related duties. For regular node operators, this will simply stay idle.
* `rocketpool_eth1` - This will be your ETH1 client, such as Geth, or a small proxy that routes ETH1 requests to a light client like Infura or Pocket.
* `rocketpool_eth2` - This will be your ETH2 beacon node client.
* `rocketpool_validator` - This will be your ETH2 validator client, which is responsible for your validator duties (such as attesting to blocks or proposing new blocks).

A few things to note:

* This is the mode that RocketPool recommends you run when you want to get a node working quickly.
* Is the most “hands-off” approach, requires little user intervention (other than updates).
* Some of the Docker containers have to run as root. Some users will not be happy about this as it could be a security hole, but if you have everything properly secured it should be fine.

### Hybrid Mode

This mode still uses Docker, but omits the ETH1 and ETH2 clients from Docker, and instead uses the Etherum clients the user specifies. If the user specifies an ETH2 client but not an ETH1 client, or vice versa, the CLI will spin up the missing client automatically.

### Native Mode

Bypasses Docker entirely and installs each program as a daemon on your system natively.

* Requires the user to manually install and keep up to date each part of the smart node.
* Offers the most flexibility as the user can change configuration as needed.
* Should only be used by experienced system administrators.

## Code Info

* The code is over 32k lines long.
* Can be found [here.](https://github.com/rocket-pool/smartnode)
* Written in Go, designed to run on Docker (though it doesn't have to).

## Misc

* When you deposit money into the node, it goes to the [Beacon Chain Deposit Contract](https://etherscan.io/address/0x00000000219ab540356cbb839cbe05303d7705fa#code).
  * This contract is currently 9.1 million ETH, valued at $25.8 Billion.
