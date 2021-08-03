# Exchange Listing

Token listings are managed in [this repository](https://github.com/balancer-labs/assets), with the following categories:

* `eligible.json`: assets that were eligible for liquidity mining in Balancer V1
* `listed.json`: assets listed on balancer.exchange
* `ui-not-eligible.json`: assets vetted by community members
* `untrusted.json`: assets that are incompatible with Balancer

Note that you can always create a pool or trade with an "unlisted" token, using the token address. You just can't search by token name, and the UIs will display a warning when interacting with "custom" tokens. \(Needless to say, do your own research when using such tokens!\)

There are two kinds of token "listings" on Balancer. The first is listing on the [Exchange](https://balancer.exchange/#/swap). Listed tokens appear on the main page as swapping options. It is possible to access unlisted pairs through a "deep link" with their addresses \(balancer.exchange/\#/swap/&lt;address1&gt;/&lt;address2&gt;\), but it displays unlisted tokens as addresses, and with a warning.

There is no formal process for listing tokens on the Balancer exchange UI. That is up to the team's discretion and relies on internal factors around trading volume, usage, and legitimacy. \(As noted above, it's always possible to trade tokens via contract address.\)

The listing criteria below are taken from this [accepted proposal](https://forum.balancer.finance/t/proposal-to-update-the-whitelist-process/217/4). \(We will endeavor to keep this up-to-date, but see the [Balancer Forum](https://forum.balancer.finance/) for the very latest.\)

