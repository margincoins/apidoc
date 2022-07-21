# Authenticated Trading Endpoints

In order to discover other topics go back to [Table of Contents](README.md)

## Place Order

That endpoint supports placing all type of orders such as limit, market, stop etc.

<pre> <b>POST</b> /sapi/v1/orders </pre>

Request body must be in JSON Format. Fields of JSON object are described below:

**Request JSON Model Fields**

| Name         | Optional | Description |
| :----------- | :------- | :---------- |
| symbol       | No       | Pair Symbol, like BTCUSDT. |
| type         | No       | Takes four values: MARKET, LIMIT, STOP_MARKET, STOP_LIMIT. |
| side         | No       | Takes two values: BUY or SELL. |
| price        | Yes      | Required if order type is limit or stop limit. |
| quantity     | Yes      | Required if order side is buy and order type is market or stop market. |
| total        | Yes      | Total is used for only market or stop market buy orders. |
| triggerPrice | Yes      | For stop orders, trigger price. |
| clientId     | Yes      | You can use that value to categorize your orders. It's kept in our db and you receive that value from reporting endpoints. |


If placing order is successful returns 200 OK.
Response body is in JSON format and includes order status and trade information.

Response model fields are described below:

| Field Name   | Field Type  | Description |
| :----------- | :---------- | :---------- |
| id           | string      | Unique order id. |
| ok           | boolean     | True, if order placed successfuly. |
| pairSymbol   | string      | Pair Symbol. |
| status       | string      | Order status; Open, Filled, Canceled. |
| quantity     | string      | Order quantity. |
| leftQuantity | string      | Left order quantity. If there is no trade, equals to quantity. |
| total        | string      | Price x quantity value. For market orders, the total value you requsted. |
| matchedTotal | string      | Sum of "price x quantity" values of all trades of the order. |
| trades       | object[]    | Order's trades. For market orders, that array will always elements. |

**Example Request**

```json
{
  "clientId": "web",
  "type": "market",
  "side": "buy",
  "symbol": "BTCUSDT",
  "price": "48185",
  "quantity": "0.00047732",
  "total": "23"
}
```

**Example Response**

```json
{
	"id": "1551482",
	"ok": true,
	"quantity": "0.00095464",
	"leftQuantity": "0.00047732",
	"matchedTotal": "22.9996642",
	"total": "23",
	"status": "Fill",
	"pairSymbol": "BTCUSDT",
	"lastTrades": [{
		"quantity": "0.00047732",
		"price": "48185"
	}]
}
```

<br />

## Cancel Order

You can cancel your all orders from this endpoint.

<pre> <b>DELETE</b> /sapi/v1/orders </pre>

**Querystrings**

| Name       | Optional | Description |
| :--------- | :------- | :---------- |
| orderId    | No       | Unique Order Id |

Order Id provided in response body on place operation. You can find your order id by using get order history and get open orders endpoints.
Successful cancel operations response 200 OK.

Extra information is included in body in JSON format.

```json
{
	"ok": true,
	"id": 1541007,
	"code": "SUCCESS"
}
```
