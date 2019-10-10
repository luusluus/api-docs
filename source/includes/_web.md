# Web Endpoints

The following set of calls can be used to access data via web endpoints. 

Call                                             | Description
-------------------------------------------------|---------------
[ticker (1.0)](#ticker-1-0)                      | XBridge 24hr trade summary (static list)
[ticker (2.0)](#ticker-2-0)                      | XBridge 24hr trade summary (dynamic list)
[history](#history)                              | XBridge 24hr trade history
[status](#status)                                | XBridge asset availability
[dxgetnetworktokens](#dxgetnetworktokens-web)    | Returns online XBridge assets
[xrgetnetworkservices](#xrgetnetworkservices-web)| Returns supported XRouter services










## ticker (1.0)

This call is used to view the XBridge trade summary for the past 24 hours and includes values of the inverse market. It is hard-coded to only include the following markets: BLOCK-LTC, LTC-BLOCK, LTC-SYS, SYS-LTC. 

Use [ticker (2.0)](#ticker-2-0) for a dynamic list that updates with whichever markets have had trades in the past 24 hours.


### Endpoint

<code class="api-call">[https://data.blocknet.co/api/v1.0/ticker](https://data.blocknet.co/api/v1.0/ticker)</code>


### Response Parameters

<aside class="success">
200 OK
</aside>

> Sample 200 Response

```cli
[
  {
    "symbol": "BLOCK-LTC",
    "open": 0.022216,
    "high": 0.022240,
    "low": 0.019437,
    "close": 0.019437,
    "volume": 27.945614,
    "lastprice": 0.019437,
    "timestamp": 1564444800
  },
  {
    "symbol": "LTC-BLOCK",
    "open": 45.012306,
    "high": 51.447171,
    "low": 44.96224,
    "close": 51.447171,
    "volume": 0.586885,
    "lastprice": 51.447171,
    "timestamp": 1564444800
  },
  {
    "symbol": "SYS-LTC",
    "open": 0.022216,
    "high": 0.022240,
    "low": 0.019437,
    "close": 0.019437,
    "volume": 27.945614,
    "lastprice": 0.019437,
    "timestamp": 1564444800
  },
  {
    "symbol": "LTC-SYS",
    "open": 45.012306,
    "high": 51.447171,
    "low": 44.96224,
    "close": 51.447171,
    "volume": 0.586885,
    "lastprice": 51.447171,
    "timestamp": 1564444800
  }
]
```

Parameter     | Type          | Description
--------------|---------------|-------------
symbol        | string        | The market in maker-taker format. Use the [status](#status) call to view the associated blockchain name for each ticker and the availabiity status.
open          | int           | Rolling 24hr opning trade price.
high          | int           | Highest trade price in the past 24hrs.
low           | int           | Lowest trade price in the past 24hrs.
close         | int           | Rolling 24hr closing trade price.
volume        | int           | Rolling 24hr trade volume denominated in the maker (first asset in the market pair).










## ticker (2.0)

This call is used to view a dynamic list of the XBridge trade summary for the past 24 hours and does *not* include values of the inverse market. Only markets that have had trades in the past 24 hours it will be included.


### Endpoint

<code class="api-call">[https://data.blocknet.co/api/v2.0/ticker](https://data.blocknet.co/api/v2.0/ticker)</code>


### Response Parameters

<aside class="success">
200 OK
</aside>

> Sample 200 Response

```cli
{
  "BLOCK-LTC": {
    "volume": "548.12435100",
    "price": "44.72284723252284837351528359",
    "open": "44.72284723252284837351528359",
    "high": "55.86592178770949720670391061",
    "low": "44.63642193485968680902170911",
    "close": "44.93061261235648931280709984",
    "timestamp": 1563219207
  },
  "LTC-BLOCK": {
    "volume": "29.70000000",
    "price": "0.022",
    "open": "0.022",
    "high": "0.022",
    "low": "0.022",
    "close": "0.022",
    "timestamp": 1563176655
  },
  "BTC-BLOCK": {
    "volume": "0.68000000",
    "price": "0.00021",
    "open": "0.00021",
    "high": "0.00021",
    "low": "0.0002",
    "close": "0.0002",
    "timestamp": 1563175709
  }
}
```

Parameter     | Type          | Description
--------------|---------------|-------------
Object        | object        | The market in maker-taker format and associated data. Use the [status](#status) call to view the associated blockchain name for each ticker and the availabiity status.
volume        | string        | Rolling 24hr trade volume denominated in the maker (first asset in the market pair).
price         | string        | The last trade price.
open          | string        | Rolling 24hr opning trade price.
high          | string        | Highest trade price in the past 24hrs.
low           | string        | Lowest trade price in the past 24hrs.
close         | string        | Rolling 24hr closing trade price.
timestamp     | int           | The Unix epoch timestamp of when the last trade took place.










## history

This call is used to view the XBridge trade history for the past 24 hours.


### Endpoint

<code class="api-call">[https://data.blocknet.co/api/v2.0/history](https://data.blocknet.co/api/v2.0/history)</code>


### Response Parameters

<aside class="success">
200 OK
</aside>

> Sample 200 Response

```cli
[
  {
    "timestamp": 1559970139,
    "txid": "4b409e5c5fb1986930cf7c19afec2c89ac2ad4fddc13c1d5479b66ddf4a8fefb",
    "to": "Bqtms8j1zrE65kcpsEorE5JDzDaHidMtLG",
    "xid": "9eb57bac331eab34f3daefd8364cdb2bb05259c407d805d0bd0c",
    "from": "BLOCK",
    "fromAmount": 0.001111,
    "to": "SYS",
    "toAmount": 0.001000
  },
  {
    "timestamp": 1559970139,
    "txid": "3de7479e8a88ebed986d3b7e7e135291d3fd10e4e6d4c6238663db42c5019286",
    "to": "Bqtms8j1zrE65kcpsEorE5JDzDaHidMtLG",
    "xid": "fd0fed3ee9fe557d5735768c9bdcd4ab2908165353e0f0cef0d5",
    "from": "BLOCK",
    "fromAmount": 0.001577,
    "to": "SYS",
    "toAmount": 0.001420
  },
  {
    "timestamp": 1559970139,
    "txid": "9cc4a0dae46f2f1849b3ab6f93ea1c59aeaf0e95662d90398814113f12127eae",
    "to": "BbrQKtutGBLuWHvq26EmHKuNaztnfBFWVB",
    "xid": "f74c614489bd77efe545c239d1f9a57363c5428e7401b2018d350",
    "from": "BLOCK",
    "fromAmount": 0.000231,
    "to": "SYS",
    "toAmount": 0.001100
  }
]
[{
  "timestamp":1564516002,
  "txid":"9f9592e4e5954645e8093c51e63cee73832b000e47dac45d8580deea3ebff8ef",
  "to":"BLOCK",
  "xid":"ca2c928552682d762d54b3cb124f9b663a7752faae11d13a",
  "from":"LTC",
  "fromAmount":"0.07393600",
  "toAmount":"3.80379800"
  
  },{"timestamp":1564515003,"txid":"fe7dac3f28ea7873aebc210ebb2fe77e60c8cd75204e2b37fb3ef0dac4a6213b","to":"BLOCK","xid":"6b169c7d40459411709a04405d3cd00d039ca78961536d57","from":"LTC","fromAmount":"0.07506700","toAmount":"3.85911500"},{"timestamp":1564513052,"txid":"edeffa602035e0f812f949206a2a9002fe1ebec9fb07148196db8b2fc082e6f1","to":"BLOCK","xid":"42e9a34f6334d58ca7aec96634ec80c902286a2088bfaf08","from":"LTC","fromAmount":"0.09047400","toAmount":"4.65205600"},{"timestamp":1564464003,"txid":"e4fd6f48dcf5fdc9af90f5237b496186a37af063a1fb07bab4a67db8e9763a0d","to":"BLOCK","xid":"27b3d828bae0c1cb9ee5cef8c6ff6609ada121d0f3676b0","from":"LTC","fromAmount":"0.13961800","toAmount":"6.27753800"},{"timestamp":1564463888,"txid":"317b70d0e54b25ed635cdc76fd85a3fc21b088bc0b4764246aefd68d7c812c29","to":"BLOCK","xid":"c822bca709ee64572a4888eda1419ac06cb5e9a016753f7","from":"LTC","fromAmount":"0.20779000","toAmount":"9.35310700"}]
```

Parameter     | Type          | Description
--------------|---------------|-------------
timestamp     | int           | Unix epoch timestamp of when the trade took place.
txid          | string        | Blocknet trade fee transaction ID.
to            | string        | Service Node that received the trade fee.
xid           | string        | XBridge transaction ID.
from          | string        | Taker trading asset; the ticker of the asset being sold by the taker.
fromAmount    | int           | Taker trading size.
to            | string        | Maker trading asset; the ticker of the asset being sold by the maker.
toAmount      | int           | Maker trading size.










## status

This call is used to view XBridge asset availability for trading and associated blockchain name for each ticker. It is hard-coded to only include assets for the markets returned in [ticker (1.0)](#ticker-1-0).

To view a full list of supported assets for trading, use [dxgetnetworktokens](#dxgetnetworktokens-web).


### Endpoint

<code class="api-call">[https://data.blocknet.co/api/v2.0/status](https://data.blocknet.co/api/v2.0/status)</code>


### Response Parameters

<aside class="success">
200 OK
</aside>

> Sample 200 Response

```cli
{
	"BLOCK": {
		"id":1,
		"name": "Blocknet",
		"frozen":0
	},
	"LTC": {
		"id":2,
		"name": "Litecoin",
		"frozen":0
	},
	"SYS": {
		"id":3,
		"name": "Syscoin",
		"frozen":0
	}
}
```

Parameter     | Type          | Description
--------------|---------------|-------------
Object        | object        | An object with the ticker's blockchain name, ID, and availability status.
id            | int           | The asset's ID number.
name          | string        | The asset's blockchain name.
frozen        | bool          | Online status. If `0`, the asset is online. If `1`, the asset is offline. Both assets of a market pair must show `0` for the market to be available for trading.










## dxgetnetworktokens (web)

This call is used to retrieve all the assets currently supported by the network for XBridge. This list may differ from the [compatibility list](https://docs.blocknet.co/protocol/xbridge/compatibility/#supported-digital-assets) due to assets being unofficially supported or assets not being supported by any nodes on the network.


### Endpoint

<code class="api-call">[https://data.blocknet.co/api/v2.0/dxgetnetworktokens](https://data.blocknet.co/api/v2.0/dxgetnetworktokens)</code>


### Response Parameters

<aside class="success">
200 OK
</aside>

> Sample 200 Response

```cli
[
  "LTC",
  "SYS",
  "MONA",
  "BLOCK"
]
```

Parameter     | Type          | Description
--------------|---------------|-------------
Array         | array         | An array of all the assets supported by the network for trading.










## xrgetnetworkservices (web)

This call is used to view the XRouter services currently supported on the network, along with the number of nodes supporting each service. XRouter SPV calls use the `xr::` namespace and XCloud services use the `xrs::` namespace.


### Endpoint

<code class="api-call">[https://data.blocknet.co/api/v2.0/xrgetnetworkservices](https://data.blocknet.co/api/v2.0/xrgetnetworkservices)</code>


### Response Parameters

<aside class="success">
200 OK
</aside>

> Sample 200 Response

```cli
{
  "reply": {
    "spvwallets": [ "xr::BLOCK", "xr::BTC", "xr::LTC", "xr::MNP", "xr::SYS", "xr::TBLOCK" ],
    "services": [ "xrs::BTCgetbestblockhash", "xrs::BTCgetblockhash", "xrs::BTCgettransaction", "xrs::SYSgetbestblockhash", "xrs::SYSgetblock", "xrs::SYSgetgovernanceinfo", "xrs::SYSgetmempool", "xrs::SYSlistoffers", "xrs::SYSofferinfo", "xrs::twilio" ],
    "nodecounts": {
      "xr::BLOCK": 27,
      "xr::BTC": 13,
      "xr::LTC": 21,
      "xr::MNP": 1,
      "xr::SYS": 9,
      "xrs::BTCgetbestblockhash": 12,
      "xrs::BTCgetblockhash": 12,
      "xrs::BTCgettransaction": 5,
      "xrs::SYSgetbestblockhash": 7,
      "xrs::SYSgetblock": 6,
      "xrs::SYSgetgovernanceinfo": 4,
      "xrs::SYSgetmempool": 4,
      "xrs::SYSlistoffers": 4,
      "xrs::SYSofferinfo": 4,
      "xrs::twilio": 1
    }
  },
  "uuid": "cd408df7-0ff8-4e29-b5cf-0148af83f93a"
}
```

Parameter     | Type          | Description
--------------|---------------|-------------
reply         | object        | An object containing information on supported services.
spvwallets    | array         | An array of supported SPV wallets, represented by the asset's ticker.
services      | array         | An array of supported XCloud services.
nodecounts    | object        | An object of supported SPV wallets and XCloud services with how many nodes support each.
-- key        | string        | The SPV wallet or XCloud service with it's namespace.
-- value      | int           | The amount of nodes supporting each respective service.
uuid          | string        | The response ID, which can be used to view this response again with [xrGetReply](#xrgetreply) (not supported via web API).






