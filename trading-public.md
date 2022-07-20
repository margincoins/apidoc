# Public Trading Endpoints

In order to discover other topics go back to [Table of Contents](README.md)

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
| :------------------ | :---------- | :---------- |
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
| :------------------ | :---------- | :---------- |
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

<br />

## Tickers

Returns all ticker data.

<pre> <b>GET</b> /v1/tickers </pre>

Ticker object fields and values are described below:

#### Ticker Object

| Field Name | Field Type | Description |
| :--------- | :--------- | :---------- |
| avg        | string     | Average price for last 24 hours. |
| ask        | string     | Best open ask order price. |
| bid        | string     | Best open bid order price. |
| change     | string     | Price change percentage between now and 24 hours ago. |
| qty        | string     | Price change quantity between now and 24 hours ago. |
| high       | string     | Highest price in last 24 hours. |
| last       | string     | Last trade's price value. |
| low        | string     | Lowest price in last 24 hours. |
| symbol     | string     | Pair Symbol, BTCUSDT |
| volume     | string     | 24-hour volume in base asset. |

Here is a sample ticker value:

```
[{
	"symbol": "BTCUSDT",
	"last": "48179",
	"ask": "48179",
	"bid": "48024",
	"high": "48179",
	"low": "48024",
	"avg": "48101.5",
	"change": "2.35",
	"qty": "123",
	"volume": "12345"
},
{
	"symbol": "ETHUSDT",
	...
}]
```

<br />

## Order Book

Order book endpoints returns best ask and bid orders of a pair. Returns maximum 50 rows for each side.

<pre> <b>GET</b> /v1/orderbook </pre>

**Querystrings**

| Name    | Optional | Description |
| :------ | :------- | :---------- |
| symbol  | No       | Pair symbol in BTCUSDT format |

To reduce the network usage, frequently recurring field names are minified.
- Field name **p**, represents **Price** as **string**.
- Field name **q**, represents **Quantity** as **string**.

Here an example response:

```
{
	"pairSymbol": "BTCUSDT",
	"asks": [{
		"p": "48179",
		"q": "0.18574314"
	},
	{
		"p": "48180",
		"q": "0.64521519"
	}],
	"bids": [{
		"p": "48076",
		"q": "1.02465343"
	},
	{
		"p": "48010",
		"q": "0.1"
	}]
}
```

<br />
