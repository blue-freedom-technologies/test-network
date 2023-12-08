# test-network

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/68949f9a-e38e-4378-9dfc-0a5ea4186c3e)


![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/d57957d9-840d-444f-85b5-74b7ddbc2bbe)

https://forum.polkadot.network/t/the-new-polkadot-community-testnet/4956

## Introduction

All the setups demonstrated in this document were done using [ubuntu-22-04-3-lts](https://fridge.ubuntu.com/2023/08/11/ubuntu-22-04-3-lts-released/). It's assumed that [Rust](https://www.rust-lang.org/tools/install) is installed and running.


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

Table of Contents

Default setup

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
    - [Restart Node II](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#restart-node-ii)
 
Zombienet setup
  
<hr>

# Default setup

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
polkadot --base-path ./tmp/node02 --chain ./tmp/raw-relay-chain-spec-private-network.json --port 30334 --rpc-port 9946 --telemetry-url "wss://telemetry.polkadot.io/submit/ 0" --validator --rpc-methods Unsafe --name MyNode02 --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWP3xqW9rmC2qUy7mLvK6GWjBUVCbWhLrJRDvcDvz2dbKe --password-interactive
```

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

#### Generate a session key using the Sr25519 scheme.

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


#### Generate the plain text chain specification

```bash
./binaries/polkadot-parachain/polkadot-parachain build-spec --disable-default-bootnode > ./tmp/plain-parachain-chain-spec-private-network.json
```

#### Generate a raw chain specification file from the modified plain text chain specification

```bash
./binaries/polkadot-parachain/polkadot-parachain build-spec --chain ./tmp/plain-parachain-chain-spec-private-network.json --disable-default-bootnode --raw > ./tmp/raw-parachain-chain-spec-private-network.json
```

Start the collator Node I

```bash
./binaries/polkadot-parachain/polkadot-parachain --collator --force-authoring --chain ./tmp/raw-parachain-chainspec.json --base-path ./tmp/parachain/coll01 --port 40333 --rpc-port 8844 -- --execution wasm --chain ./tmp/raw-relay-chain-spec-private-network.json --port 30343 --rpc-port 9977 --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWNq7DyDjscNDe8ASAQnVmRT9RaHqvvQ1UjRHkURbfbw87 --password-interactive
```


./binaries/polkadot-parachain/polkadot-parachain key insert --base-path ./tmp/parachain/coll01 --chain ./tmp/raw-parachain-chainspec.json --scheme Sr25519 --suri "elevator exotic trick couple pave trend rude income spider leader first churn" --password-interactive --key-type aura


./target/release/node-template key insert --base-path /tmp/node01 \
  --chain customSpecRaw.json \
  --scheme Sr25519 \
  --suri <your-secret-seed> \
  --password-interactive \
  --key-type aura



https://spec.polkadot.network/chap-host-api#sect-crypto-api



<hr>
<hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr><hr>




### Start the rococo-chain

List of [chain specs](https://github.com/paritytech/polkadot-sdk/tree/polkadot-v1.3.0/polkadot/node/service/chain-specs):
- [rococo.json](https://github.com/paritytech/polkadot-sdk/blob/polkadot-v1.3.0/polkadot/node/service/chain-specs/rococo.json)
- [kusama.json](https://github.com/paritytech/polkadot-sdk/blob/polkadot-v1.3.0/polkadot/node/service/chain-specs/kusama.json)
- [westend.json](https://github.com/paritytech/polkadot-sdk/blob/polkadot-v1.3.0/polkadot/node/service/chain-specs/westend.json)
- [wococo.json](https://github.com/paritytech/polkadot-sdk/blob/polkadot-v1.3.0/polkadot/node/service/chain-specs/wococo.json)

#### Generate the plain text chain specification

```bash
./binaries/polkadot-parachain/polkadot-parachain build-spec --disable-default-bootnode > ./tmp/plain-parachain-chainspec-private-network.json
polkadot build-spec --chain rococo-local > rococo-chain-spec.json
```

#### Modify the plain text chain specification

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/3e8d21ff-6dfb-4db1-9eea-431621485db8)

Modify aura field to specify the nodes with the authority to create blocks by adding the Sr25519 SS58 address keys for each network participant

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/25ef68b4-af34-4033-9dc9-62332195080d)

#### Convert the chain specification to raw format

```bash
./binaries/polkadot-parachain/polkadot-parachain build-spec --chain=./tmp/plain-parachain-chainspec-private-network.json --raw --disable-default-bootnode > ./tmp/raw-parachain-chainspec-private-network.json
```

#### Start the node I
```bash
./binaries/polkadot-parachain/polkadot-parachain  --base-path ./tmp/node01   --chain ./tmp/raw-parachain-chainspec-private-network.json --port 30333 --rpc-port 9945 --telemetry-url "wss://telemetry.polkadot.io/submit/ 0" --validator --rpc-methods Unsafe --name MyNode01 --password-interactive
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/28258dc5-86a0-4e78-b450-4b431a2f5f58)



```text
12D3KooWRHQKBTnjmsmq1Jeq9CVQBXYgh5SZKJnyeNBH3VAxWA3p
```

#### Add [aura](https://wiki.polkadot.network/docs/glossary#aura) secret to the keystore.

```bash
./binaries/polkadot-parachain/polkadot-parachain key insert --base-path ./tmp/node01 --chain ./tmp/raw-parachain-chainspec-private-network.json --scheme Sr25519 --suri "sea decline anger behave eyebrow addict junior never brief island copy peanut" --password-interactive  --key-type aura
```

```bash
ls -l ./tmp/node01/chains/local_testnet/keystore
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/1e5b9cbe-53aa-4068-be5e-42ce5f45cd61)

#### Add [grandpa](https://wiki.polkadot.network/docs/glossary#grandpa-finality-gadget) secret to the keystore.

```bash
./binaries/polkadot-parachain/polkadot-parachain key insert --base-path ./tmp/node01 --chain ./tmp/raw-parachain-chainspec-private-network.json --scheme Ed25519 --suri "sea decline anger behave eyebrow addict junior never brief island copy peanut" --password-interactive --key-type gran
```

```bash
ls -l ./tmp/node01/chains/local_testnet/keystore
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/2d78dc67-545b-4995-b66f-4ed4d3ec3e4b)

Copy the [PeerId](https://docs.libp2p.io/concepts/appendix/glossary/#peerid) from the node I.

#### Start the node II

```bash
./binaries/polkadot-parachain/polkadot-parachain --base-path ./tmp/node02 --chain ./tmp/raw-parachain-chainspec-private-network.json --port 30336 --rpc-port 9946 --telemetry-url "wss://telemetry.polkadot.io/submit/ 0" --validator --rpc-methods Unsafe --name MyNode02 --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWRHQKBTnjmsmq1Jeq9CVQBXYgh5SZKJnyeNBH3VAxWA3p --password-interactive
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/4e9848ea-086f-498b-b991-dccae072ca24)

[PeerId](https://docs.libp2p.io/concepts/appendix/glossary/#peerid)

```text
12D3KooWKaf2H6rj7fZ9y5KUCB7vaV8tDA6EUsithWRgW9R53u1L
```

#### Add [aura](https://wiki.polkadot.network/docs/glossary#aura) secret to the keystore.

```bash
./binaries/polkadot-parachain/polkadot-parachain key insert --base-path ./tmp/node02 --chain ./tmp/raw-parachain-chainspec-private-network.json --scheme Sr25519 --suri "behind paper spike lonely ring blood alert ribbon window layer ring accuse" --password-interactive --key-type aura
```

#### Add [grandpa](https://wiki.polkadot.network/docs/glossary#grandpa-finality-gadget) secret to the keystore.

```bash
./binaries/polkadot-parachain/polkadot-parachain key insert --base-path ./tmp/node02 --chain ./tmp/raw-parachain-chainspec-private-network.json --scheme Ed25519 --suri "behind paper spike lonely ring blood alert ribbon window layer ring accuse" --password-interactive --key-type gran
```

```bash
ls -l ./tmp/node02/chains/local_testnet/keystore
```

![image](https://github.com/blue-freedom-technologies/test-network/assets/142290531/61cead0b-9018-427c-934b-114157d9d736)

<hr>




https://docs.substrate.io/tutorials/build-a-blockchain/add-trusted-nodes/#enable-other-participants-to-join































[acquire-a-testnet-slot](https://docs.substrate.io/tutorials/build-a-parachain/acquire-a-testnet-slot/)

# Zombienet setup

## Relay Chain

## Parachain

Spawn a local testing network:

```bash
 zombienet-linux-x64 spawn dev-rococo-local.toml -p native
```

```text
Key password: 
Secret phrase:       airport crumble matter grunt vicious excite thing unable object opera second deer
  Network ID:        substrate
  Secret seed:       0xde2c289cf3a329580f2bfc98d3c298ff137443f18ea8e3d24917092d947b57f0
  Public key (hex):  0xd85eeaaa1b26ac4f1ebeb9159def66b36d5dc339cdcf12c8e5828d553b33a245
  Account ID:        0xd85eeaaa1b26ac4f1ebeb9159def66b36d5dc339cdcf12c8e5828d553b33a245
  Public key (SS58): 5GxQPwioR7rSfCE9oU6eBGKncxXPXdkm7RkF36D3LDdwsuKw
  SS58 Address:      5GxQPwioR7rSfCE9oU6eBGKncxXPXdkm7RkF36D3LDdwsuKw
```


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


A minimal configuration example with two validators and one parachain:

```bash
[settings]
timeout = 1000

[relaychain]
default_image = "paritypr/polkadot-debug:master"
chain = "rococo-local"

  [[relaychain.nodes]]
  name = "alice"

  [[relaychain.nodes]]
  name = "bob"

[[parachains]]
id = 100

  [parachains.collator]
  name = "collator01"
  image = "paritypr/colander:master"
  command = "adder-collator"
```

<hr>



[Parachain node for smart contracts](https://github.com/paritytech/polkadot-sdk/blob/polkadot-v1.3.0/cumulus/parachains/runtimes/contracts/contracts-rococo/README.md)

### Chain specification



```bash
polkadot key inspect --password-interactive --scheme Ed25519 "dish reveal swallow tonight city early exhibit return able entry estate host"
```



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
