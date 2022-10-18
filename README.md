![](cover.png)

**A set of challenges to learn offensive security of smart contracts in Ethereum.**

Featuring flash loans, price oracles, governance, NFTs, lending pools, smart contract wallets, timelocks, and more!

## Play

Visit [damnvulnerabledefi.xyz](https://damnvulnerabledefi.xyz)

## Disclaimer

All Solidity code, practices and patterns in this repository are DAMN VULNERABLE and for educational purposes only.

DO NOT USE IN PRODUCTION.

## Challenge #1 - Unstoppable

### Overview

The unstoppable challenge consists of a Lending contract that provides flashloans in DVT(Damn Vulnerable Token).

Goal: stop the contract from providing flashloans.

[Unstoppable contracts code](https://github.com/jooohneth/damn-vulnerable-defi/tree/master/contracts/unstoppable)

### Solution

Create a Denial-of-Service attack by sending DVT tokens directly to the pool contract.

[Solution code](https://github.com/jooohneth/damn-vulnerable-defi/blob/master/test/unstoppable/unstoppable.challenge.js)

#### Explanation

The Unstoppable contract consists of two functions: depositTokens() and flashLoan()

depositTokens() function takes care of depositing DVT tokens into the pool and updates poolBalance variable accordingly.

flashLoan() function checks eligibility and provides the flashloan.

flashLoan() function has an assertion that is vulnerable to a DOS Attack:

```solidity
    uint256 balanceBefore = damnValuableToken.balanceOf(address(this));
    assert(poolBalance == balanceBefore);
```

By sending DVT tokens directly to the contract and increasing the balanceBefore variable we can break the assertion since the poolBalance variable is only increased when we send DVT tokens through depositTokens() function.
