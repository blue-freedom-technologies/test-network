## Chain

Create a local test network:

Create the directories:
```bash
mkdir test_network
cd test_network
mkdir binaries
```

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

  [[relaychain.nodes]]
  name = "bob"

  [[relaychain.nodes]]
  name = "charlie"

  [[relaychain.nodes]]
  name = "dave"

[[parachains]]
id = 1000
cumulus_based = true

  [parachains.collator]
  name = "parachain-node1-1000-collator"
  command = "./binaries/node/parachain-template-node"
 
 [[parachains]]
id = 1001
cumulus_based = true

  [parachains.collator]
  name = "parachain-node2-1001-collator"
  command = "./binaries/node/parachain-template-node"

```

![image](https://github.com/blue-freedom-technologies/chain/assets/142290531/2dc29217-22c8-4e75-8165-80508f20aa87)

Spawn a local testing network:

```bash
 ./zombienet-linux-x64 spawn config.toml -p native -c 1
```

Functional pallets:

 - [pallet_assets](https://paritytech.github.io/substrate/master/pallet_assets/index.html)
 - [pallet_collective](https://paritytech.github.io/substrate/master/pallet_collective/index.html)
 - [pallet_utility](https://paritytech.github.io/substrate/master/pallet_utility/index.html)
 - [pallet_contracts](https://paritytech.github.io/polkadot-sdk/master/pallet_contracts/index.html)

<hr>
References:<br>

[Extended Parachain Template](https://github.com/paritytech/extended-parachain-template/)<br>
[Substrate Parachain Template](https://github.com/substrate-developer-hub/substrate-parachain-template)<br>
[Simulate Parachains](https://docs.substrate.io/test/simulate-parachains/)<br>
[Parachain Templates (EPT & FPT)](https://www.youtube.com/watch?v=zZvR1ii8X30)<br>
