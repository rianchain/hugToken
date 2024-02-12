# How to create crypto tokens ERC20 with hardhat 


### GETTING STARTED WITH VISUAL STUDIO CODE

create a folder for the project

![image](https://github.com/rianchain/hugToken/assets/142986591/8d752860-c1f1-40fb-a883-9ed59897b760)

drag the folder to visual studio code workspace

![image](https://github.com/rianchain/hugToken/assets/142986591/e944ca2f-aec4-44bd-9983-72af947663dc)

open terminal on vscode

![image](https://github.com/rianchain/hugToken/assets/142986591/6b46996f-8b1c-4005-a733-56876fdcad1b)

![image](https://github.com/rianchain/hugToken/assets/142986591/b7b36462-8aad-463c-a665-ad689858e441)

first step we need to initial the project with npm on terminal visual studio code

```
$ npm init
```

after initial the project, then install hardhat

```
$ npm install --save-dev hardhat
```

after installation hardhat, we need to initial the hardhat project

```
$ npx hardhat init
```

create solidity file in the contracts hardhat folder with `.sol` extension, for instance:

![4](https://github.com/rianchain/hugToken/assets/142986591/f3f85180-b0f5-458c-8e10-8c3a6eaddce1)

create smart contract, for example:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract HugToken is ERC20 {
    constructor() ERC20("hugToken", "HUG") {
        _mint(msg.sender, 1000000 * 10 ** decimals());
    }
}
```

and then we need to install open zeppelin for smart contract

```
$ npm install @openzeppelin/contracts
```

modify the `hardhat-config.js`, for instance:

```
defaultNetwork: "sepolia",
  networks: {
    hardhat: {
    },
    sepolia: {
      url: "https://eth-sepolia.g.alchemy.com/v2/your-api",
      accounts: [privateKey]
    }
  },
```

copy the privateKey from metamask

and create `const privateKey = "your private key"`

modify the `scripts/deploy.js`, for instance:


```
const { ethers } = require("hardhat");

async function main() {
  const [deployer] = await ethers.getSigners();

  console.log("Deploying contracts with the account:", deployer.address);

  const MicroCoin = await ethers.getContractFactory("MicroCoin"); // Pastikan nama kontrak sesuai dengan yang Anda gunakan
  const microCoin = await MicroCoin.deploy(deployer.address); // Sesuaikan argumen konstruktor sesuai kebutuhan kontrak

  await microCoin.waitForDeployment();

  console.log("MicroCoin deployed to:", microCoin.target);
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });


```

and then, deploy the `scripts/deploy.js` to the blockchain with sepolia testnet by this command:

```
$ npx hardhat run --network sepolia scripts/deploy.js
```

finnaly we can scan with `https://sepolia.etherscan.io`
