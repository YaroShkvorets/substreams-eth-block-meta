# StreamingFast Substreams Template
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## Quick Start

Use this quickstart guide to set up your environment to use Substreams locally.

## Install Dependencies

### Install Rust

We're going to be using the [Rust programming language](https://www.rust-lang.org/), to develop some custom logic.

There are [several ways to install Rust](https://www.rust-lang.org/tools/install), but for the sake of brevity:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env # to configure your current shell
```

### Install `buf`

[https://buf.build](https://buf.build) is a tool used to simplify the generation of typed structures in any language. It invokes `protoc` and simplifies a good number of things. Substreams packages are compatible with [buf Images](https://docs.buf.build/reference/images).

See the [installation instructions here](https://docs.buf.build/installation).

## Obtain the `substreams` CLI tool

### From `brew` (for Mac OS)

```
brew install streamingfast/tap/substreams
```

### From pre-compiled binary

- Download the binary

```bash
# Use correct binary for your platform
wget https://github.com/streamingfast/substreams/releases/download/v0.0.12/substreams_0.0.12_linux_x86_64.tar.gz
tar -xzvf substreams_0.0.12_linux_x86_64.tar.gz
export PATH="`pwd`:$PATH"
```

> Check https://github.com/streamingfast/substreams/releases and use the latest release available

### Validation

Ensure that `substreams` CLI works as expected:

```
substreams -v
version (...)
```

## Generating Protobuf

```bash
substreams protogen ./substreams.yaml --exclude-paths="sf/ethereum,sf/substreams,google"
```

## Compile

At this point, we're ready to build our WASM binary and Protobuf definitions.

```bash
cargo build --target wasm32-unknown-unknown --release
```

The resulting WASM artifact will be found at `./target/wasm32-unknown-unknown/release/substreams_template.wasm`

## Run your Substream

We're now ready to run our example Substream!

> Don't forget to be at the root of the project to run the following commands

```bash
# to run the map module
substreams run -e api-dev.streamingfast.io:443 substreams.yaml map_transfers --start-block 12292922 --stop-block +1

# to run the store module (and the map module in the background)
substreams run -e api-dev.streamingfast.io:443 substreams.yaml store_transfers --start-block 12292922 --stop-block +1
```
Let's break down everything happening above.

- `substreams` is our executable
- `-e api-dev.streamingfast.io:443` is the provider going to run our Substreams
- `substream.yaml` is the path where we have defined our Substreams Manifest
- `map_transfers` (or `store_transfers`) this is the module which we want to run, defined in the manifest
- `--start-block 12292922` start from block `12292922`
- `--stop-block +1` only request a single block (stop block will be manifest's start block + 1)

Here is the example of an output of the `map_transfers` starting at `12292922` block for only `1` block.
The `[...]` was added to abbreviate the JSON output as there was a lot of ERC20 transfers.

```bash
2022-05-30T11:11:22.431-0400 INFO (substreams) connecting...
2022-05-30T11:11:22.620-0400 INFO (substreams) connected

----------- IRREVERSIBLE BLOCK #12,292,922 (12292922) ---------------
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: log: NFT Contract bc4ca0eda7647a8ab7c2061c2e118a18a936f13d invoked
map_transfers: message "eth.erc721.v1.Transfers": {
  "transfers": [
    {
      "from": "AAAAAAAAAAAAAAAAAAAAAAAAAAA=",
      "to": "q6cWGn+2nIjhbtn0Vc5it5HuTQM=",
      "trxHash": "z7GX9i7Fx/DnGhHsDEoOOUo6pB21OG6FUm+GyEs/J5Y=",
      "ordinal": "85"
    },
    <continued>,
    {
      "from": "AAAAAAAAAAAAAAAAAAAAAAAAAAA=",
      "to": "q6cWGn+2nIjhbtn0Vc5it5HuTQM=",
      "tokenId": "29",
      "trxHash": "z7GX9i7Fx/DnGhHsDEoOOUo6pB21OG6FUm+GyEs/J5Y=",
      "ordinal": "114"
    }
  ]
}
```

## Next Steps

Congratulations! You've successfully run a Substream.

- Read the documentation at https://github.com/streamingfast/substreams under _Documentation_.
- Look at [Playground](https://github.com/streamingfast/substreams-playground) for more learning examples.
