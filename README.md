# Proxy Contract

This example of contracts demostrates how to use generated clients to call another contracts, in this case, it is used in the Proxy contract which will use the contracts clients from ping and traffic light contracts that are in this repository.

The Proxy contract will send the messages to both contracts using the clients.

## Table of content

- [Proxy Contract state](#proxy-contract-state)
- [Contract clients](#contracts-clients)
- [Contracts](#contracts)
- [How to use the template](#how-to-use-the-template)

## Proxy Contract state

The Proxy contract state use RefCell to store the state of the contract as a part of the Program itself, this avoids the errors of static variables and is safer to handle state, and for clients, it save on gas fees by keeping them in the state.

## Contracts Clients

When you compile a contract, you can set that in compilation time it generates the client for the contract, it helps to send messages to the contract.

To use this clients in your contracts, you need to move that file in your contract directories, in this case, the Proxy Contract contains a `clients` directory where stores all the clients for others contracts, this directory is in `proxy_contract/app/src/clients`, where you will find the clients for ping and traffic light contracts.

## Contracts

In the directory you will find the `proxy`, `ping` and `traffic light` contracts, that you can compile and upload in the [Gear IDEA](https://idea.gear-tech.io/programs?node=wss%3A%2F%2Ftestnet.vara.network)

## How to use the template

1. First 

1. First, you need to compile all the contracts with:

    ```bash
    cargo b -r
    ```



<p align="center">
  <a href="https://gitpod.io/#https://github.com/Vara-Lab/Multicontract-Frontend-Template.git" target="_blank">
    <img src="https://gitpod.io/button/open-in-gitpod.svg" width="240" alt="Gitpod">
  </a>
</p>

