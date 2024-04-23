---
sidebar_position: 2
---

# Optimism DEX Trades API

<head>
<meta name="title" content="How to Get Optimism Decentralized Exchange Data with Optimism DEX Trades API"/>
<meta name="description" content="Get on-chain data of any Optimism based DEX through our DEX Trades API."/>
<meta name="keywords" content="Optimism DEX Trades api,Optimism DEX Trades python api,Optimism DEX Trades token api,Optimism Dex NFT api, DEX Trades scan api, DEX Trades api, DEX Trades api docs, DEX Trades crypto api, DEX Trades blockchain api,Optimism network api, Optimism web3 api"/>
<meta name="robots" content="index, follow"/>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<meta name="language" content="English"/>

<!-- Open Graph / Facebook -->

<meta property="og:type" content="website" />
<meta
  property="og:title"
  content="How to Get Optimism Decentralized Exchange Data with Optimism DEX Trades API"
/>
<meta
  property="og:description"
  content="Get on-chain data of any Optimism based DEX through our DEX Trades API."
/>

<!-- Twitter -->

<meta property="twitter:card" content="summary_large_image" />
<meta property="twitter:title" content="How to Get Optimism Decentralized Exchange Data with Optimism DEX Trades API" />
<meta property="twitter:description" content="Get on-chain data of any Optimism based DEX through our DEX Trades API." />
</head>

If you were using Optimism RPC till now to get data, forget about it.

Our Optimism real time streams are perfect alternative for Optimism web3 subscribe.



In this section we will see how to get Optimism DEX trades information using our GraphQL APIs.

This Optimism API is part of our Early Access Program (EAP), which is intended for evaluation purposes. This program allows you to test the data and its integration into your applications before full-scale implementation. Read more [here](https://docs.bitquery.io/docs/graphql/dataset/EAP/)

## Subscribe to Latest Optimism Trades

This subscription will return information about the most recent trades executed on Optimism's DEX platforms.
You can find the query [here](https://ide.bitquery.io/Latest-trades-on-optimism#)

```
subscription {
  EVM(network: optimism) {
    Transfers(
      where: {
        Transfer: {
          Currency: {
            Fungible: false
            SmartContract: { is: "0x57aDd45EA2818fb327C740d123B366955E27d321" }
          }
        }
      }
    ) {
      Block {
        Hash
        Number
      }
      Transfer {
        Amount
        Currency {
          Name
          Symbol
          Native
        }
        Sender
        Receiver
      }
    }
  }
}


```

## Subscribe to Latest Price of a Token in Real-time

This query provides real-time updates on price of WETH `0x4200000000000000000000000000000000000006` in terms of USDC `0x7f5c764cbc14f9669b88837ca1490cca17c31607`, including details about the DEX, market, and order specifics. Find the query [here](https://ide.bitquery.io/Price-of-WETH-in-terms-of-USDC-on-Optimism#)

```
subscription {
  EVM(network: optimism) {
    DEXTrades(
      where: {Trade: {Sell: {Currency: {SmartContract: {is: "0x4200000000000000000000000000000000000006"}}}, Buy: {Currency: {SmartContract: {is: "0x7f5c764cbc14f9669b88837ca1490cca17c31607"}}}}}
    ) {
      Block {
        Time
      }
      Trade {
        Buy {
          Amount
          Buyer
          Seller
          Price_in_terms_of_sell_currency: Price
          Currency {
            Name
            Symbol
            SmartContract
          }
        }
        Sell {
          Amount
          Buyer
          Seller
          Price_in_terms_of_buy_currency: Price
          Currency {
            Symbol
            SmartContract
            Name
          }
        }
      }
    }
  }
}

```