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
  - [Node I](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#node-i)
    - [Generate the Sr25519 key for producing blocks using aura](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-the-sr25519-key-for-producing-blocks-using-aura)
    - [Generate Ed25519 key for finalizing blocks using grandpa](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-ed25519-key-for-finalizing-blocks-using-grandpa)
  - [Node II](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#node-ii)
    - [Generate the Sr25519 key for producing blocks using aura](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-the-sr25519-key-for-producing-blocks-using-aura-1)
    - [Generate Ed25519 key for finalizing blocks using grandpa](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-ed25519-key-for-finalizing-blocks-using-grandpa-1)
  - [Start the parachain nodes](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#start-the-parachain-nodes)
    - [Generate the plain text chain specification](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#generate-the-plain-text-chain-specification-1)
    - [Convert the chain specification to raw format](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#convert-the-chain-specification-to-raw-format)
    - [Start the node I](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#start-the-node-i)
      - [Add aura secret to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-aura-secret-to-the-keystore)
      - [Add grandpa secret to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-grandpa-secret-to-the-keystore)
    - [Start the node II](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#start-the-node-ii)
      - [Add aura secret to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-aura-secret-to-the-keystore-1)
      - [Add grandpa secret to the keystore](https://github.com/blue-freedom-technologies/test-network/blob/main/README.md#add-grandpa-secret-to-the-keystore-1)


 
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

#### Generate a session key using the Sr25519 scheme for Node I([validator](https://wiki.polkadot.network/docs/maintain-guides-how-to-validate-polkadot)).

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

#### Derive the [beefy](https://wiki.polkadot.network/docs/learn-consensus#bridging-beefyt) key using EdDSA scheme.

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

#### Generate the Sr25519 key for **producing blocks** using [babe](https://wiki.polkadot.network/docs/glossary#babe).

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

For Node I([validator](https://wiki.polkadot.network/docs/maintain-guides-how-to-validate-polkadot)) we will have :
- key(Sr25519):```5HeYFTPrAufPytrEGQUvSSLHbKSqb9e2NVaBRDTBvZ769kq3```
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



https://spec.polkadot.network/chap-host-api#sect-crypto-api

https://wiki.polkadot.network/docs/learn-cryptography#session-keys






#### Derive the Ed25519 key for **finality gadget for Polkadot** using [grandpa](https://wiki.polkadot.network/docs/glossary#grandpa-finality-gadget).

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

#### Derive the Sr25519 key for **the ImOnline module** using imon.

```bash
polkadot key inspect --password-interactive --scheme Sr25519 "sick cry forget enroll retreat female slab uncover remember neutral time stadium"
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

#### Derive the Sr25519 key for **the Parachain Validator Key** using para.

```bash
polkadot key inspect --password-interactive --scheme Sr25519 "sick cry forget enroll retreat female slab uncover remember neutral time stadium"
```





  
### Node I


#### Generate the Sr25519 key for **producing blocks** using [aura](https://wiki.polkadot.network/docs/glossary#aura).

```bash
polkadot key generate --scheme Sr25519 --password-interactive
```

```bash
Key password:********
Secret phrase:       wasp pudding interest planet plug fluid slush better perfect rather apart rich
  Network ID:        substrate
  Secret seed:       0x2ae747faf8ee10b161b124d7003eae01ed16e7905db94fb5489b3a9df6c38aeb
  Public key (hex):  0xdaa19095c45af73d76f80f4e1c4eb27a781831d1779abe27969969912cc0c21b
  Account ID:        0xdaa19095c45af73d76f80f4e1c4eb27a781831d1779abe27969969912cc0c21b
  Public key (SS58): 5H1NHpUiKnsibP7Q7777RszrcQfZbfHx7JhU56xX6MSfXohX
  SS58 Address:      5H1NHpUiKnsibP7Q7777RszrcQfZbfHx7JhU56xX6MSfXohX
```

#### Generate Ed25519 key for **finalizing blocks** using [grandpa](https://wiki.polkadot.network/docs/glossary#grandpa-finality-gadget)

```bash
polkadot key inspect --password-interactive --scheme Ed25519 "wasp pudding interest planet plug fluid slush better perfect rather apart rich"
```

```text
Key password:********
Secret phrase:       wasp pudding interest planet plug fluid slush better perfect rather apart rich
  Network ID:        substrate
  Secret seed:       0x2ae747faf8ee10b161b124d7003eae01ed16e7905db94fb5489b3a9df6c38aeb
  Public key (hex):  0xda2e9d5d15ec8a19e003bdcca060ad2605db9c9cafaf0f99a85d65e61d2d4f27
  Account ID:        0xda2e9d5d15ec8a19e003bdcca060ad2605db9c9cafaf0f99a85d65e61d2d4f27
  Public key (SS58): 5Gzn9GwG9aDNTzXjVDwsUtnoDJvwkeAakw5Dm9wkzNB1PA3A
  SS58 Address:      5Gzn9GwG9aDNTzXjVDwsUtnoDJvwkeAakw5Dm9wkzNB1PA3A
```

```text
Sr25519: 5H1NHpUiKnsibP7Q7777RszrcQfZbfHx7JhU56xX6MSfXohX for aura.
Ed25519: 5Gzn9GwG9aDNTzXjVDwsUtnoDJvwkeAakw5Dm9wkzNB1PA3A for grandpa.
```

### Node II

Keys are generated in a **air-gapped computer** that is deliberately separated from the internet for security reasons. This means that the computer does not have any physical or wireless connections to any other network that is connected to the internet.

#### Generate the Sr25519 key for **producing blocks** using [aura](https://wiki.polkadot.network/docs/glossary#aura).

```bash
polkadot key generate --scheme Sr25519 --password-interactive
```

```text
Key password:********
Secret phrase:       steel seed timber fitness type armed delay ready unlock enter garment sport
  Network ID:        substrate
  Secret seed:       0xe1966bcabb954981a50da6a226aa37df13776b065aa9ff7f2cb048bf851d2eba
  Public key (hex):  0x8060acb6b71fefc935bf6dc58b58fe1586329a61d82ad024388e6b1e84309d77
  Account ID:        0x8060acb6b71fefc935bf6dc58b58fe1586329a61d82ad024388e6b1e84309d77
  Public key (SS58): 5Ey2hq7w9itfw82QLo1AkWKfw8oWMsGaW6Cr5y6wk9Lu2vuK
  SS58 Address:      5Ey2hq7w9itfw82QLo1AkWKfw8oWMsGaW6Cr5y6wk9Lu2vuK
```

#### Generate Ed25519 key for **finalizing blocks** using [grandpa](https://wiki.polkadot.network/docs/glossary#grandpa-finality-gadget)

```bash
polkadot key inspect --password-interactive --scheme Ed25519 "steel seed timber fitness type armed delay ready unlock enter garment sport"
```

```text
Key password:********
Secret phrase:       steel seed timber fitness type armed delay ready unlock enter garment sport
  Network ID:        substrate
  Secret seed:       0xe1966bcabb954981a50da6a226aa37df13776b065aa9ff7f2cb048bf851d2eba
  Public key (hex):  0x91cf7f2223413db01956dc0cbe1efd66528af64501ba128922aebdde9a203fc9
  Account ID:        0x91cf7f2223413db01956dc0cbe1efd66528af64501ba128922aebdde9a203fc9
  Public key (SS58): 5FMtSTnHwwYonhH55u4h1DQvZYSBnKv3tRBfX8XLGxKuAsrx
  SS58 Address:      5FMtSTnHwwYonhH55u4h1DQvZYSBnKv3tRBfX8XLGxKuAsrx
```

```text
Sr25519: 5Ey2hq7w9itfw82QLo1AkWKfw8oWMsGaW6Cr5y6wk9Lu2vuK for aura.
Ed25519: 5FMtSTnHwwYonhH55u4h1DQvZYSBnKv3tRBfX8XLGxKuAsrx for grandpa.
```

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

[PeerId](https://docs.libp2p.io/concepts/appendix/glossary/#peerid)

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
