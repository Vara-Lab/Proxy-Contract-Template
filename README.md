# Proxy Contract

This example of contracts demostrates how to use generated clients to call another contracts, in this case, it is used in the Proxy contract which will use the contracts clients from ping and traffic light contracts that are in this repository.

The Proxy contract will send the messages to both contracts using the clients.

## Table of content


- [Proxy Contract state](#proxy-contract-state)
- [Contract clients](#contracts-clients)
- [Setting up your own client](#setting-up-your-own-client)
- [Contracts](#contracts)
- [How to use the template](#how-to-use-the-template)

## Prerequisites

- [Rust instalation](#rust-instalation)
- [Update rust](#update-rust)

### Rust instalation.

If you don't have Rust installed, follow the steps below:

1. Linux users need to install GCC and Clang (according to their distribution’s documentation).

    - For ubuntu users:
        ```bash
        sudo apt install -y build-essential clang cmake curl
        ```
    
    - On macOS, you can get a compiler toolset with the command:
    
        ```bash
        xcode-select --install
        ```
2. Install rust, in this case [Rustup](https://rustup.rs/). With rustup you will install Rust, you will be able to change the Rust version and install additional toolchains.

    ```bash
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    ```

3.  Then, you need to install the target to compile your contracts to Wasm:

    ```bash
    rustup target add wasm32-unknown-unknown
    ```

4. Finally, you have to install a wasm-opt to optmize your contracts wasm files.

    - With linux users:

        ```bash
        sudo apt install binaryen
        ```
    
    - With macOs users:

        ```bash
        brew install binaryen
        ```

### Update Rust

If you already have installed rust, you need to check for updates:

- To compile your contracts, you need to have rust 1.81 or newer to be able to compile the contract.

    ```bash
    rustup install 1.81
    rustup default 1.81
    ```    

- Then, you need to install the target to compile your contracts to Wasm (In case you don't have it):

    ```bash
    rustup target add wasm32-unknown-unknown
    ```

- Finally, you have to install a wasm-opt to optmize your contracts wasm files (In case you don't have it):

    - With linux users:

        ```bash
        sudo apt install binaryen
        ```
    
    - With macOs users:

        ```bash
        brew install binaryen
        ```

## Proxy Contract state

The Proxy contract state use RefCell to store the state of the contract as a part of the Program itself, this avoids the errors of static variables and is safer to handle state, and for clients, it save on gas fees by keeping them in the state.

## Contracts Clients

When you compile a contract, you can set that in compilation time it generates the client for the contract, it helps to send messages to the contract.

To use this clients in your contracts, you need to move that file in your contract directories, in this case, the Proxy Contract contains a `clients` directory where stores all the clients for others contracts, this directory is in `proxy_contract/app/src/clients`, where you will find the clients for ping and traffic light contracts.

## Setting up your own client

In order to establish your own client, you must follow the following steps:

1. In case you need to set up your own client, your `build.rs` file must be configured to be able to generate it. You can see the `proxy_contract/wasm/build.rs` file as an example to configure your contract.

2. Next, you will need to copy the generated client file into the `clients` directory of the proxy contract, and, in the `mod.rs` file, you have to "import" your client (with pub mod file_name.rs).

3. Then, you need to create the service to make calls to your contract using the client, you need to set the service with generics to be able to use the client in your custom service (you need to create the file and add it to the `mod.rs` file in the services directory).

4. Once you create your new service to make calls to your contract, you have to add the route to your service in the program, and create the RefCell with the client to save in gas fees (you can follow the routes of the ping and traffic light contracts).

## Contracts

In the directory you will find the `proxy`, `ping` and `traffic light` contracts, that you can compile and upload in the [Gear IDEA](https://idea.gear-tech.io/programs?node=wss%3A%2F%2Ftestnet.vara.network)

## How to use the template

1. First you will have to clone the repository to the directory you want and enter to the template:

    ```bash
    git clone https://github.com/Vara-Lab/Proxy-Contract-Template.git 
    cd Proxy-Contract-Template
    ```

2. Second, you need to compile all the contracts, with (it's only one command):

    ```bash
    cd ping_pong_contract && cargo b -r && cd ../traffic_light_contract && cargo b -r && cd ../proxy_contract && cargo b -r && cd ..
    ```

3. You need to deploy all the contracts to the [Gear IDEA](https://idea.gear-tech.io/programs?node=wss%3A%2F%2Frpc.vara.network), you need to follow the next steps:

    - To interact with the Gear IDEA and deploy your contract, you will need to download a wallet extension such as [Polkadot-JS](https://polkadot.js.org/extension/), [Talisman](https://talisman.xyz/), or [Subwallet](https://subwallet.app/) to interact with Substrate-based chains.

    <div align="center">
    <img src="https://polkadot.js.org/extension/extension-overview.png" alt="Polkadot-JS Extension">
    </div>

    - Then you have to upload the contracts on [Gear IDEA](https://idea.gear-tech.io/programs?node=wss%3A%2F%2Frpc.vara.network):
        + Access [Gear IDEA](https://idea.gear-tech.io/programs?node=wss%3A%2F%2Frpc.vara.network) using your web browser.
        + Connect your Substrate wallet to Gear IDE.
        + Upload the `wasm.opt.wasm` (which is inside the `target\wasm32-unknown-unknown\release` directory in each of the contracts ) and `app.idl` (which is inside the `wasm` directory in each of the contracts) files by clicking the "Upload Program" button.
        + Repeat this steps with all contracts. 

4. Next, you will need to configure the proxy contract so that it can send messages to the ping and traffic light contracts. This, establishing the ids of both contracts in the Proxy contract sending the messages with the ids.

5. By following the steps, you will have your proxy contract configured!, which can send messages to both contracts, as well as read the state of the contracts.

## Try it on GitPod!

<p align="center">
  <a href="https://gitpod.io/#https://github.com/Vara-Lab/Proxy-Contract-Template.git" target="_blank">
    <img src="https://gitpod.io/button/open-in-gitpod.svg" width="240" alt="Gitpod">
  </a>
</p>

