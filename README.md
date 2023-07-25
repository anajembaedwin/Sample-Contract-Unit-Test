# Sample-Contract-Unit-Test
Writing automated smart contract tests using chai assertions and hardhat

## Setup with Hardhat
npm install --save-dev hardhat
npx hardhat
npx hardhat compile
npm install @openzeppelin/contracts

local blockchains are a great fit for automated tests

npx hardhat node //for a local blockchain (Hardhat Network)

you will need to have a window open running Hardhat Network on your machine
sample port: http://127.0.0.1:8545/

npm install --save-dev @nomiclabs/hardhat-ethers ethers

deploy the Box contract to the local network
npx hardhat run --network localhost scripts/deploy.js

use the Hardhat console to interact with our deployed Box contract on our localhost network.
npx hardhat console --network localhost
const Box = await ethers.getContractFactory('Box');
const box = await Box.attach('0x5FbDB2315678afecb367f032d93F642f64180aa3')

Sending transactions
await box.store(42)

Querying state - using queries doesn’t cost any Ether on any network
await box.retrieve()

display the big number as a string - uint256 is too large a number for JavaScript
(await box.retrieve()).toString()

For more Hardhate Console
https://hardhat.org/hardhat-runner/docs/guides/hardhat-console

Learn Async Functions
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function

To run scripts/index.js file
npx hardhat run --network localhost ./scripts/index.js


In a real-world application, you may want to estimate the gas of your transactions, and check a gas price oracle to know the optimal values to use on every transaction.
https://docs.ethers.org/v5/api/contract/contract/#contract-estimateGas




## Testing with Chai
https://www.chaijs.com/
npm install --save-dev chai

set of principles designed for testing Solidity smart contracts
https://github.com/MolochVentures/moloch/tree/4e786db8a4aa3158287e0935dcbc7b1e43416e38/test#moloch-testing-guide

To run the test
npx hardhat test

A very good idea at this point to set up a Continuous Integration service
to make your tests run automatically every time you commit your code to GitHub

### Performing complex assertions
Many interesting properties of contracts may be hard to capture, such as:

- verifying that the contract reverts on errors
- measuring by how much an account’s Ether balance changed
- checking that the proper events are emitted

OpenZeppelin Test Helpers is a library designed to help you test all of these properties.
https://docs.openzeppelin.com/test-helpers/0.5/

- OpenZeppelin Test Helpers is web3.js based.
- Hardhat users should use the Truffle plugin for compatibility.
https://hardhat.org/hardhat-runner/docs/other-guides/truffle-testing 
- Instead using Hardhat Chai Matchers as a better supported alternative for Ethers.js.
https://hardhat.org/hardhat-chai-matchers/docs/overview

To install and use the OpenZeppelin Test Helpers, run:
npm install --save-dev @openzeppelin/test-helpers

Install web3 and the hardhat-web3 plugin:
npm install --save-dev @nomiclabs/hardhat-web3 web3

https://docs.openzeppelin.com/test-helpers/0.5/
https://hardhat.org/hardhat-runner/plugins/nomiclabs-hardhat-web3#installation

Testing with Web3.js & Truffle:
npm install --save-dev @nomiclabs/hardhat-truffle5 @nomiclabs/hardhat-web3 'web3@^1.0.0-beta.36'
https://hardhat.org/hardhat-runner/docs/other-guides/truffle-testing



<!-- To install and use the hardhat-chai-matchers, run:
or
npm install --save-dev @nomicfoundation/hardhat-chai-matchers
or
yarn add --dev @nomicfoundation/hardhat-chai-matchers -->

We can then update our tests to use OpenZeppelin Test Helpers for very large number support, to check for an event being emitted and to check that a transaction reverts.

