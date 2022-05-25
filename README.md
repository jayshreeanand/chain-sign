# Chainlink powered e-Document verification and signing using smart contracts, IPFS and chainlink APIs

[LIVE DEMO](https://chain-sign-demo.herokuapp.com)

Built with:

- [Next.js](https://nextjs.org)
- [TypeScript](https://www.typescriptlang.org)
- [Hardhat](https://hardhat.org)
- [TypeChain](https://github.com/dethcrypto/TypeChain)
- [Ethers.js](https://docs.ethers.io/v5/)
- [useDApp](https://usedapp.io)
- [Chakra UI](https://chakra-ui.com)
- [Moralis](https://moralis.io/)

## Inspiration

Chainsign adds signing and verifying e-contract and document function to the blockchain. This solves legal issues involved with documents through use of chainlink and smart contracts

With blockchain, documents are embedded in digital code and stored in transparent, shared databases, where they’re protected from deletion, tampering and revision. Every agreement, every task, and every payment would have a digital record and signature that could be identified, validated, stored, and shared. Intermediaries like lawyers, brokers and institutions might no longer be necessary. Individuals and organizations would freely transact and interact with one another with little friction. This is the immense potential of blockchain.

## What it does

Document upload flow

![Chainlink](https://user-images.githubusercontent.com/5363211/170849311-7afa8745-4c78-4c28-a234-b4301c0ea753.jpeg)

Certificates are issued by an authority, such as an education institute, legal institution stored oncentralized document management server, or on a distributed file system like IPFS and signed with a cryptographic function. The content hash and certificate’s metadata hash are then stored on the blockchain digital ledger and attached to the user’s digital identity as a smart contract address that stores this information This represents a sort of unique authenticity token, which identifies the document in a non-questionable way.

- Signer has to LogIn
- After LogIn has been successful you can upload a document.
- You can sign uploaded document.
- DocumentHash / Meta data hash is generated. DocumentHash should be stored on Blockchain. Signed document is stored on IPFS.

Document verification flow

![Verification flow](https://user-images.githubusercontent.com/5363211/170849621-b2091dd8-5a4b-481e-a7c4-c488b463a8d3.jpeg)

Users who need to verify their certificates with a third party do so by sharing the authenticity token (that is, the file contract address), which contains all the necessary information to verify that the document exists and is authentic and not counterfeited.

The user retrieves the certificate to verify from its location and initiates a new transaction on the blockchain network, transferring the authenticity token to the verification authority. The authority obtains the signed content and metadata of the certificate being verified and then compares them with the equivalent hash values from the off-chain copy. If the values match, the document is verified
End-to-end implementation of the following Chainlink features using Hardhat development environment and Next.js frontend framework:

Built with:

- [Next.js](https://nextjs.org)
- [TypeScript](https://www.typescriptlang.org)
- [Hardhat](https://hardhat.org)
- [TypeChain](https://github.com/dethcrypto/TypeChain)
- [Ethers.js](https://docs.ethers.io/v5/)
- [useDApp](https://usedapp.io)
- [Chakra UI](https://chakra-ui.com)
- Linting with [ESLint](https://eslint.org)
- Formatting with [Prettier](https://prettier.io)

![Document upload and signing flow](https://user-images.githubusercontent.com/5363211/170849311-7afa8745-4c78-4c28-a234-b4301c0ea753.jpeg)

![Verification flow](https://user-images.githubusercontent.com/5363211/170849621-b2091dd8-5a4b-481e-a7c4-c488b463a8d3.jpeg)

## Requirements

- [Node](https://nodejs.org/en/download/)
- [Yarn](https://classic.yarnpkg.com/en/docs/install/#mac-stable)
- [Git](https://git-scm.com/downloads)

In order to use the frontend portion of the demo application you will need

- A crypto wallet such as [Metamask](https://metamask.io/) or [Coinbase Wallet](https://www.coinbase.com/wallet)
- Test $LINK for the relevant testnet. You can get some at the [Chainlink Faucets](https://faucets.chain.link/) page.
- Test $ETH to pay for gas costs. You can get some at the [Chainlink Faucets](https://faucets.chain.link/) page.

## Quick Start

Clone the repo and install all dependencies:

```bash
git clone https://github.com/hackbg/chainlink-fullstack
cd chainlink-fullstack

git submodule init
git submodule update

yarn install
```

Start up the local Hardhat network and deploy all contracts:

```bash
yarn chain
```

In a second terminal start up the local development server run the front-end app:

```bash
yarn dev
```

To interact with the local network, follow this step-by-step guide on how to use [MetaMask with a Hardhat node](https://support.chainstack.com/hc/en-us/articles/4408642503449-Using-MetaMask-with-a-Hardhat-node).

If you've set the mnemonic from MetaMask the first 20 accounts will be funded with ETH.

## Environment Variables

To make setting environment variables easier there are `.env.example` files in the `hardhat` and `frontend` workspaces. You can copy them to new `.env` files and replace the values with your own.

#### Hardhat

| Name                | Description                                                                                                                                                                                                                 |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `NETWORK_RPC_URL`   | Required to deploy to public networks. Obtain from [Infura's site](https://infura.io).                                                                                                                                      |
| `MNEMONIC`          | Used to derive accounts from wallet seed phrase, ie Metamask. The first account must have enough ETH to deploy the contracts, as well as LINK which can be obtained from [Chainlink's faucets](https://faucets.chain.link). |
| `PRIVATE_KEY`       | Alternative to using mnemonic. Some changes are required in `hardhat.config.js`                                                                                                                                             |
| `ETHERSCAN_API_KEY` | Verify contract code on Etherscan.                                                                                                                                                                                          |

#### Front-end

| Name                     | Description                       |
| ------------------------ | --------------------------------- |
| `NEXT_PUBLIC_INFURA_KEY` | Read-only mode and WalletConnect. |

## Deploy Contracts

This will run the deploy scripts to a local Hardhat network:

```bash
yarn deploy
```

To deploy on a public network:

```bash
yarn deploy --network kovan
```

## Auto-Funding

The Hardhat project will attempt to auto-fund any newly deployed contract that uses Any-API or VRF, which otherwise has to be done manually.

The amount in LINK to send as part of this process can be modified in this [Hardhat Config](https://github.com/hackbg/chainlink-fullstack/blob/main/packages/hardhat/helper-hardhat-config.ts), and are configurable per network.

| Parameter  | Description                                       | Default Value |
| ---------- | :------------------------------------------------ | :------------ |
| fundAmount | Amount of LINK to transfer when funding contracts | 1 LINK        |

If you wish to deploy the smart contracts without performing the auto-funding, run the following command when doing your deployment:

```bash
yarn deploy --tags main
```

## Test

If the test command is executed without a specified network it will run locally and only perform the unit tests:

```bash
yarn test:contracts
```

Integration tests must be run on a public testnet that has Chainlink oracles responding:

```bash
yarn test:contracts --network kovan
```

For coverage report:

```bash
yarn coverage:contracts
```

## Verify on Etherscan

You'll need an `ETHERSCAN_API_KEY` environment variable. You can get one from the [Etherscan API site.](https://etherscan.io/apis)

```bash
npx hardhat verify --network <NETWORK> <CONTRACT_ADDRESS> <CONSTRUCTOR_PARAMETERS>
```

example:

```bash
npx hardhat verify --network kovan 0x9279791897f112a41FfDa267ff7DbBC46b96c296 "0x9326BFA02ADD2366b30bacB125260Af641031331"
```

## Format

Fix formatting according to prettier config in the respective workspace:

```bash
yarn format:frontend
yarn format:hardhat
```

## Lint

```bash
yarn lint:frontend
```

## Testnet Contracts

This repo includes deployed and verified contracts on Kovan and Rinkeby so the front-end can run without the need to deploy them.

Once the `deploy` command is executed on any network the contracts config will be overwritten and you can start from scratch with your own deployments.

#### Kovan

| Name                   | Address                                                                                                                          |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `PriceConsumerV3`      | [0x01E2C7cA6D6A82D059287Cb0bC43a39Cd0ff4B00](https://kovan.etherscan.io/address/0x01E2C7cA6D6A82D059287Cb0bC43a39Cd0ff4B00)      |
| `FeedRegistryConsumer` | [0xB9ebb63D4820c45a2Db09d71cefA24daBd047b50](https://kovan.etherscan.io/address/0xB9ebb63D4820c45a2Db09d71cefA24daBd047b50)      |
| `APIConsumer`          | [0x14005AB90bc520E20Ffd7815Cae64372abb6b04d](https://kovan.etherscan.io/address/0x14005AB90bc520E20Ffd7815Cae64372abb6b04d)      |
| `RandomNumberConsumer` | [0xF9556187bf86823Cf0D7081625F97391642Fc242](https://kovan.etherscan.io/address/0xF9556187bf86823Cf0D7081625F97391642Fc242#code) |
| `RandomSVG`            | [0xb4Bac68d9Fa99D2852E5dFb124be74de2E8c4F76](https://kovan.etherscan.io/address/0xb4Bac68d9Fa99D2852E5dFb124be74de2E8c4F76)      |

#### Rinkeby

| Name                   | Address                                                                                                                       |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `PriceConsumerV3`      | [0x4998Bd433216bBc56976BCb4Fe5AA240bA766763](https://rinkeby.etherscan.io/address/0x4998Bd433216bBc56976BCb4Fe5AA240bA766763) |
| `APIConsumer`          | [0x43a87559277fd5F6F1AdC6e6331998899634e9Aa](https://rinkeby.etherscan.io/address/0x43a87559277fd5F6F1AdC6e6331998899634e9Aa) |
| `RandomNumberConsumer` | [0xA0e617aaA36Ff4A6bf61C4Ce2Ed66822B1e24726](https://rinkeby.etherscan.io/address/0xA0e617aaA36Ff4A6bf61C4Ce2Ed66822B1e24726) |
| `RandomSVG`            | [0xeC6CcE025e538D12E52D8C90181849B099a776A3](https://rinkeby.etherscan.io/address/0xeC6CcE025e538D12E52D8C90181849B099a776A3) |

## References

- [Chainlink Docs](https://docs.chain.link)
- [Chainlink Hardhat Box](https://github.com/smartcontractkit/hardhat-starter-kit)
- [Scaffold ETH](https://github.com/scaffold-eth/scaffold-eth/blob/nextjs-typescript)
