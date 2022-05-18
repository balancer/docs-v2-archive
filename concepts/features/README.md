# Features

## Overview

### Flash Loans

Flash Loans are uncollateralized loans that must be repaid (with interest) in the same transaction that they are borrowed. By consolidating multiple pools' tokens in the Vault, otherwise fragmented liquidity can be lent in a flash.

{% content-ref url="flash-loans.md" %}
[flash-loans.md](flash-loans.md)
{% endcontent-ref %}

### Asset Managers

{% hint style="info" %}
**Coming soon**! \
There are also new pool types in development that achieve the capital efficiency goals of Asset Managers in a manner that concentrates liquidity better, while requiring less maintenance. The first solutions will likely be released in that form.\
\
The original asset manager architecture can be used for cases where tokens need to be removed from a pool (e.g., for voting, or staking).
{% endhint %}

Asset Managers improve the capital efficiency of trading pools by reinvesting idle assets. Typical trading pools with deep liquidity benefit only from low slippage, but tokens not involved in trades do not contribute to the fees accrued by the pool. Asset Managers tap into that otherwise idle capital, using it on external protocols.&#x20;

{% content-ref url="asset-managers.md" %}
[asset-managers.md](asset-managers.md)
{% endcontent-ref %}
