<h1 align="center">

Simple Contract POC
<br>

</h1>

<h4 align="center">A simple Supply Chain setup with <a href="https://docs.soliditylang.org/en/v0.8.4/" target="_blank">Solidity</a>.</h4>

<p align="center">
  <a href="#description">Description</a> •
  <a href="#architecture">Architecture</a> •
  <a href="#flow">Flow</a> •
  <a href="#working">Working</a> •
  <a href="#contract-diagrams">Contract Diagrams</a> •
  <a href="#installation-and-setup">Installation and Setup</a> •
  <a href="#license">License</a>
</p>

## Description

Inventory management and control have always been a challenge for any business. Most of the time, the inventory is managed by a single person, but this is not always the case. In this project, we will build a smart contract that will allow you to manage your inventory in a decentralized way. This also has support for multiple users, and will allow you to create and manage your own inventory.

## Architecture

The smart contract will be built using the [Solidity](https://solidity.readthedocs.io/en/v0.8.4/) language. The smart contract will be deployed to the [Ethereum network](https://ethereum.org/). For testing purpose we use ganache-cli, which is a [Ethereum](https://ethereum.org/) localnet. This project has been tested in nodejs v14.

## Working

<p>
  A product's lifecycle begins when manufactureProduct() is called (while making an entry) after the final product is manufactured and the product and manufacturer details are entered into the blockchain. The productHistory[] is initialised, and the current product data is saved in the current owner's database (manufacturer).
</p>
<p>
  This product is now available for purchase by a Third Party. When a product is purchased by a third-party seller, the purchasedByThirdParty() method is invoked, where the owner is set to thirdParty and the current data is pushed to the productHistory[] table (which helps us to track the origin and handling of the product). Simultaneously, the product is shipped by the manufacturer (shipToThirdParty()) and received by the Third Party, where receivedByThirdParty() is called and the Third Party seller's information is entered. The data from each of these checkpoints is saved in product history, and the state is updated at each step.
</p>
<p>
  The product is purchased from a Third Party via the internet. When a customer orders a product, it is shipped by a Third Party (shipByThirdParty()) and delivered to the delivery hub. The function ByDeliveryHub() is called. The customer address is saved here, the owner is set to Delivery Hub, the Delivery Hub details are fed, and the current data state is pushed to the product. History[].
</p>
<p>
  Finally, the product is sent by the Delivery Hub (shipByDeliveryHub()) and received by the customer, where receivedByCustomer() is called, and the product's current and final states are pushed to it. History[].
</p>
<p>
  All of these juncture functions must be called only after the product and productHistory[] have been completely verified while entering a checkpoint. (For example, a customer accepts and confirms a product by clicking the receive button from his account only after it has been verified.) 
</p>
<p>
  <strong>fetchProductPart1()</strong>, <strong>fetchProductPart2()</strong>, <strong>fetchProductPart3()</strong>, <strong>fetchProductHistoryLength()</strong>, <strong>fetchProductCount()</strong>, <strong>fetchProductState()</strong> are the functions to retreive data of a product queried with UID and data type as product(current state) or history.
</p>
<p>
  The hashes (read certificates) are generated using the Solidity cryptographic function keccak256(), which in the blockchain setup implements a SHA-3 hash. Aside from smart contracts being immutable, keccak256() generates a secure 256-bit hash, which is the main basis of security in the entire mainnet. Certificates are generated at each stage of the product's shipping in our supply chain setup.
</p>

## Contract Diagrams

<h3>Sequence</h3>
The flow of the functions in the smart contracts.
<p align="centre">
  <a>
    <img src="https://github.com/karan-vk/SuppyChainSample/blob/main/images/sequencediagram.png?raw=true" width="1000">
  </a>
</p>

## Installation and Setup

Prerequisites : `npm, git, docker(optional)`

Clone the repository

```Bash
git clone <url>repo
&& cd eth-supplychain-dapp
```

Install dependencies

```Bash
npm i
```

Install ganache-cli

```Bash
npm i -g ganache-cli
```

Configure ganache-cli for 10 accounts and extend gasLimit to 6721975000 and beyond, so as to have enough gas for migrating the smart contracts and a data flow for the prototype.

```Bash
ganache-cli --accounts 10 --gasLimit 6721975000
```

Migrate the contracts

```Bash
truffle migrate --network=develop --reset
```

Open a second terminal and enter the client folder

```Bash
cd client
```

Install all packages in the package.json file

```Bash
npm i
```

Run the app

```Bash
npm start
```

The app gets hosted by default at port 3000.

## License

This project uses an [MIT](https://opensource.org/licenses/MIT) license.

## Documentation to help with Solidity

https://docs.soliditylang.org/en/v0.8.4/

## Documentation to help with React

https://reactjs.org/docs/getting-started.html

## Documentation to help with Truffle

https://www.trufflesuite.com/docs/truffle/reference/configuration

## Documentation to help with Ganache-cli

https://www.trufflesuite.com/docs/ganache/overview
