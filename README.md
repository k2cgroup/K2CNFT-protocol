## Smart contracts for K2CNFT protocol

Consists of:

- Exchange v2: responsible for sales, auctions etc.
- Tokens: for storing information about NFTs
- Specifications for on-chain royalties supported by K2CNFT

## Compile, Test, Deploy

```shell
yarn
yarn bootstrap
```

then use truffle to compile, test: cd into directory and then

```shell
truffle test --compile-all
```

## Overview of the protocol

K2CNFT protocol is a combination of smart-contracts for exchanging tokens, tokens themselves, APIs for order creation, discovery, standards used in smart contracts.

Protocol is primarily targeted to NFTs, but it's not limited to NFTs only. Any asset on EVM blockchain can be traded on K2CNFT.

Smart contracts are constructed in the way to be upgradeable, orders have versioning information, so new fields can be added if needed in future.

## Trade process overview

Users should do these steps to successfully trade on K2CNFT:

- approve transfers for their assets to Exchange contracts (e.g.: call approveForAll for ERC-721, approve for ERC-20) - amount of money needed for trade is price + fee on top of that. learn more at exchange contracts readme
- sign trading order via preferred wallet (order is like a statement "I would like to sell my precious crypto kitty for 10 ETH")
- save this order and signature to the database using K2CNFT protocol API (in future, storing orders on-chain will be supported too)

If user wants to cancel order, he must call cancel function of the Exchange smart contract

Users who want to purchase something on K2CNFT should do the following:

- find asset they like with an open order
- approve transfers the same way (if not buying using Ether)
- form order in the other direction (statement like "I would like to buy precious crypto kitty for 10 ETH")
- call Exchange.matchOrders with two orders and first order signature. 
