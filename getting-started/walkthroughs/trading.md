# Trade

## Overview

This walkthrough will go over the minimal steps to execute a standard trade. 

## Go to the Balancer App

Navigate to [https://app.balancer.fi/\#/trade](https://app.balancer.fi/#/trade)

## Connect your wallet

\(We're using MetaMask in this example\)

![](../../.gitbook/assets/export.jpg)

Click one of the "Connect wallet" buttons, click MetaMask, and connect your desired wallet in the extension popup.

## Select your trade tokens

### Pick your input token

![](../../.gitbook/assets/token_in_click_and_pick.jpg)

### Pick your output token

![](../../.gitbook/assets/token_out_click_and_pick.jpg)

## Enter trade amount

You can specify either an input amount or an output amount. In this example, we've entered an input amount

![](../../.gitbook/assets/10_enter_trade_amount%20%281%29.jpg)

## Approve the input token

{% hint style="info" %}
**Why?** You need to "Approve" tokens on Balancer \(and any other decentralized exchange\) because you need to authorize the exchange to move your input token on your behalf
{% endhint %}

{% hint style="info" %}
Because Balancer Protocol V2 is an entirely different system from V1, approvals unfortunately do not carry over; you will need to re-approve tokens.
{% endhint %}

Approving your token will issue an Ethereum transaction that will have a gas cost. This is **not** paying a fee for your trade; you will need to issue another transaction.

![](../../.gitbook/assets/screen-shot-2021-05-10-at-8.48.56-pm.png)

## Make your swap

Click swap and approve the transaction in MetaMask.

![](../../.gitbook/assets/11_approved_now_swap.jpg)

### Wait for your trade to get executed, and get your receipt!

![](../../.gitbook/assets/12_swapping%20%281%29.jpg)

![](../../.gitbook/assets/13_swapped.jpg)

