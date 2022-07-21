# WebSockets

In order to discover other topics go back to [Table of Contents](README.md)

## Introduction

- Websocket endpoint is wss://stream.margincoins.com.
- Authentication is not mandatory. Guest connections can receive public data.
- One time authentication is enough for each connection.

#### Supported Features

MarginCoins websocket supports these features:

- Public last trades
- Public ticker values
- Public orderbook values
- Last tradingview candle by different resolutions
- Balance change notifications for authenticated users
- Order execution informations for authenticated users

#### Message Format

All sending and receiving messages are in same format.

```
message-type | { json message body }
```

An example to subscribe tickers channel:

```
subscribe|{"c":"tickers","s":true}
```

<br />

## Authentication

Authentication is not mandatory for connecting to websocket and receiving the public trading data.
But receiving order status or balance change event data, the guest websocket connection must send successful authentication message at least one time.
For each TCP connection, one-time authentication is enough.

WebSocket authentication is similar to HTTP authentication. Same parameters are required:

- Public API Key
- Current Timestamp in Unix milliseconds
- Signature (HMAC)
- Nonce in unix milliseconds (timestamp tolerance duration)

#### Authentication with API Key Model

Model type is **api-login**. JSON Model fields are:

| Field Name | Field Type | Description |
| :--------- | :--------- | :---------- |
| pk         | string     | Public Key |
| s          | string     | Signature |
| ts         | integer    | Timestamp |
| n          | integer    | Nonce |

Your full string message should seem like this:

```api-login|{"pk":"Fc3x...Geq1s","s":"jM3...s8e","ts":1234567890,"n":15000}```

#### Authentication Response

After an authentication message is sent, server process the message and sends a response message to the client. If the response message tells the authentication is succesful, the TCP connection will be authenticated connection until it closed.

Response model type is api-auth. And it includes only one field with name v and boolean type. If the value is true, authentication is successful.

Here is a sample response message:

```api-auth|{"v":true}```

<br />

## Channel Subscriptions

Public trading data streams over websocket channels. In order to receive public trading data, you need to subscribe to a channel. 

- You can subscribe to a channel only one time. If you send same subscription message twice, subscription will not be doubled.
- All channel names are lowercase.
- Seperator symbol is **@** for parametered channels.
- Channel subscription message type is subscribe.
- Subscription model requires two fields:
  - **c :** channel name in string format.
  - **s :** in boolean format, true for subscribe, false for unsubscribe.

The Sample subscription message below is used for subscribing to tickers channel:

```subscribe|{"c":"tickers","s":true}```

To unsubscribe from a channel requires same message. The only thing you need to do is sending **s** value **false**.

#### Verifying Channel Subscription

When you subscribe to a channel, you receive the same message from server with subscribe-response message type.

Sample message:

```subscribe-response|{"c":"tickers","s":true}```

#### Parametered Channels

Some channels require parameters, usually pair symbol.
For example to subscribe order book of BTCUSDT pair, channel name should be specified with **@** seperator, like **orderbook@btcusdt**.

Sample message:

```subscribe|{"c":"orderbook@btcusdt","s":true}```

<br />

## Tickers Channel
