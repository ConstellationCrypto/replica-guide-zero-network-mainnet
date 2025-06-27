# Replica Guide

To use: You'll want to bring your own more performant RPC URL for the base chain instead of using the default. Configure this via the `EN_ETH_CLIENT_URL` environment variable in the `external-node` service in `docker-compose.yml`. Then run `docker compose up`.

A number of constants have already been set:

- the chain IDs for L1 (`EN_L1_CHAIN_ID: 1` which is ethereum) and L2 (`EN_L2_CHAIN_ID: 543210` which is zero network)
- the sequencer http url (`EN_MAIN_NODE_URL: https://zero-network.calderachain.xyz/http`), which allows for transactions sent to the replica node to be forwarded to the sequencer, effectively meaning you can use the replica node like a full RPC provider

The RPC is exposed via port 3060 (HTTP) and 3061 (websocket) as specified in the `docker-compose.yml`. After running `docker compose up`, you may query the RPC as follows:

```bash
curl -X POST \
     -H 'Content-Type: application/json' \
     -d '{"jsonrpc":"2.0","id":0,"method":"eth_chainId","params":[]}' \
localhost:3060

{"jsonrpc":"2.0","result":"0x849ea","id":0}
```

# More Notes

- The `docker-compose.yml` also includes services for prometheus and grafana, but these aren't necessary to spin up
- The postgres user password should probably be changed from the default value (`POSTGRES_PASSWORD` env variable)
