---
title: "What is a Smart Contract?"
date: 2021-07-04T12:56:32-07:00
advertise: true
draft: false
---

## Smart Contracts

A smart contract simply put are contracts that self execute based upon certain criteria that is coded into the smart contract. These contracts exist in a blockchain, where it is completely decentralized. When a smart contract is coded, they are written as if-then statements. For example, if the weather drops below 60 degrees, then send an alert to this person's phone. Smart contracts are a very safe way of carrying out agreements, by use of a blockchain. This eliminates the need for a middleman, and directly connects the two entities. While most people don't understand them quite yet, these contracts may very well change the world we live in. 

<img src='/images/contract.jpg' style='border:solid black 2px; margin:50px 0 0 0'>

<br/>

## Smart Contract Example

This is an example of a real smart contract. This is a contract for a very simple cryptocurrency. This contract has a few key aspects, such as giving only the creator the right to create coins, anyone can send coins to each other without using a username and password, while instead just needing an Ethereum keypair.

<br/>


```solidity
pragma solidity >=0.5.0 <0.7.0;

contract Coin {
    // The keyword "public" makes variables
    // accessible from other contracts
    address public minter;
    mapping (address => uint) public balances;

    // Events allow clients to react to specific
    // contract changes you declare
    event Sent(address from, address to, uint amount);

    // Constructor code is only run when the contract
    // is created
    constructor() public {
        minter = msg.sender;
    }

    // Sends an amount of newly created coins to an address
    // Can only be called by the contract creator
    function mint(address receiver, uint amount) public {
        require(msg.sender == minter);
        require(amount < 1e60);
        balances[receiver] += amount;
    }

    // Sends an amount of existing coins
    // from any caller to an address
    function send(address receiver, uint amount) public {
        require(amount <= balances[msg.sender], "Insufficient balance.");
        balances[msg.sender] -= amount;
        balances[receiver] += amount;
        emit Sent(msg.sender, receiver, amount);
    }
}
```



