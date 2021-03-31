# Subgraph

The Balancer Subgraph indexes data on the Balancer smart contracts with a graphql interface.  It updates data in response to function calls and contract events to maintain data on the `Vault`, `Pools`,  `AssetManagers` etc, to power frontend apps and integrations.

### Explore our data

Kovan: [https://thegraph.com/explorer/subgraph/balancer-labs/balancer-kovan-v2](https://thegraph.com/explorer/subgraph/balancer-labs/balancer-kovan-v2)

Mainnet: Coming soon

For how to use the subgraph, refer to the graph's documentation [https://thegraph.com/docs/introduction](https://thegraph.com/docs/introduction)

Github repository: [https://github.com/balancer-labs/balancer-subgraph-v2](https://github.com/balancer-labs/balancer-subgraph-v2)

### GraphQL Schema

The schema of GraphQL elements available is defined in [`/schema.graphql` ](https://github.com/balancer-labs/balancer-subgraph-v2/blob/master/schema.graphql)\`\`

The data included in this subgraph data layer is the data that is most applicable to our pool management frontend.  It aims at the very least to keep track of all the resources in the  `Vault` contract, and keep track of basic pool data.



