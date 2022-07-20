
## Exchange Info

Exchange Info endpoint  returns all assets and pairs in MarginCoins.

<pre> <b>GET</b> /v1/exchange/info </pre>

Response data is in JSON format. Asset data and pair data are described below.

```
{
    "assets": [
        { .. asset data .. },
        { .. asset data .. },
        ...
    ],
    "pairs: [
        { .. pair data .. },
        { .. pair data .. },
        ...
    ]
}
```

#### Asset Data

In response model, assets field contains an asset data array. Each asset data includes these fields:

| Field Name          | Field Type  | Description |
| ------------------- | ----------- | ----------- |
| symbol              | string      | Asset symbol, BTC. |
| name                | string      | Asset name, Bitcoin. |
| description         | string      | Asset description. |
| type                | string      | Asset type, CRYPTO or FIAT. |
| isEnabled           | boolean     | Asset status. |
| isWithdrawalEnabled | boolean     | Asset withdrawal status. |
| isDepositEnabled    | boolean     | Asset deposit status. |
| precision           | integer     | Asset withdrawal and deposit precision. |
| displayPrecision    | integer     | Asset display precision for user balance pages etc. |
| minDeposit          | string      | Minimum deposit quantity. |
| minWithdrawal       | string      | Minimum withdrawal quantity. |

<br />

#### Pair Data

In response model, pairs field contains an pair data array. Each pair data includes these fields:

| Field Name          | Field Type  | Description |
| ------------------- | ----------- | ----------- |
| symbol              | string      | Pair Symbol, BTCUSDT. |
| base                | string      | Base asset symbol, BTC. |
| quote               | string      | Quote asset symbol, USDT. |
| minExchangeValue    | string      | Min order total in quote, such as "5" in USDT. |
| leverageCross       | integer     | Cross margin leverage, 3. Zero for market disabled. |
| leverageIsolated    | integer     | Isolated margin leverage, 10. Zero for market disabled. |
| minPrice            | string      | Minimum price in quote asset. |
| maxPrice            | string      | Maximum price in quote asset. |
| quantityPrecision   | integer     | Maximum quantity precision. For example 8 for BTCUSDT. |
| pricePrecision      | integer     | Maximum price precision. |
| totalPrecision      | integer     | Total precision. Used for market buy orders. |
| commissionPrecision | integer     | Fee precision. Used for ui and display. |
| isEnabled           | boolean     | Pair system status. |
| displayOrder        | integer     | Pair recommended display order in websites, mobile applications etc. |
| status              | string      | Pair matching engine status. |
| marketTypes         | string[]    | Supported market types such as SPOT, CROSS, ISOLATED |
| orderTypes          | string[]    | Supported order types such as MARKET, LIMIT, STOP_MARKET. |
