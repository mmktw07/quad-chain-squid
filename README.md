# Squid tracking USDC transfers across four chains

This [squid](https://docs.subsquid.io/) captures USDC Transfer events on ETH, BSC, Base and Moonbeam, stores them in the same database and serves the data over a common GraphQL API.

Data ingester ("processor") code for each network is located at the corresponding `src/` subdirectory: `src/eth`, `src/bsc`, `src/base` and`src/moonbeam`. The scripts file `commands.json` contains commands for running each processor (`process:eth`, `process:bsc`, `process:base` and `process:moonbeam` correspondingly). GraphQL server runs as a separate process started by `sqd serve`. You can also use `sqd run` to run all the services at once.

The squid uses [Subsquid Network](https://docs.subsquid.io/subsquid-network) as its primary data source.

Dependencies: Node.js, Docker, Git.

## Quickstart

```bash
# 0. Install @subsquid/cli a.k.a. the sqd command globally
npm i -g @subsquid/cli

# 1. Clone the repo
git clone https://github.com/subsquid-labs/quest-quad-chain-squid
cd quest-quad-chain-squid

# 2. Install dependencies
npm ci

# 3. Start containers for the Postgres database and the network query gateway
sqd up

# 4. Build and start the processors _in separate terminals_
sqd process:eth
sqd process:bsc
sqd process:base
sqd process:moonbeam

# 5. Start the GraphQL server by running in yet another terminal
sqd serve
```
A GraphiQL playground will be available at [localhost:4350/graphql](http://localhost:4350/graphql).
