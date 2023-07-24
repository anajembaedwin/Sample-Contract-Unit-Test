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
npm install --save-dev chai
