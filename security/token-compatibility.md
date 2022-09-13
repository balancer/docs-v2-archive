# Token Compatibility

## Overview

Some tokens are not compatible with Balancer because of how they interact with the Vault.

## Incompatibile Token Types

Examples of incompatible tokens include but are not limited to:

* Tokens that either change balances outside of `transfer`, `mint`, or `burn` or have transfers that do not result in exactly `amount` moving from `account0` to `account1`
  * Examples **include but are not limited to**:
    * Streaming tokens
    * Rebasing tokens
    * Deflationary tokens
    * Inflationary tokens
    * Tokens that charge transfer fees
* Proxy tokens with multiple entrypoints
* Tokens with `transfer` callbacks
