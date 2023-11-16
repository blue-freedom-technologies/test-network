## test-network

[The Polkadot Parachain Host Implementers' Guide](https://paritytech.github.io/polkadot-sdk/book/)


[Parachain node for smart contracts](https://github.com/paritytech/polkadot-sdk/blob/polkadot-v1.3.0/cumulus/parachains/runtimes/contracts/contracts-rococo/README.md)

### Chain specification

Generate keys for node I

```bash
polkadot key generate --scheme Sr25519 --password-interactive
```

Generate the Sr25519 key for **producing blocks** using [aura](https://wiki.polkadot.network/docs/glossary#aura) for node I.

```text
Key password:polkadot2023
Secret phrase:       dish reveal swallow tonight city early exhibit return able entry estate host
  Network ID:        substrate
  Secret seed:       0x4122f08c02f51053676519275a30a91ebff531cb48f7710671662b531decc50a
  Public key (hex):  0x40268e2a126891c85036b6688020f0cfd53d890c03111be2bdb0944a6bdd550a
  Account ID:        0x40268e2a126891c85036b6688020f0cfd53d890c03111be2bdb0944a6bdd550a
  Public key (SS58): 5DWpNi7UFMdhGviBxLsfTvg95HrQME5UV8dUBY8rcXGcdJfD
  SS58 Address:      5DWpNi7UFMdhGviBxLsfTvg95HrQME5UV8dUBY8rcXGcdJfD
```

```bash
polkadot key inspect --password-interactive --scheme Ed25519 "dish reveal swallow tonight city early exhibit return able entry estate host"
```

Generate Ed25519 key for **finalizing blocks** using [grandpa](https://wiki.polkadot.network/docs/glossary#grandpa-finality-gadget) for node I.

```text
Key password:polkadot2023 
Secret phrase:       dish reveal swallow tonight city early exhibit return able entry estate host
  Network ID:        substrate
  Secret seed:       0x4122f08c02f51053676519275a30a91ebff531cb48f7710671662b531decc50a
  Public key (hex):  0x961f2b4968cf18e802cbc75924495968c005c42b802f7ae8b2bb0db23fdc61b1
  Account ID:        0x961f2b4968cf18e802cbc75924495968c005c42b802f7ae8b2bb0db23fdc61b1
  Public key (SS58): 5FTYJJ9x5wRxPYqeSjDbP4RhjMgpwQDpgbttWrgmm6jb4qHZ
  SS58 Address:      5FTYJJ9x5wRxPYqeSjDbP4RhjMgpwQDpgbttWrgmm6jb4qHZ
```

Generate keys for node II

Generate the Sr25519 key for **producing blocks** using [aura](https://wiki.polkadot.network/docs/glossary#aura) for node II.

```bash
polkadot key generate --scheme Sr25519 --password-interactive
```

```text
Key password:nodeII2023
Secret phrase:       agree destroy want saddle diagram gallery critic address daughter flee retire pet
  Network ID:        substrate
  Secret seed:       0x514f375ec23492e7d63873011ea2ffbb4e89f28d11c52767b7c16204cd75a11f
  Public key (hex):  0xa8267c75604afbfc520dba8462a01bef8ab8f7d0c45b2b34ae275fe20afde309
  Account ID:        0xa8267c75604afbfc520dba8462a01bef8ab8f7d0c45b2b34ae275fe20afde309
  Public key (SS58): 5FsBLMkJSbx53fFYAV4aZ4gzeANztBTV1kJPPWnzuuVxkaoK
  SS58 Address:      5FsBLMkJSbx53fFYAV4aZ4gzeANztBTV1kJPPWnzuuVxkaoK
```

Generate Ed25519 key for **finalizing blocks** using [grandpa](https://wiki.polkadot.network/docs/glossary#grandpa-finality-gadget) for node II.

```bash
polkadot key inspect --password-interactive --scheme Ed25519 "agree destroy want saddle diagram gallery critic address daughter flee retire pet"
```

```text
Key password: 
Secret phrase:       agree destroy want saddle diagram gallery critic address daughter flee retire pet
  Network ID:        substrate
  Secret seed:       0x514f375ec23492e7d63873011ea2ffbb4e89f28d11c52767b7c16204cd75a11f
  Public key (hex):  0x03fd5af7fb0521fd46631c23d28a85463edbe333b3c39dad1f626a5446759805
  Account ID:        0x03fd5af7fb0521fd46631c23d28a85463edbe333b3c39dad1f626a5446759805
  Public key (SS58): 5C9wGDEMPhBCtCJHHEmsVtV5GndNDVsggRpcNDHxrYo8kcjX
  SS58 Address:      5C9wGDEMPhBCtCJHHEmsVtV5GndNDVsggRpcNDHxrYo8kcjX
```





```bash
polkadot build-spec --disable-default-bootnode --chain rococo-local > dev-blue-freedom-spec.json
```


Convert the dev-blue-freedom-spec.json chain specification to the raw format with the file name dev-blue-freedom-spec-raw.json

```bash
polkadot build-spec --chain=dev-blue-freedom-spec.json --raw --disable-default-bootnode > dev-blue-freedom-spec-raw.json
```

```bash
git clone --branch polkadot-v1.3.0 https://github.com/paritytech/polkadot-sdk.git
```

<hr>
<hr><hr><hr><hr><hr>

[The Parity Polkadot Blockchain SDK](https://github.com/paritytech/polkadot-sdk)




This directory currently contains runtimes for the Polkadot, Kusama, Westend, and Rococo networks. In the future, these will be relocated to the runtimes repository.
https://github.com/paritytech/polkadot-sdk/tree/master/polkadot 

https://doc.deepernetwork.org/tutorials/v3/cumulus/start-relay/

# Relay Chain


Clone

```bash
git clone --branch polkadot-v1.3.0 https://github.com/paritytech/polkadot-sdk.git
```

Compile Polkadot

```bash
cd polkadot-sdk
cargo build --release --bin polkadot
```

```bash
cp -r ./target/release/ ../binaries/polkadot
```

Generate a raw chain spec

```bash
./target/release/polkadot build-spec --chain rococo-local --disable-default-bootnode --raw > rococo-local-cfde.json
```

Alice

```bash
./target/release/polkadot --chain rococo-local-cfde.json --alice --tmp
```

Bob (In a separate terminal)
```bash
./target/release/polkadot --chain rococo-local-cfde.json --bob --tmp --port 30334
```

## Parachain

Clone

```bash
git clone https://github.com/paritytech/polkadot-sdk
```

```bash
cd  cumulus/polkadot-parachain
```


```bash
cargo build --release --bin polkadot-parachain
```

```bash
cp -r ./target/release/ ../binaries/polkadot-parachain
```

Export genesis state

```bash
./target/release/polkadot-parachain export-genesis-state > genesis-state
```

# Export genesis wasm

```bash
./target/release/polkadot-parachain export-genesis-wasm > genesis-wasm
```

Collator1

```bash
./target/release/polkadot-parachain --collator --alice --force-authoring --tmp --port 40335 --rpc-port 9946 -- --chain ../polkadot/rococo-local-cfde.json --port 30335
```

Collator2

```bash
./target/release/polkadot-parachain --collator --bob --force-authoring --tmp --port 40336 --rpc-port 9947 -- --chain ../polkadot/rococo-local-cfde.json --port 30336
```

Parachain Full Node 1

```bash
./target/release/polkadot-parachain --tmp --port 40337 --rpc-port 9948 -- --chain ../polkadot/rococo-local-cfde.json --port 30337
```



<hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>

Create the directories:
```bash
mkdir test_network
cd test_network
mkdir binaries
```

### The relay chain node

```bash
git clone --branch polkadot-v1.3.0 https://github.com/paritytech/polkadot-sdk.git
cd polkadot-sdk
cargo build --release
cp -r ./target/release/ ../binaries/polkadot
```

Download [raw-local-chainspec.json](https://docs.substrate.io/assets/tutorials/relay-chain-specs/raw-local-chainspec.json/)

Start the "alice" validator

```bash
./binaries/polkadot/polkadot --alice --validator --base-path ./tmp/relay/alice --chain ./tmp/raw-local-chainspec.json --port 30333 --rpc-port 9944
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/75031d03-2363-412d-b782-89fd5eef219b)

Start the "bob" validator

```bash
./binaries/polkadot/polkadot --bob --validator --base-path ./tmp/relay/bob --chain ./tmp/raw-local-chainspec.json --port 30334 --rpc-port 9945
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/8522dbeb-24bf-4fb9-ad22-a3bf28f02f67)

### The parachain node

[plain-local-chainspec](https://docs.substrate.io/assets/tutorials/relay-chain-specs/plain-local-chainspec.json/)<br>
[raw-local-chainspec.json](https://docs.substrate.io/assets/tutorials/relay-chain-specs/raw-local-chainspec.json/)<br>

 

```bash
git clone --depth 1 --branch polkadot-v1.0.0 https://github.com/substrate-developer-hub/substrate-parachain-template.git
cd substrate-parachain-template
git switch -c test-network
cargo build --release
cp -r ./target/release/ ../binaries/parachain
```

Create the [ParaId](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/parachains/parathreads)

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/71d8b140-a547-4d2d-b746-56bbf298a537)


Generate the plain text chain specification for the parachain node:

```bash
./binaries/parachain/parachain-template-node build-spec --disable-default-bootnode > plain-parachain-chainspec.json
```

Generate a raw chain specification file from the modified plain text chain specification file:

```bash
./binaries/parachain/parachain-template-node build-spec --chain plain-parachain-chainspec.json --disable-default-bootnode --raw > raw-parachain-chainspec.json
```

Export the WebAssembly runtime for the parachain.

```bash
./binaries/parachain/parachain-template-node export-genesis-wasm --chain ./tmp/raw-parachain-chainspec.json para-2000-wasm
```

Generate a parachain genesis state.

```bash
./binaries/parachain/parachain-template-node export-genesis-state --chain ./tmp/raw-parachain-chainspec.json para-2000-genesis-state
```


Start a collator node

```bash
./binaries/parachain/parachain-template-node --alice --collator --force-authoring --chain ./tmp/raw-parachain-chainspec.json --base-path /tmp/parachain/alice --port 40333 --rpc-port 8844 -- --execution wasm --chain ./tmp/raw-local-chainspec.json --port 30343 --rpc-port 9977
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/5a815d0d-6841-4230-bf30-4c5f9ec7c031)



<hr>
<hr>
<hr>
<hr>
<hr>
<hr>

### Create a local test network


Add the polkadot binaries(relay chain):

```bash
git clone https://github.com/paritytech/polkadot-sdk
cd polkadot-sdk
cargo build --release
cp ./target/release ../binaries/polkadot
```

Add the parachain binaries(parachain node):

```bash
git clone https://github.com/paritytech/extended-parachain-template
cd extended-parachain-template
cargo build --release
cp ./target/release ../binaries/extended-parachain-template-node
```

Download the [Zombienet executable](https://github.com/paritytech/zombienet/releases) and execute:

```bash
chmod +x zombienet-linux-x64
sudo cp zombienet-linux-x64 /usr/local/bin
```

config.toml

```text
[relaychain]
default_command = "./binaries/polkadot/polkadot"
default_args = [ "-lparachain=debug" ]
chain = "rococo-local"

  [[relaychain.nodes]]
  name = "alice"
  validator = true

  [[relaychain.nodes]]
  name = "bob"
  validator = true
 
[[parachains]]
id = 2000
addToGenesis = true
cumulus_based = true

  [parachains.collator]
  name = "node-parachain-collator01"
  command = "./binaries/node/parachain-template-node"
```

Spawn a local testing network:

```bash
 zombienet-linux-x64 spawn config.toml -p native
```
Note: use the "-c 1" if using more than one parachain.

![image](https://github.com/blue-freedom-technologies/chain/assets/142290531/2889795d-2e01-4a44-b073-178a13e1a3f2)

Open a [Substrate Portal](https://polkadot.js.org/apps/#/explorer) and validate the 2000 Parachain Id.

![image](https://github.com/blue-freedom-technologies/chain/assets/142290531/371eaf9e-afd6-4b76-b389-c09b21efbc6e)


<hr>
https://docs.substrate.io/tutorials/build-a-parachain/<br>
https://wiki.polkadot.network/docs/build-pdk#your-go-to-overview-for-developing-a-parachain
<hr>

Functional pallets:

 - [pallet_assets](https://paritytech.github.io/substrate/master/pallet_assets/index.html)/[frame-assets](https://github.com/paritytech/polkadot-sdk/tree/master/substrate/frame/assets)
 - [pallet_collective](https://paritytech.github.io/substrate/master/pallet_collective/index.html)/[frame-collective](https://github.com/paritytech/polkadot-sdk/tree/master/substrate/frame/collective)
 - [pallet_utility](https://paritytech.github.io/substrate/master/pallet_utility/index.html)/[frame-utility](https://github.com/paritytech/polkadot-sdk/tree/master/substrate/frame/utility)
 - [pallet_contracts](https://docs.rs/pallet-contracts/24.0.0/pallet_contracts/)/[frame-contracts](https://github.com/paritytech/polkadot-sdk/tree/master/substrate/frame/contracts)/[crate](https://crates.io/crates/pallet-contracts)

<hr>
References:<br>

[Extended Parachain Template](https://github.com/paritytech/extended-parachain-template/)<br>
[Substrate Parachain Template](https://github.com/substrate-developer-hub/substrate-parachain-template)<br>
[Substrate Contracts Node](https://github.com/paritytech/substrate-contracts-node)<br>
[Simulate Parachains](https://docs.substrate.io/test/simulate-parachains/)<br>
[Build a Parachain](https://docs.substrate.io/tutorials/build-a-parachain/)<br>
[Parachain Templates (EPT & FPT)](https://www.youtube.com/watch?v=zZvR1ii8X30)<br>
[Zombienet](https://github.com/paritytech/zombienet/)<br>
[Astar](https://github.com/AstarNetwork/Astar/tree/master)<br>
[Kusama](https://kusama.network/)<br>
[Overview of Polkadot and its Design Considerations](https://arxiv.org/abs/2005.13456.pdf)<br>

Examples:<br>
https://github.com/paritytech/cumulus/blob/master/parachains/runtimes/contracts/contracts-rococo/Cargo.toml<br>
https://github.com/paritytech/trappist/blob/e51c1fead095341210e2a7a5a5971900f476636c/runtime/trappist/src/contracts.rs<br>
https://github.com/paritytech/trappist/tree/main/runtime/trappist
