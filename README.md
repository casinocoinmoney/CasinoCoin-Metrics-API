# CasinoCoin (CSC) Metrics API for market trading data on XRP Ledger DEX
#### Version 1, dated 5th May 2021

## Endpoint

```
https://api.casinocoin.info/metrics
```

## Information returned


| Root Property | Description |
| --- | --- |
| `serverTimeGMT` | Timestamp of the server at the time of processing the request. |
| `tradedPairs` | Array of objects for each CSC currency pair directly traded on the DEX. |
| `calculatedPairs` | Array of objects for some calculated equivalent pairs, based on actual trades from other liquid pairs.  Currently only CSC/USD calculated pairing available. |


## tradedPairs
### For each pair:

| Property | Description |
| --- | --- |
| `sourceExchangeCode` | Code for source of trade information of the reported pair |
| `sourceExchangeName` | Descriptive name for source of trade information of the reported pair |
| `pair` | Currency pair reported with middle slash |
| `pairBase` | Base currency reported (always "CSC") |
| `pairQuote` | Quote currency reported |
| `high24hrGMT` | Highest price recorded within the current GMT day starting at 00:00 GMT |
| `low24hrGMT` | Lowest price recorded within the current GMT day starting at 00:00 GMT |
| `high24hrRolling` | Highest price recorded within the current 24-hour rolling period |
| `low24hrRolling` | Lowest price recorded within the current 24-hour rolling period |
| `percentChange24hrRolling` | Percentage price change on this pair from end of previous rolling 24-hour period to now (`serverTimeGMT`) |
| `priceHighestBid` | Highest bid price on the order books at time of the request |
| `priceLowestAsk` | Lowest ask price on the order books at time of the request |
| `priceSpread` | Bid-Ask price spread |
| `priceMid` | Mid price between `priceHighestBid` and `priceLowestAsk` |
| `priceLastTraded` | Weighted average price of all orders of the pair that were executed together most recently |
| `volumeBase24hrRolling` | Volume of base currency (CSC) traded within the current 24-hour rolling period |
| `volumeQuote24hrRolling` | Volume of quote currency (`pairQuote`) traded within the current 24-hour rolling period |

#### Example:
```
"tradedPairs": [
    {
      "sourceExchangeCode": "XRPLDEX",
      "sourceExchangeName": "XRP Ledger Decentralized Exchange",
      "pair": "CSC/XRP",
      "pairBase": "CSC",
      "pairQuote": "XRP",
      "high24hrGMT": 0.002715500002723885,
      "low24hrGMT": 0.00239047619047619,
      "high24hrRolling": 0.002715500002723885,
      "low24hrRolling": 0.00239047619047619,
      "percentChange24hrRolling": -3.7511848364149567,
      "priceHighestBid": 0.0024449877756395413,
      "priceLowestAsk": 0.002609999996751946,
      "priceSpread": 0.00016501222111240402,
      "priceMid": 0.002527493886195743,
      "priceLastTraded": 0.002458320511854315,
      "volumeBase24hrRolling": 36281791.87295876,
      "volumeQuote24hrRolling": 91256.529869
    },
},
...
]
```



## calculatedPairs
### For each pair:
| Property | Description |
| --- | --- |
| `calculatedFromPair` | Pair used to synthetically calculate equivalent trade pairing reported |
| `pair` | Currency pair reported with middle slash |
| `pairBase` | Base currency reported (always "CSC") |
| `pairQuote` | Quote currency reported |
| `sourceExchangeCode` | Code for source of trade information of the `calculatedFromPair` pair |
| `sourceExchangeName` | Descriptive name for source of trade information of the `calculatedFromPair` pair |
| `high24hrRolling` | Highest price recorded within the current 24-hour rolling period |
| `low24hrRolling` | Lowest price recorded within the current 24-hour rolling period |
| `percentChange24hrRolling` | Percentage price change on this calculated pair from end of previous rolling 24-hour period to now (`serverTimeGMT`) |
| `priceMid` | Mid price considered as current equivalent price now |
| `volumeBase24hrRolling` | Volume of base currency (CSC) traded within the current 24-hour rolling period |
| `volumeQuote24hrRolling` | Equivalent calculated volume of quote currency (`pairQuote`) traded via `calculatedFromPair` within the current 24-hour rolling period |


#### Example:
```
"calculatedPairs": [
    {
      "calculatedFromPair": "CSC/XRP",
      "pair": "CSC/USD",
      "pairBase": "CSC",
      "pairQuote": "USD",
      "sourceExchangeCode": "XRPLDEX",
      "sourceExchangeName": "XRP Ledger Decentralized Exchange",
      "high24hrRolling": 0.004136998750000001,
      "low24hrRolling": 0.003426974104859334,
      "percentChange24hrRolling": -0.9203194106264986,
      "priceMid": 0.003449704450027308,
      "volumeBase24hrRolling": 34300634.22536636,
      "volumeQuote24hrRolling": 126064.3923559277
    }
]
```