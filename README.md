Node.js API wrapper to BTC China exchange
===============

A node.js wrapper for the [Trading](http://btcchina.org/api-trade-documentation-en#trade_api_authentication) and [Market](http://btcchina.org/api-market-data-documentation-en) APIs exposed by bitcoin exchange [BTC China](https://www.btcchina.com).
You will need have a registered account with [BTC China](https://www.btcchina.com) and generated API keys to access the private methods.

Please contact support@btcchina.com if you are having trouble opening and account or generating an API key.

### Install

`npm install btc-china`

### Error handling
The first parameter to each API function is a callback function which is passed error and data objects.
The error object is an instance of [VError](https://github.com/davepacheco/node-verror) which is an extension of the standard Error object. The error message property will try and capture call the available information so problems in production can be diagnosed.

### Examples

```js
var BTCChina = require('btc-china');

// Test public data APIs
var publicClient = new BTCChina();

publicClient.getTicker(console.log, 'BTCCNY');

publicClient.getOrderBook(console.log, 'BTCCNY');

// get 2 trades since 1 minute ago
var since1Minute = new Date().getTime() / 1000 -  60;
//publicClient.getHistoryData(console.log, {limit: 2, since: since1Minute, sincetype: 'time' });

// WARNING never commit your API keys into a public repository.
var key = 'your-api-key';
var secret = 'your-api-secret';

var privateClient = new BTCChina(key, secret);

privateClient.getAccountInfo(console.log, 'all');

// add limit orders
privateClient.createOrder2(console.log, 'buy', 999, 0.0001, 'BTCCNY');
privateClient.createOrder2(console.log, 'sell', 8888, 0.0002, 'BTCCNY');

// add market order
privateClient.createOrder2(console.log, 'buy', null, 0.0001, 'BTCCNY');

// cancel an order
privateClient.cancelOrder(console.log, 1);

// get your open orders
privateClient.getOrders(console.log);
```

Please see exmaples.js for more examples