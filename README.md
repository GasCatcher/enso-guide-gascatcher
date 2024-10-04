# Step-by-Step Guide for temper

## Step 1: Clone the Repo

To begin working with the repository:
```
git clone https://github.com/EnsoFinance/temper.git
cd temper
```

## Step 2: Install Dependencies
Navigate to the directory and install the necessary dependencies (likely Node.js packages or Rust):
```
npm install
```
or
```
yarn install
```

## Step 3: Run Tests

Assuming that the repository contains test suites for the smart contracts, you can typically run the tests using:

```
npm run test
```

or, if Hardhat is being used:

```
npx hardhat test
```

Let’s say the repository uses Hardhat to run tests. You might write a test file in test/example.js like this:

```
const { expect } = require("chai");

describe("Token contract", function () {
    let Token;
    let hardhatToken;
    let owner;
    let addr1;
    let addr2;
    
    beforeEach(async function () {
        Token = await ethers.getContractFactory("Token");
        [owner, addr1, addr2] = await ethers.getSigners();
        hardhatToken = await Token.deploy();
    });

    describe("Deployment", function () {
        it("Should set the right owner", async function () {
            expect(await hardhatToken.owner()).to.equal(owner.address);
        });

        it("Should assign the total supply of tokens to the owner", async function () {
            const ownerBalance = await hardhatToken.balanceOf(owner.address);
            expect(await hardhatToken.totalSupply()).to.equal(ownerBalance);
        });
    });
});
```

This test ensures that the deployed token contract assigns ownership correctly and distributes the supply to the owner.

## Step 4: Deployment (optional)

If the repository includes deployment scripts, you can typically deploy the contracts to a local or test network:

```
npx hardhat run scripts/deploy.js --network rinkeby
```

