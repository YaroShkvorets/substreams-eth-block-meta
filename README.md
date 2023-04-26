# Block Meta Subgraph

This subgraph indexes Ethereum blocks meta data using corresponding substream
Allows you to query information like:
- What is the block at the start of day June 30th, 2022?
- What is the block at the end of July 2022?

## Requirements

- Rust: `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
- Docker: `https://docs.docker.com/desktop/`
- The Graph CLI: `npm i -g @graphprotocol/graph-cli`
- Substreams CLI: `https://substreams.streamingfast.io/getting-started/installing-the-cli`

## Indexing the subgraph locally

- Set env variables (generate $PINAX_KEY on https://pinax.network)
```
export SUBSTREAMS_ENDPOINT=https://eth-mar.firehose.pinax.network:9000
export SUBSTREAMS_API_TOKEN=$(curl https://auth.pinax.network/v1/auth/issue -s --data-binary '{"api_key":"'$PINAX_KEY'"}' | jq -r .token)
export ETH_MAINNET_RPC="http://eth-evmr73.mar.eosn.io:8080" # or another Ethereum RPC or EVMX endpoint
```
- Start graph node and wait until all 4 containers start up
```
cd graph-node
./up.sh     // script that starts docker containers needed to run graph node
```
- Now switch to another terminal and build and deploy substream and subgraph
```
make deploy_local
```

If everything went well you should see messages like `Applying 3 entity operation(s), block_hash: 0xd4e56...`.
If not and you get ECONNRESET error, wait a bit more until graph-node fully starts up, and try again.

At that point you can open http://127.0.0.1:8000/subgraphs/name/block_meta/graphql and run a query like
```
query MyQuery {
  blockMetas(first: 5) {
    id
    hash
    number
    timestamp
  }
}
```
