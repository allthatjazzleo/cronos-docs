# Cronos: Deploy Smart Contract

This documentation demostrate the deployment of smart contract to Cronos, using Solidity. `@openzeppelin/contracts` is used for the demo sodlity script.

Both Truffle and Hardhat are included in this documentation, feel free to choose one of them.

## Pre-requisites

### Supported OS

We officially support macOS, Windows and Linux only. Other platforms may work but there is no guarantee. We will extend our support to other platforms after we have stabilized our current architecture.

### Prepare nodejs and npm environment 

You can refer to [Downloading and installing Node.js and npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)  
`Nodejs v10` is suggested 

### Sufficient fund on deployer address
You can access to [Croeseid testnet faucet and explorer](http://localhost:8080/docs/getting-started/croeseid-testnet.html#croeseid-testnet-faucet-and-explorer) to obtain testnet TCRO.

## Truffle: Deploy ERC20 Contract

### Step 1. Enter `smart-contract-example/truffle` folder
  ```bash
  $ cd smart-contract-example/truffle
  ```

### Step 2. Run `npm install` inside the folder
  ```bash
  $ npm install
  ```

### Step 3. Make a copy of `.env.example` to `.env`
  ```bash
  $ cp .env.example .env
  ```

### Step 4. Modify `.env` and fill *ONE* of the field
  ```bash
  MNEMONIC=goose easy ivory ...
  PRIVATE_KEY=XXXXXXX
  ```

### Step 5. Review Migration Script at `migrations/2_deploy_cronos_token.js`
  ```javascript
    const CronosToken = artifacts.require("CronosToken");
    
    module.exports = function (deployer) {
        deployer.deploy(CronosToken, "Cronos Token", "CRT", "1000000000000000000000000");
    };
  ```
  
### Step 6. Deploy Contract
  ```bash
  npm run deploy-contract-cronos
  ```

### Step 7. Obtain Contract address from console and input to Metamask
Correct balance will be shown on Metamask page
<img src="./assets/cronos-smart-contract/truffle_deploy_contract_address.png" />
<img src="./assets/cronos-smart-contract/metamask_add_tokens.png" />
<img src="./assets/cronos-smart-contract/metamask_add_token_success.png" />

## Hardhat: Deploy ERC20 Contract
### Step 1. Enter `smart-contract-example/hardhat` folder
  ```bash
  $ cd smart-contract-example/hardhat
  ```

### Step 2. Run `npm install` inside the folder
  ```bash
  $ npm install
  ```

### Step 3. Make a copy of `.env.example` to `.env`
  ```bash
  $ cp .env.example .env
  ```

### Step 4. Modify `.env` and fill *ONE* of the field
  ```bash
  MNEMONIC=goose easy ivory ...
  PRIVATE_KEY=XXXXXXX
  ```

### Step 5. Review Migration Script at `scripts/deploy-cronos-token.js`
  ```javascript
    async function main() {
        const CronosToken = await hre.ethers.getContractFactory("CronosToken");
        const cronosToken = await CronosToken.deploy("Cronos Token", "CRT", "1000000000000000000000000");
    
        await cronosToken.deployed();
    
        console.log("CronosToken deployed to:", cronosToken.address);
    }
  ```

### Step 6. Deploy Contract
  ```bash
  npm run deploy-contract-cronos
  ```

### Step 7. Obtain Contract address from console and input to Metamask
Correct balance will be shown on Metamask page
  ```bash
  CronosToken deployed to: 0x5F803c894a0A16B46fe5982fB5D89eb334eAF68
  ```
<img src="./assets/cronos-smart-contract/metamask_add_tokens.png" />
<img src="./assets/cronos-smart-contract/metamask_add_token_success.png" />