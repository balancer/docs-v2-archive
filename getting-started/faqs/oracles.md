# Oracles

## What are Balancer Price Oracles?

Balancer V2 introduces price oracles that are resistant to sandwich attacks by leveraging accumulators. There are two types of oracles that can be queried:

* Instant — A more up-to-date price but less resilient to manipulation
* Resilient — Less up-to-date but more resilient to manipulation

## How do I decide which type of Oracle to choose?

Choosing a price type varies depending on each use case. For example, lending protocols will likely use a Resilient Oracle while prediction markets could use the Instant Price Oracle.

