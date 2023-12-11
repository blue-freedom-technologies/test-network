# test-network

All the setups demonstrated in this document were done using [ubuntu-22-04-3-lts](https://fridge.ubuntu.com/2023/08/11/ubuntu-22-04-3-lts-released/). It's assumed that [Rust](https://www.rust-lang.org/tools/install) is installed and running.

# Table of Contents

Requirements

- [Polkadot SDK](https://github.com/blue-freedom-technologies/test-network#polkadot-sdk)
- [Zombienet](https://github.com/blue-freedom-technologies/test-network#zombienet)

Manual setup

- [Relay Chain](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#relay-chain)
  - [Create the directories](https://github.com/blue-freedom-technologies/test-network#create-the-directories)
  - [Generate a raw chain spec](https://github.com/blue-freedom-technologies/test-network#generate-a-raw-chain-spec)
  - [Start-the alice node](https://github.com/blue-freedom-technologies/test-network#start-the-alice-nodenew-terminal)
  - [Start the bob node](https://github.com/blue-freedom-technologies/test-network#start-the-bob-nodenew-terminal)
  - [Connect to the relay chain](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#connect-to-the-relay-chain)
  - [Reserve a paraid](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#reserve-a-paraid)
  - [Confirm the events](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#confirm-the-events)
- [Parachain](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#parachain)
  - [Clone the repo to get the Cumulus sdk](https://github.com/blue-freedom-technologies/test-network#clone-the-repo-to-get-the-cumulus-sdk)
  - [Compile the polkadot parachain node](https://github.com/blue-freedom-technologies/test-network#compile-the-polkadot-parachain-node)
  - [Copy the polkadot-parachain binary](https://github.com/blue-freedom-technologies/test-network#copy-the-polkadot-parachain-binary)
  - [Generate the plain text chain specification](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-the-plain-text-chain-specification)
  - [Modify the plain text chain specification](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#modify-the-plain-text-chain-specification)
  - [Generate-a-raw-chain-specification-file-from-the-modified--plain-text-chain-specification](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-a-raw-chain-specification-file-from-the-modified--plain-text-chain-specification)
  - [Export the webassembly runtime](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#export-the-webassembly-runtime)
  - [Generate a parachain genesis state](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-a-parachain-genesis-state)
  - [Start the collator node alice](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#start-the-collator-node-alice)
  - [Register the parachain with the local relay chain](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#register-the-parachain-with-the-local-relay-chain)
  - [Sudo transaction](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#sudo-transaction)
  - [Testing the parachain](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#testing-the-parachain)
- [Relay Chain(Private network of trusted validators)](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#relay-chain-private-network-of-trusted-validators)
  - [Session keys for Node I(validator)](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#session-keys-for-node-ivalidator)
    - [Generate a session key using the Sr25519 scheme](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-a-session-key-using-the-sr25519-scheme)
    - [Derive the grandpa key using Ed25519 scheme](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#derive-the-grandpa-key-using-ed25519-scheme)
    - [Derive the beefy key using EdDSA scheme](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#derive-the-beefy-key-using-eddsa-scheme)
    - [Generate the babe key using Sr25519 scheme](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-the-babe-key-using-sr25519-scheme)
    - [Node I(validator) keys](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#node-ivalidator-keys)
  - [Session keys for Node II(validator)](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#session-keys-for-node-iivalidator)
    - [Generate a session key using the Sr25519 scheme](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-a-session-key-using-the-sr25519-scheme-1)
    - [Derive the grandpa key using Ed25519 scheme](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#derive-the-grandpa-key-using-ed25519-scheme-1)
    - [Derive the beefy key using EdDSA scheme](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#derive-the-beefy-key-using-eddsa-scheme-1)
    - [Generate the babe key using Sr25519 scheme](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-the-babe-key-using-sr25519-scheme-1)
    - [Node II(validator) keys](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#node-iivalidator-keys)
  - [Create a custom chain specification](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#create-a-custom-chain-specification)
    - [Generate a raw chain spec](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-a-raw-chain-spec-1)
    - [Modify the local relay chain specification](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#modify-the-local-relay-chain-specification)
    - [Generate the plain-text-chain-specification](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-the-plain-text-chain-specification-1)
  - [Start Node I validator](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#start-node-i-validator)
    - [Add grandpa key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-grandpa-key-to-the-keystore)
    - [Add beefy key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-beefy-key-to-the-keystore)
    - [Add babe key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-babe-key-to-the-keystore)
    - [Add imon key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-imon-key-to-the-keystore)
    - [Add para key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-para-key-to-the-keystore)
    - [Add asgn key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-asgn-key-to-the-keystore)
    - [Add audi key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-audi-key-to-the-keystore)
    - [Verify the seven files holding the keys created in the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#verify-the-seven-files-holding-the-keys-created-in-the-keystore)
    - [Restart Node I](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#restart-node-i)
  - [Start Node II validator](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#start-node-ii-validator)
    - [Add grandpa key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-grandpa-key-to-the-keystore-1)
    - [Add beefy key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-beefy-key-to-the-keystore-1)
    - [Add babe key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-babe-key-to-the-keystore-1)
    - [Add imon key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-imon-key-to-the-keystore-1)
    - [Add para key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-para-key-to-the-keystore-1)
    - [Add asgn key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-asgn-key-to-the-keystore-1)
    - [Add audi key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-audi-key-to-the-keystore-1)
    - [Verify the seven files holding the keys created in the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#verify-the-seven-files-holding-the-keys-created-in-the-keystore-1)
    - [Restart Node II](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#restart-node-ii)
- [Parachain (Private network of trusted collatores)](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#parachain-private-network-of-trusted-collatores)
  - [Clone the repo to get the Cumulus sdk](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#clone-the-repo-to-get-the-cumulus-sdk-1)
  - [Compile the polkadot parachain node](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#compile-the-polkadot-parachain-node-1)
  - [Copy the polkadot-parachain binary](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#copy-the-polkadot-parachain-binary-1)
  - [Generate two session keys using the sr25519-scheme for aura](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-two-session-keys-using-the-sr25519-scheme-for-aura)
  - [Generate the plain text chain specification](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-the-plain-text-chain-specification-2)
  - [Modify the plain text chain specification](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#modify-the-plain-text-chain-specification-1)
  - [Generate a raw chain specification file from the modified plain text chain specification](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-a-raw-chain-specification-file-from-the-modified-plain-text-chain-specification)
  - [Start the collator node](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#start-the-collator-node)
  - [Add aura key to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-aura-key-to-the-keystore)
  - [Verify the file holding the key created in the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#verify-the-file-holding-the-key-created-in-the-keystore)
  - [Restart collator node](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#restart-collator-node)
  - [Export the webassembly runtime](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#export-the-webassembly-runtime-1)
  - [Generate-a-parachain-genesis-state](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-a-parachain-genesis-state-1)
  - [Register the parachain with the local relay chain](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#register-the-parachain-with-the-local-relay-chain-1)
  - [Sudo transaction](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#sudo-transaction-1)
  - [Testing the parachain](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#testing-the-parachain-1)

Zombienet setup

- [Simple-network](https://github.com/blue-freedom-technologies/test-network#simple-network)
  - [Create the network specification file](https://github.com/blue-freedom-technologies/test-network#create-the-network-specification-file)
  - [Spawn a local testing network](https://github.com/blue-freedom-technologies/test-network#spawn-a-local-testing-network)
  - [Testing the parachain](https://github.com/blue-freedom-technologies/test-network#testing-the-parachain-2)
- [Network with hrmp channels](https://github.com/blue-freedom-technologies/test-network#network-with-hrmp-channels)
  - [Create the network specification file](https://github.com/blue-freedom-technologies/test-network#create-the-network-specification-file-1)
  - [Spawn a local testing network](https://github.com/blue-freedom-technologies/test-network#spawn-a-local-testing-network-1)

<hr>

## Polkadot SDK

Install [polkadot sdk](https://github.com/paritytech/polkadot-sdk/tree/polkadot-v1.3.0/polkadot) via Cargo

```bash
cargo install --git https://github.com/paritytech/polkadot-sdk --tag polkadot-v1.3.0 polkadot --locked
```

Test the setup

```bash
polkadot --version
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/14efafe6-6391-4fe4-8c9b-324f837fc389)

[The Polkadot Parachain Host Implementers' Guide](https://paritytech.github.io/polkadot-sdk/book/)

<hr>

## Zombienet

Install [Zombienet executable](https://github.com/paritytech/zombienet/releases)

```bash
chmod +x zombienet-linux-x64
sudo cp zombienet-linux-x64 /usr/local/bin
```

Test the setup

```bash
zombienet-linux-x64 version

```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/24fd7221-db5f-4063-94b4-c1ed72469a4b)

[Zombienet Book](https://paritytech.github.io/zombienet/intro.html)

<hr>

# Manual setup

## Relay Chain

We should have at least two validators (relay chain nodes) running for every collator (parachain block authoring nodes) on our network.

#### Create the directories

```bash
mkdir test-network
cd test-network
mkdir binaries
```

#### Generate a raw chain spec

```bash
polkadot build-spec --chain rococo-local --disable-default-bootnode --raw > ./tmp/raw-relay-chainspec.json
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/5bb28f46-fd7a-4a34-a883-3b9350c217a5)

#### Start the Alice node(new terminal)
 
```bash
polkadot --chain ./tmp/raw-relay-chainspec.json --alice --validator --tmp --port 30333
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/d328d1a6-3e0c-4838-ba45-edbc6b2f0387)

#### Start the Bob node(new terminal)
 
```bash
polkadot --chain ./tmp/raw-relay-chainspec.json --bob --validator --tmp --port 30334
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/fb5307e6-1b49-4b8a-9144-4b4006737049)

#### Connect to the [relay chain](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/parachains/parathreads)

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/c3a9215f-5a38-4be7-a393-d9dc38fcc1f2)

#### Reserve a paraid

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/29dc9f98-aee7-4f08-a477-35d1a4cd0dd9)

#### Confirm the events

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/12760045-3ad6-4224-b2a7-176b9ee865ef)

## Parachain

#### Clone the repo to get the [Cumulus SDK](https://github.com/paritytech/polkadot-sdk/tree/polkadot-v1.3.0/cumulus)

```bash
git clone --branch polkadot-v1.3.0 https://github.com/paritytech/polkadot-sdk.git
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/b6c5acb2-6e82-49ea-b760-3c8ce330e373)

#### Compile the polkadot parachain node

```bash
cd polkadot-sdk/cumulus/polkadot-parachain
cargo build --release --bin polkadot-parachain
```

#### Copy the polkadot-parachain binary

```bash
cd ../../../
cp -r ./polkadot-sdk/target/release/ ./binaries/polkadot-parachain
```

#### Generate the plain text chain specification

```bash
./binaries/polkadot-parachain/polkadot-parachain build-spec --disable-default-bootnode > ./tmp/plain-parachain-chainspec.json
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/9bff08d3-9b76-4ba4-a4bd-32a2816046e5)

#### Modify the plain text chain specification

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/68d5909b-0b70-4777-9630-34b23edc12b4)

#### Generate a raw chain specification file from the modified  plain text chain specification

```bash
./binaries/polkadot-parachain/polkadot-parachain build-spec --chain ./tmp/plain-parachain-chainspec.json --disable-default-bootnode --raw > ./tmp/raw-parachain-chainspec.json
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/1d8336c8-c796-4d6d-adeb-e4fbb436c578)

#### Export the WebAssembly runtime

```bash
./binaries/polkadot-parachain/polkadot-parachain export-genesis-wasm --chain ./tmp/raw-parachain-chainspec.json ./tmp/para-2000-wasm
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/9af0e96b-5e9e-4fb0-9d61-1a4ac7f4e4ce)

#### Generate a parachain genesis state

```bash
./binaries/polkadot-parachain/polkadot-parachain export-genesis-state --chain ./tmp/raw-parachain-chainspec.json ./tmp/para-2000-genesis-state
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/51b77976-166b-4789-aa8b-09ce19fc147d)

#### Start the collator node alice

```bash
./binaries/polkadot-parachain/polkadot-parachain --alice --collator --force-authoring --chain ./tmp/raw-parachain-chainspec.json --base-path /tmp/parachain/alice --port 40333 --rpc-port 8844 -- --execution wasm --chain ./tmp/raw-relay-chainspec.json --port 30343 --rpc-port 9977
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/56adcac9-36a1-4e2c-9198-341775870832)

#### Register the parachain with the [local relay chain](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/sudo)

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/c33c46d7-06f4-4411-90fb-ff836981f8c5)

#### Sudo transaction
Note: We are bypassing the steps required to acquire a parachain or parathread slot which normally is a [parachain auction](https://wiki.polkadot.network/docs/learn-auction).

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/2e7ad33c-6591-4317-b016-a40baf0383c3)

#### Testing the parachain.

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/2daf3a1e-e666-4dc5-a4fa-2829f3afb42d)

## Relay Chain (Private network of trusted validators)

We should have at least two validators (relay chain nodes) running for every collator (parachain block authoring nodes) on our network.
Keys are generated in a **air-gapped computer** that is deliberately separated from the internet for security reasons. This means that the computer does not have any physical or wireless connections to any other network that is connected to the internet.

### Session keys for Node I([validator](https://wiki.polkadot.network/docs/maintain-guides-how-to-validate-polkadot))

[Session keys](https://wiki.polkadot.network/docs/learn-cryptography#session-keys) are hot keys that must be kept online by a validator to perform network operations.

#### Generate a session key using the Sr25519 scheme. 

```bash
polkadot key generate --scheme Sr25519 --password-interactive
```

```text
Key password:********
Secret phrase:       sick cry forget enroll retreat female slab uncover remember neutral time stadium
  Network ID:        substrate
  Secret seed:       0x6f1a8e2665eeec408ad9efd4d5ae5e38737f8b7777d58d063364a61584a42d19
  Public key (hex):  0xf6fb2baa764e9c7e1d6c27324f55dc585b89e1e74b8d7a409d84c5bccf818341
  Account ID:        0xf6fb2baa764e9c7e1d6c27324f55dc585b89e1e74b8d7a409d84c5bccf818341
  Public key (SS58): 5HeYFTPrAufPytrEGQUvSSLHbKSqb9e2NVaBRDTBvZ769kq3
  SS58 Address:      5HeYFTPrAufPytrEGQUvSSLHbKSqb9e2NVaBRDTBvZ769kq3
```

#### Derive the [grandpa](https://wiki.polkadot.network/docs/glossary#grandpa-finality-gadget) key using Ed25519 scheme.

```bash
polkadot key inspect --password-interactive --scheme Ed25519 "sick cry forget enroll retreat female slab uncover remember neutral time stadium"
```

```text
Key password:********
Secret phrase:       sick cry forget enroll retreat female slab uncover remember neutral time stadium
  Network ID:        substrate
  Secret seed:       0x6f1a8e2665eeec408ad9efd4d5ae5e38737f8b7777d58d063364a61584a42d19
  Public key (hex):  0xd020bc843ece07f62adafd6e73fd59fbb4983eb37308b00302b9b68784141a11
  Account ID:        0xd020bc843ece07f62adafd6e73fd59fbb4983eb37308b00302b9b68784141a11
  Public key (SS58): 5GmbYPGYH1KxnHw1nXunNQjKJMfeFf2vtmAJJLKq9B856Nfx
  SS58 Address:      5GmbYPGYH1KxnHw1nXunNQjKJMfeFf2vtmAJJLKq9B856Nfx
```

#### Derive the [beefy](https://wiki.polkadot.network/docs/learn-consensus#bridging-beefy) key using EdDSA scheme.

```bash
polkadot key inspect --password-interactive --scheme Ecdsa "sick cry forget enroll retreat female slab uncover remember neutral time stadium"
```

```text
Key password:********
Secret phrase:       sick cry forget enroll retreat female slab uncover remember neutral time stadium
  Network ID:        substrate
  Secret seed:       0x6f1a8e2665eeec408ad9efd4d5ae5e38737f8b7777d58d063364a61584a42d19
  Public key (hex):  0x03e6f4ff962acbc87abca901754e5aa4caa78169150cd3caa0a9955b6e4a74a856
  Account ID:        0x8dd3e3b15d3cf068ec8b23bcba4883a0ed0db744eabcd9e117b1a85001ff6a48
  Public key (SS58): KWDw8nyTtutLkcAyJE6jFsaZFVPUkoZjzXF5U8XaYX4kAKGwD
  SS58 Address:      5FGfZ3FhBZCQFNh1BZyNzC1Hv3aPhw2jATnKz9NbkNxLuNc6
```

#### Generate the [babe](https://wiki.polkadot.network/docs/glossary#babe) key using Sr25519 scheme.

```bash
polkadot key generate --scheme Sr25519 --password-interactive
```

```text
Key password:********
Secret phrase:       vanish street orphan print magic atom link census clever sound quote logic
  Network ID:        substrate
  Secret seed:       0xfeb1e206b7394fdff897a2243c8b2ae113e0b6fded4a9d2f42f691851dcc0745
  Public key (hex):  0x2c9b041e0d7f686834958607c306b900701c07cf10265eb67d1aaf1cf2e23407
  Account ID:        0x2c9b041e0d7f686834958607c306b900701c07cf10265eb67d1aaf1cf2e23407
  Public key (SS58): 5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf
  SS58 Address:      5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf
```

#### Node I([validator](https://wiki.polkadot.network/docs/maintain-guides-how-to-validate-polkadot)) keys:
- Id key(Sr25519):```5HeYFTPrAufPytrEGQUvSSLHbKSqb9e2NVaBRDTBvZ769kq3```
- grandpa (gran/Ed25519):```5GmbYPGYH1KxnHw1nXunNQjKJMfeFf2vtmAJJLKq9B856Nfx```
- beefy (beef/EdDSA):```KWDw8nyTtutLkcAyJE6jFsaZFVPUkoZjzXF5U8XaYX4kAKGwD```
- babe (babe/Sr25519):```5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf```
- im_online (imon/Sr25519):```5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf```
- para_validator (para/Sr25519):```5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf```
- para_assignment (asgn/Sr25519):```5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf```
- authority_discovery (audi/Sr25519):```5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf```

```text
"session": {
  "keys": [
    [
    "5HeYFTPrAufPytrEGQUvSSLHbKSqb9e2NVaBRDTBvZ769kq3",
    "5HeYFTPrAufPytrEGQUvSSLHbKSqb9e2NVaBRDTBvZ769kq3",
      {
        "grandpa": "5GmbYPGYH1KxnHw1nXunNQjKJMfeFf2vtmAJJLKq9B856Nfx",
        "babe": "5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf",
        "im_online": "5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf",
        "para_validator": "5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf",
        "para_assignment": "5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf",
        "authority_discovery": "5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf",
        "beefy": "KWDw8nyTtutLkcAyJE6jFsaZFVPUkoZjzXF5U8XaYX4kAKGwD"
      }
    ]
},
```

### Session keys for Node II([validator](https://wiki.polkadot.network/docs/maintain-guides-how-to-validate-polkadot))

[Session keys](https://wiki.polkadot.network/docs/learn-cryptography#session-keys) are hot keys that must be kept online by a validator to perform network operations.

#### Generate a session key using the Sr25519 scheme.

```bash
polkadot key generate --scheme Sr25519 --password-interactive
```

```text
Key password:********
Secret phrase:       voice now jewel reopen distance notice cry output dwarf broccoli hint gaze
  Network ID:        substrate
  Secret seed:       0xe05300a2a2233a5ae2620737f7c96e61b9d98e8e027cda8f467de3160cfe0320
  Public key (hex):  0x6e7b0b13b3f316a794a644b50953b14b6238c7daddda688601a09e27dc662b13
  Account ID:        0x6e7b0b13b3f316a794a644b50953b14b6238c7daddda688601a09e27dc662b13
  Public key (SS58): 5EZZgACHStMKRERaEV6xdrB459SEunYxkNhWEiCBZB3WZ8WG
  SS58 Address:      5EZZgACHStMKRERaEV6xdrB459SEunYxkNhWEiCBZB3WZ8WG
```

#### Derive the [grandpa](https://wiki.polkadot.network/docs/glossary#grandpa-finality-gadget) key using Ed25519 scheme.

```bash
polkadot key inspect --password-interactive --scheme Ed25519 "voice now jewel reopen distance notice cry output dwarf broccoli hint gaze"
```

```text
Key password:********
Secret phrase:       voice now jewel reopen distance notice cry output dwarf broccoli hint gaze
  Network ID:        substrate
  Secret seed:       0xe05300a2a2233a5ae2620737f7c96e61b9d98e8e027cda8f467de3160cfe0320
  Public key (hex):  0xf18e8c9d4ef09dc3cdb87ed3a893a711949349e5582e26f2bbfc22f3ea338e0d
  Account ID:        0xf18e8c9d4ef09dc3cdb87ed3a893a711949349e5582e26f2bbfc22f3ea338e0d
  Public key (SS58): 5HXRk4txhxjAGHPVTyPgpu1zDeWtGruJWyPmih5bDq1rSkZf
  SS58 Address:      5HXRk4txhxjAGHPVTyPgpu1zDeWtGruJWyPmih5bDq1rSkZf
```

#### Derive the [beefy](https://wiki.polkadot.network/docs/learn-consensus#bridging-beefyt) key using EdDSA scheme.

```bash
polkadot key inspect --password-interactive --scheme Ecdsa "voice now jewel reopen distance notice cry output dwarf broccoli hint gaze"
```

```text
Key password:********
Secret phrase:       voice now jewel reopen distance notice cry output dwarf broccoli hint gaze
  Network ID:        substrate
  Secret seed:       0xe05300a2a2233a5ae2620737f7c96e61b9d98e8e027cda8f467de3160cfe0320
  Public key (hex):  0x027742dd115c12ea392832333fc36bedc943df190b0fe585c310241fc5bd284f53
  Account ID:        0x0f8fd6db89bfd4554c6efac2273b3f0621d88790262b881d958e113253fc2b7b
  Public key (SS58): KW5d2JWTUEQTPFvLgDQVuj3w1Ww6cqrwCn8vN4pt7hbtm7i3H
  SS58 Address:      5CR7Jd1YoKuKkEQ3dZn7X18tNcJFQPi4zVHTchJwGQTtyVmq
```

#### Generate the [babe](https://wiki.polkadot.network/docs/glossary#babe) key using Sr25519 scheme.

```bash
polkadot key generate --scheme Sr25519 --password-interactive
```

```text
Key password:********
Secret phrase:       expire sleep seminar sad eager faculty inflict great arm slice champion similar
  Network ID:        substrate
  Secret seed:       0xc35d77c56c05ff2365af8b8974403e1ac2c16c9da0958245efd63ea9a0f0372b
  Public key (hex):  0x0ca09f828a324f1161064a9508057e742f87abd4fc8624a8485a18f90b13982a
  Account ID:        0x0ca09f828a324f1161064a9508057e742f87abd4fc8624a8485a18f90b13982a
  Public key (SS58): 5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K
  SS58 Address:      5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K
```

#### Node II([validator](https://wiki.polkadot.network/docs/maintain-guides-how-to-validate-polkadot)) keys:
- key(Sr25519):```5EZZgACHStMKRERaEV6xdrB459SEunYxkNhWEiCBZB3WZ8WG```
- grandpa (gran/Ed25519):```5HXRk4txhxjAGHPVTyPgpu1zDeWtGruJWyPmih5bDq1rSkZf```
- beefy (beef/EdDSA):```KW5d2JWTUEQTPFvLgDQVuj3w1Ww6cqrwCn8vN4pt7hbtm7i3H```
- babe (babe/Sr25519):```5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K```
- im_online (imon/Sr25519):```5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K```
- para_validator (para/Sr25519):```5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K```
- para_assignment (asgn/Sr25519):```5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K```
- authority_discovery (audi/Sr25519):```5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K```

```text
"session": {
  "keys": [
    [
    "5EZZgACHStMKRERaEV6xdrB459SEunYxkNhWEiCBZB3WZ8WG",
    "5EZZgACHStMKRERaEV6xdrB459SEunYxkNhWEiCBZB3WZ8WG",
      {
        "grandpa": "5HXRk4txhxjAGHPVTyPgpu1zDeWtGruJWyPmih5bDq1rSkZf",
        "babe": "5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K",
        "im_online": "5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K",
        "para_validator": "5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K",
        "para_assignment": "5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K",
        "authority_discovery": "5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K",
        "beefy": "KW5d2JWTUEQTPFvLgDQVuj3w1Ww6cqrwCn8vN4pt7hbtm7i3H"
      }
    ]
},
```

### Create a custom chain specification

#### Generate a raw chain spec

```bash
polkadot build-spec --disable-default-bootnode --chain rococo-local > ./tmp/plain-relay-chain-spec-private-network.json
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/dedc7c48-91b5-47f2-af60-46a8d9c02b1e)

#### Modify the local relay chain specification

```text
"session": {
  "keys": [
    [
      "5HeYFTPrAufPytrEGQUvSSLHbKSqb9e2NVaBRDTBvZ769kq3",
      "5HeYFTPrAufPytrEGQUvSSLHbKSqb9e2NVaBRDTBvZ769kq3",
      {
        "grandpa": "5GmbYPGYH1KxnHw1nXunNQjKJMfeFf2vtmAJJLKq9B856Nfx",
        "babe": "5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf",
        "im_online": "5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf",
        "para_validator": "5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf",
        "para_assignment": "5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf",
        "authority_discovery": "5D5C1jcLDnzV4KXDsrbKpeM1bzBrCXJywAJk1DHraSdvBmQf",
        "beefy": "KWDw8nyTtutLkcAyJE6jFsaZFVPUkoZjzXF5U8XaYX4kAKGwD"
      }
    ],
    [
      "5EZZgACHStMKRERaEV6xdrB459SEunYxkNhWEiCBZB3WZ8WG",
      "5EZZgACHStMKRERaEV6xdrB459SEunYxkNhWEiCBZB3WZ8WG",
      {
        "grandpa": "5HXRk4txhxjAGHPVTyPgpu1zDeWtGruJWyPmih5bDq1rSkZf",
        "babe": "5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K",
        "im_online": "5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K",
        "para_validator": "5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K",
        "para_assignment": "5CMG9U65GY9gR4qoKHdZbSfAu9NEUo2CXAg9uSeZiv1ENM1K",
        "authority_discovery": "5FHneW46xGXgs5mUiveU4sbTyGBzmstUspZC92UhjJM694ty",
        "beefy": "KW5d2JWTUEQTPFvLgDQVuj3w1Ww6cqrwCn8vN4pt7hbtm7i3H"
      }
    ]
  ]
},
```

#### Generate the plain text chain specification
```bash
polkadot build-spec --chain=./tmp/plain-relay-chain-spec-private-network.json --raw --disable-default-bootnode > ./tmp/raw-relay-chain-spec-private-network.json
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/df6f6d77-ed39-4136-881b-1f83ef3207a4)

### Start Node I validator.

```bash
polkadot --base-path ./tmp/node01 --chain ./tmp/raw-relay-chain-spec-private-network.json --port 30333 --rpc-port 9945 --telemetry-url "wss://telemetry.polkadot.io/submit/ 0" --validator --rpc-methods Unsafe --name MyNode01 --password-interactive
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/5dc54a7c-b9b0-4fd1-a488-72b1b9f213df)

#### Add grandpa key to the keystore(in a new terminal).

 ```bash
polkadot key insert --base-path ./tmp/node01 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Ed25519 --suri "sick cry forget enroll retreat female slab uncover remember neutral time stadium" --password-interactive --key-type gran
```

#### Add beefy key to the keystore.

 ```bash
polkadot key insert --base-path ./tmp/node01 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Ecdsa --suri "sick cry forget enroll retreat female slab uncover remember neutral time stadium" --password-interactive --key-type beef
```

#### Add babe key to the keystore.

```bash
polkadot key insert --base-path ./tmp/node01 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Sr25519 --suri "vanish street orphan print magic atom link census clever sound quote logic" --password-interactive --key-type babe
```

#### Add imon key to the keystore.

```bash
polkadot key insert --base-path ./tmp/node01 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Sr25519 --suri "vanish street orphan print magic atom link census clever sound quote logic" --password-interactive --key-type imon
```

#### Add para key to the keystore.

```bash
polkadot key insert --base-path ./tmp/node01 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Sr25519 --suri "vanish street orphan print magic atom link census clever sound quote logic" --password-interactive --key-type para
```

#### Add asgn key to the keystore.

```bash
polkadot key insert --base-path ./tmp/node01 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Sr25519 --suri "vanish street orphan print magic atom link census clever sound quote logic" --password-interactive --key-type asgn
```

#### Add audi key to the keystore.

```bash
polkadot key insert --base-path ./tmp/node01 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Sr25519 --suri "vanish street orphan print magic atom link census clever sound quote logic" --password-interactive --key-type audi
```

#### Verify the seven files holding the keys created in the keystore.

```bash
ls -l ./tmp/node01/chains/rococo_local_testnet/keystore/
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/f5d984a3-78a6-4cef-92d2-ed8b5438a514)

#### Restart Node I.

```bash
polkadot --base-path ./tmp/node01 --chain ./tmp/raw-relay-chain-spec-private-network.json --port 30333 --rpc-port 9945 --telemetry-url "wss://telemetry.polkadot.io/submit/ 0" --validator --rpc-methods Unsafe --name MyNode01 --password-interactive
```

[PeerId](https://docs.libp2p.io/concepts/appendix/glossary/#peerid)

```bash
12D3KooWRVmQxg1iqCb92GPLETct2t1qPNpscQXe8YkLdyfNnZwx
```

### Start Node II validator.

```bash
polkadot --base-path ./tmp/node02 --chain ./tmp/raw-relay-chain-spec-private-network.json --port 30334 --rpc-port 9946 --telemetry-url "wss://telemetry.polkadot.io/submit/ 0" --validator --rpc-methods Unsafe --name MyNode02 --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWRVmQxg1iqCb92GPLETct2t1qPNpscQXe8YkLdyfNnZwx --password-interactive
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/076ba4a4-22a1-4e3d-bd6a-a9ea0ef509dd)

#### Add grandpa key to the keystore(in a new terminal).

 ```bash
polkadot key insert --base-path ./tmp/node02 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Ed25519 --suri "voice now jewel reopen distance notice cry output dwarf broccoli hint gaze" --password-interactive --key-type gran
```

#### Add beefy key to the keystore.

 ```bash
polkadot key insert --base-path ./tmp/node02 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Ecdsa --suri "voice now jewel reopen distance notice cry output dwarf broccoli hint gaze" --password-interactive --key-type beef
```

#### Add babe key to the keystore.

```bash
polkadot key insert --base-path ./tmp/node02 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Sr25519 --suri "expire sleep seminar sad eager faculty inflict great arm slice champion similar" --password-interactive --key-type babe
```

#### Add imon key to the keystore.

```bash
polkadot key insert --base-path ./tmp/node02 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Sr25519 --suri "expire sleep seminar sad eager faculty inflict great arm slice champion similar" --password-interactive --key-type imon
```

#### Add para key to the keystore.

```bash
polkadot key insert --base-path ./tmp/node02 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Sr25519 --suri "expire sleep seminar sad eager faculty inflict great arm slice champion similar" --password-interactive --key-type para
```

#### Add asgn key to the keystore.

```bash
polkadot key insert --base-path ./tmp/node02 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Sr25519 --suri "expire sleep seminar sad eager faculty inflict great arm slice champion similar" --password-interactive --key-type asgn
```

#### Add audi key to the keystore.

```bash
polkadot key insert --base-path ./tmp/node02 --chain ./tmp/raw-relay-chain-spec-private-network.json --scheme Sr25519 --suri "expire sleep seminar sad eager faculty inflict great arm slice champion similar" --password-interactive --key-type audi
```

#### Verify the seven files holding the keys created in the keystore.

```bash
ls -l ./tmp/node02/chains/rococo_local_testnet/keystore/
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/3495be8f-23cb-4e22-a487-db79acf17d27)

#### Restart Node II.

```bash
polkadot --base-path ./tmp/node02 --chain ./tmp/raw-relay-chain-spec-private-network.json --port 30334 --rpc-port 9946 --telemetry-url "wss://telemetry.polkadot.io/submit/ 0" --validator --rpc-methods Unsafe --name MyNode02 --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWRVmQxg1iqCb92GPLETct2t1qPNpscQXe8YkLdyfNnZwx --password-interactive
```

#### Connect to the [relay chain](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9945#/parachains/parathreads)

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/3cc114f2-2ceb-4dc2-91fa-1e3d9c6bb132)

#### Reserve a paraid

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/df2ce41d-b55e-4c67-afce-f377a9d6a719)

#### Confirm the events

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/efd8ab26-6909-48cd-a68e-001cea620fb2)

## Parachain (Private network of trusted collatores)

#### Clone the repo to get the [Cumulus SDK](https://github.com/paritytech/polkadot-sdk/tree/polkadot-v1.3.0/cumulus)

```bash
git clone --branch polkadot-v1.3.0 https://github.com/paritytech/polkadot-sdk.git
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/b6c5acb2-6e82-49ea-b760-3c8ce330e373)

#### Compile the polkadot parachain node

```bash
cd polkadot-sdk/cumulus/polkadot-parachain
cargo build --release --bin polkadot-parachain
```

#### Copy the polkadot-parachain binary

```bash
cd ../../../
cp -r ./polkadot-sdk/target/release/ ./binaries/polkadot-parachain
```

#### Generate two session keys using the Sr25519 scheme for [aura](https://wiki.polkadot.network/docs/glossary#aura)

```bash
./binaries/polkadot-parachain/polkadot-parachain key generate --scheme Sr25519 --password-interactive
```

```text
Key password:********
Secret phrase:       elevator exotic trick couple pave trend rude income spider leader first churn
  Network ID:        substrate
  Secret seed:       0xd3bb290be811bc5d9fb1762236edced9b43edac30e71a739dc3f90a8424d9a56
  Public key (hex):  0xaabf7651b017d3ffbe23674ea434f297ea468ffee560cfb55b03cbe505cb8d2f
  Account ID:        0xaabf7651b017d3ffbe23674ea434f297ea468ffee560cfb55b03cbe505cb8d2f
  Public key (SS58): 5FvasdQkzcgBBWVMTjminfi3Nk4s9ymZEJLxrcB3L9KikpRm
  SS58 Address:      5FvasdQkzcgBBWVMTjminfi3Nk4s9ymZEJLxrcB3L9KikpRm
```

```text
Key password:********
Key password: 
Secret phrase:       enemy bus social knock parrot maple into actress pause brisk know bracket
  Network ID:        substrate
  Secret seed:       0x8b334e8c01fe1542ccb715ad7f3cb9f2585106a8dd78aa0698564c2c9f42a1e6
  Public key (hex):  0x187e85ee44a439442b11d423f1aadbc3d1016f1208317326d1ad67d8bc9fe82c
  Account ID:        0x187e85ee44a439442b11d423f1aadbc3d1016f1208317326d1ad67d8bc9fe82c
  Public key (SS58): 5CcpbGUiNjeHH9tsCMQQBNwNxfTPGSWMV2i9uY9kx7MjCh9p
  SS58 Address:      5CcpbGUiNjeHH9tsCMQQBNwNxfTPGSWMV2i9uY9kx7MjCh9p
```

#### Generate the plain text chain specification

```bash
./binaries/polkadot-parachain/polkadot-parachain build-spec --disable-default-bootnode > ./tmp/plain-parachain-chain-spec-private-network.json
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/6e891bc6-6be5-48a0-8d8d-7b106bf35a14)

#### Modify the plain text chain specification

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/0b056eab-f9b8-45da-a47b-86d517b2fac2)

```bash
"aura": {
  "authorities":
    [
      "5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY",
      "5CcpbGUiNjeHH9tsCMQQBNwNxfTPGSWMV2i9uY9kx7MjCh9p"
    ]
},
```

#### Generate a raw chain specification file from the modified plain text chain specification

```bash
./binaries/polkadot-parachain/polkadot-parachain build-spec --chain ./tmp/plain-parachain-chain-spec-private-network.json --disable-default-bootnode --raw > ./tmp/raw-parachain-chain-spec-private-network.json
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/82b24e19-adb8-4aa8-8055-cd89c1a00a99)

#### Start the collator node

```bash
./binaries/polkadot-parachain/polkadot-parachain --collator --force-authoring --chain ./tmp/raw-parachain-chain-spec-private-network.json --base-path ./tmp/parachain/coll01 --port 40333 --rpc-port 8844 -- --execution wasm --chain ./tmp/raw-relay-chain-spec-private-network.json --port 30343 --rpc-port 9977 --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWRVmQxg1iqCb92GPLETct2t1qPNpscQXe8YkLdyfNnZwx --password-interactive
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/f1b69a8e-acdf-4c93-b470-ae5520c2025d)

#### Add aura key to the keystore.

```bash
./binaries/polkadot-parachain/polkadot-parachain key insert --base-path ./tmp/parachain/coll01 --chain ./tmp/raw-parachain-chain-spec-private-network.json  --scheme Sr25519 --suri "elevator exotic trick couple pave trend rude income spider leader first churn" --password-interactive --key-type aura
```

#### Verify the file holding the key created in the keystore.

```bash
ls -l ./tmp/parachain/coll01/chains/local_testnet/keystore/
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/e70b1064-14a9-4475-9b41-a21c80b6db7c)

#### Restart collator node.

```bash
./binaries/polkadot-parachain/polkadot-parachain --collator --force-authoring --chain ./tmp/raw-parachain-chain-spec-private-network.json --base-path ./tmp/parachain/coll01 --port 40333 --rpc-port 8844 -- --execution wasm --chain ./tmp/raw-relay-chain-spec-private-network.json --port 30343 --rpc-port 9977 --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWRVmQxg1iqCb92GPLETct2t1qPNpscQXe8YkLdyfNnZwx --password-interactive
```

#### Export the WebAssembly runtime

```bash
./binaries/polkadot-parachain/polkadot-parachain export-genesis-wasm --chain ./tmp/raw-parachain-chain-spec-private-network.json ./tmp/parachain-private-network-wasm
```

#### Generate a parachain genesis state

```bash
./binaries/polkadot-parachain/polkadot-parachain export-genesis-state --chain ./tmp/raw-parachain-chain-spec-private-network.json ./tmp/parachain-private-network-state
```

#### Register the parachain with the local [relay chain](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9945#/sudo)

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/d737761d-0cb5-41c4-9445-4741b9d8ed03)

#### Sudo transaction

Note: We are bypassing the steps required to acquire a parachain or parathread slot which normally is a parachain auction.

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/8db12fa5-6d64-485b-884b-400e33056495)

#### Testing the parachain.

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/33d45b11-a5d8-4d62-b8b8-0d3f852cb93a)

<hr>

# Zombienet setup

## Simple network

A simple [network specification](https://paritytech.github.io/zombienet/network-definition-spec.html) with two relay chain validators nodes and one collator.

#### Create the network specification file

```bash
[relaychain]
default_command = "polkadot"
chain = "rococo-local"

  [[relaychain.nodes]]
  name = "node01"
  validator = true

  [[relaychain.nodes]]
  name = "node02"
  validator = true

[[parachains]]
id = 2000
cumulus_based = true

  [parachains.collator]
  name = "collator01"
  command = "./binaries/polkadot-parachain/polkadot-parachain"
  args = ["--force-authoring","-lparachain=debug"]
```

#### Spawn a local testing network

```bash
zombienet-linux-x64 spawn network-specification.toml -p native
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/55006985-f370-41bb-95ae-737241d3c4af)

#### Testing the parachain

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/3f0b54b9-5a23-40a0-b3c1-5076d6240d00)

## Network with HRMP Channels

A [network specification](https://paritytech.github.io/zombienet/network-definition-spec.html) with tree relay chain validators nodes and two parahachains with four collators. This type of setup is used for building with the [hrmp-channels](https://wiki.polkadot.network/docs/build-hrmp-channels)


#### Create the network specification file

```bash
[settings]
node_spawn_timeout = 240

[relaychain]
default_command = "polkadot"
default_args = [ "-lparachain=debug,xcm=trace" ]
chain = "rococo-local"

	[[relaychain.nodes]]
	name = "node01"
	validator = true
	rpc_port = 9932
	ws_port = 9942
	balance = 2000000000000

	[[relaychain.nodes]]
	name = "node02"
	validator = true
	rpc_port = 9933
	ws_port = 9943
	balance = 2000000000000

	[[relaychain.nodes]]
	name = "node03"
	validator = true
	rpc_port = 9934
	ws_port = 9944
	balance = 2000000000000

[[parachains]]
id = 1013
cumulus_based = true

	[[parachains.collators]]
	name = "collator01-1013"
	validator = true
	command = "./binaries/polkadot-parachain/polkadot-parachain"
	rpc_port = 8933
	ws_port = 8943
	args = [
		"-lparachain=debug,runtime::bridge-hub=trace,runtime::bridge=trace,runtime::bridge-dispatch=trace,bridge=trace,runtime::bridge-messages=trace,xcm=trace",
		"--force-authoring"
	]

	# run bob as parachain collator
	[[parachains.collators]]
	name = "collator02-1013"
	validator = true
	command = "./binaries/polkadot-parachain/polkadot-parachain"
	rpc_port = 8934
	ws_port = 8944
	args = [
		"-lparachain=trace,runtime::bridge-hub=trace,runtime::bridge=trace,runtime::bridge-dispatch=trace,bridge=trace,runtime::bridge-messages=trace,xcm=trace",
		"--force-authoring"
	]

[[parachains]]
id = 1000
cumulus_based = true

	[[parachains.collators]]
	name = "collator01-1000"
	rpc_port = 9911
	ws_port = 9910
	command = "./binaries/polkadot-parachain/polkadot-parachain"
	args = [
		"-lparachain=debug,xcm=trace,runtime::bridge-transfer=trace"
	]

	[[parachains.collators]]
	name = "collator02-1000"
	command = "./binaries/polkadot-parachain/polkadot-parachain"
	args = [
		"-lparachain=debug,xcm=trace,runtime::bridge-transfer=trace"
	]

#[[hrmp_channels]]
#sender = 1000
#recipient = 1013
#max_capacity = 4
#max_message_size = 524288
#
#[[hrmp_channels]]
#sender = 1013
#recipient = 1000
#max_capacity = 4
#max_message_size = 524288
```

#### Spawn a local testing network

```bash
zombienet-linux-x64 spawn network-specification-hrmp.toml -p native
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/28579bc6-7a4d-4b99-ba64-d2f1d93fbd73)

#### Testing the parachains

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/b413f4d9-2200-4134-a827-f7e502d7a7c5)

<hr>
References:<br>
[Polkadot SDK(v1.3.0)](https://github.com/paritytech/polkadot-sdk/tree/polkadot-v1.3.0)<br>
[Cumulus SDK](https://github.com/paritytech/polkadot-sdk/tree/polkadot-v1.3.0/cumulus#cumulus-%EF%B8%8F)<br>
[Polkado(v1.3.0](https://github.com/paritytech/polkadot-sdk/tree/polkadot-v1.3.0/polkadot)<br>
[Zombienet](https://github.com/paritytech/zombienet)<br>

<hr>



List of [chain specs](https://github.com/paritytech/polkadot-sdk/tree/polkadot-v1.3.0/polkadot/node/service/chain-specs):
- [rococo.json](https://github.com/paritytech/polkadot-sdk/blob/polkadot-v1.3.0/polkadot/node/service/chain-specs/rococo.json)
- [kusama.json](https://github.com/paritytech/polkadot-sdk/blob/polkadot-v1.3.0/polkadot/node/service/chain-specs/kusama.json)
- [westend.json](https://github.com/paritytech/polkadot-sdk/blob/polkadot-v1.3.0/polkadot/node/service/chain-specs/westend.json)
- [wococo.json](https://github.com/paritytech/polkadot-sdk/blob/polkadot-v1.3.0/polkadot/node/service/chain-specs/wococo.json)


[acquire-a-testnet-slot](https://docs.substrate.io/tutorials/build-a-parachain/acquire-a-testnet-slot/)






[Parachain node for smart contracts](https://github.com/paritytech/polkadot-sdk/blob/polkadot-v1.3.0/cumulus/parachains/runtimes/contracts/contracts-rococo/README.md)


<hr>
<hr><hr><hr><hr><hr>

[The Parity Polkadot Blockchain SDK](https://github.com/paritytech/polkadot-sdk)


This directory currently contains runtimes for the Polkadot, Kusama, Westend, and Rococo networks. In the future, these will be relocated to the runtimes repository.
https://github.com/paritytech/polkadot-sdk/tree/master/polkadot 

https://doc.deepernetwork.org/tutorials/v3/cumulus/start-relay/


<hr>
https://docs.substrate.io/tutorials/build-a-parachain/<br>
https://wiki.polkadot.network/docs/build-pdk#your-go-to-overview-for-developing-a-parachain
<hr>

Functional pallets:

 - [pallet_assets](https://paritytech.github.io/substrate/master/pallet_assets/index.html)/[frame-assets](https://github.com/paritytech/polkadot-sdk/tree/master/substrate/frame/assets)
 - [pallet_collective](https://paritytech.github.io/substrate/master/pallet_collective/index.html)/[frame-collective](https://github.com/paritytech/polkadot-sdk/tree/master/substrate/frame/collective)
 - [pallet_utility](https://paritytech.github.io/substrate/master/pallet_utility/index.html)/[frame-utility](https://github.com/paritytech/polkadot-sdk/tree/master/substrate/frame/utility)
 - [pallet_contracts](https://docs.rs/pallet-contracts/24.0.0/pallet_contracts/)/[frame-contracts](https://github.com/paritytech/polkadot-sdk/tree/master/substrate/frame/contracts)/[crate](https://crates.io/crates/pallet-contracts)


[Extended Parachain Template](https://github.com/paritytech/extended-parachain-template/)<br>
[Substrate Parachain Template](https://github.com/substrate-developer-hub/substrate-parachain-template)<br>
[Substrate Contracts Node](https://github.com/paritytech/substrate-contracts-node)<br>
[Simulate Parachains](https://docs.substrate.io/test/simulate-parachains/)<br>
[Build a Parachain](https://docs.substrate.io/tutorials/build-a-parachain/)<br>
[Parachain Templates (EPT & FPT)](https://www.youtube.com/watch?v=zZvR1ii8X30)<br>
[Astar](https://github.com/AstarNetwork/Astar/tree/master)<br>
[Kusama](https://kusama.network/)<br>
[Overview of Polkadot and its Design Considerations](https://arxiv.org/abs/2005.13456.pdf)<br>

Examples:<br>
https://github.com/paritytech/cumulus/blob/master/parachains/runtimes/contracts/contracts-rococo/Cargo.toml<br>
https://github.com/paritytech/trappist/blob/e51c1fead095341210e2a7a5a5971900f476636c/runtime/trappist/src/contracts.rs<br>
https://github.com/paritytech/trappist/tree/main/runtime/trappist


![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/68949f9a-e38e-4378-9dfc-0a5ea4186c3e)


![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/d57957d9-840d-444f-85b5-74b7ddbc2bbe)

https://forum.polkadot.network/t/the-new-polkadot-community-testnet/4956
