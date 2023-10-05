# ERC777 and ERC1363: Solutions and Problems  

## Introduction  

Ethereum token standards have evolved to address various challenges posed by earlier implementations and to offer advanced features to developers. ERC777 and ERC1363 are two standards that have evolved on top of ERC20.

## ERC777  

- [ERC777 Spec](https://eips.ethereum.org/EIPS/eip-777)  
- [ERC777 OpenZeppelin Code](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/release-v4.9/contracts/token/ERC777/ERC777.sol)  
- [ERC777 Issue](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/2620)  
- [ERC777 Tweet Thread](https://twitter.com/dmihal/status/1251505373992845317)  
- [ERC777 Reentrancy](https://www.rareskills.io/post/where-to-find-solidity-reentrancy-attacks)  

### Advantages  

1. **Hooks**: It introduced hooks, which are essentially functions that are called during transfer and receipt of tokens. This provides a mechanism to execute custom logic during token transactions.  
- _Hooks allow streamlining of the sending process and offer a single way to send tokens to any recipient. Thanks to the `tokensReceived hook`, contracts are able to react and prevent locking tokens upon reception._  

2. **Simplified Transaction Process**: Unlike ERC20, where you'd have to call `approve()` and then `transferFrom()` for third-party transactions, ERC777 combines these into a single transaction.  

3. **Backwards Compatibility**: ERC777 is compatible with ERC20, ensuring smooth transition for platforms and services which are already integrated with ERC20 tokens.  

### Issues with ERC777  

**Reentrancy Attack**: Shortly after its introduction, a vulnerability related to the use of hooks was discovered. Attackers could exploit these hooks to perform a reentrancy attack, which [has been seen previously on Uniswap](https://blog.openzeppelin.com/exploiting-uniswap-from-reentrancy-to-actual-profit).  

## ERC1363  

ERC1363 was introduced to address the security vulnerabilities present with ERC777.  

ERC-1363 allows for developers to add a callback after transferring or approving tokens to be executed.  

- [ERC1363 Spec](https://eips.ethereum.org/EIPS/eip-1363)  
- [ERC1363 Code](https://github.com/vittominacori/erc1363-payable-token/tree/master/contracts/token/ERC1363)  

There are many proposed uses of Ethereum smart contracts that can accept EIP-20 callbacks. Examples could be:  
- to create a token payable crowdsale  
- selling services for tokens  
- paying invoices  
- making subscriptions  

### Advantages  

1. **Extendable Functions**: It introduces `transferAndCall()` and `transferFromAndCall()` functions which allow tokens to be spent and notify a receiver contract in a single transaction.  

2. **Custom Logic Execution**: Like ERC777, ERC1363 permits the execution of custom logic after the token transfer.  

3. **Backwards Compatibility**: Ensures a broad range of application and reduces integration friction for platforms.  

4. **Solves the Reentrancy Attack Problem**: ERC1363 addresses the reentrancy attack vulnerability posed by ERC777 by implementing the execution of post-transfer logic.  

### Why ERC1363 was introduced  

1. **Security Concerns with ERC777**: Given the vulnerabilities in ERC777, there was a need for a safer standard that preserved the beneficial features.  

2. **Better Developer Experience**: Combining features from ERC20 and ERC777, while eliminating their vulnerabilities, offers developers a more robust and versatile standard.  

3. **Optimization of Transaction Processes**: With ERC1363, developers can execute more complex operations while minimizing the number of transactions, leading to a better user experience and cost savings.  

## Summary  

While ERC20 paved the way for tokens on the Ethereum platform, the subsequent evolution of token standards, such as ERC777 and ERC1363, demonstrates the community's commitment to enhancing security, usability, and versatility for developers and users alike. Before choosing a token standard, it's crucial to evaluate the specific requirements of the use case and stay informed about any potential vulnerabilities or updates.  
