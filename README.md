## Chain

Create a local test network:

Create the directories:
```bash
mkdir test_network
cd test_network
mkdir binaries
```

Add the polkadot binaries:

```bash
git clone https://github.com/paritytech/polkadot-sdk
cd polkadot-sdk
cargo build --release
cp ./target/release/polkadot ../binaries/polkadot
```

Add the parachain binaries:

```bash
git clone https://github.com/paritytech/extended-parachain-template
cd extended-parachain-template
cargo build --release
cp ./target/release/polkadot ../binaries/polkadot
cp ./target/release/extended-parachain-template ../binaries/extended-parachain-template-node
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
[Parachain Templates (EPT & FPT)](https://www.youtube.com/watch?v=zZvR1ii8X30)<br>
