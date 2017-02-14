# BTC.com Pool API Doc

Using the API provided by the BTC pool to obtain the running status and user account information in real time.

## API structure

API Call the path as follows:

`https://${Endpoint}/${Version}/${Path}`

* Endpoint：
    * China `cn-pool.api.btc.com`
    * America `us-pool.api.btc.com`

* Version： `v1`
* Path: For specific API paths, see the definitions below

## Authentication

* Calling the user-related interface requires the `access_key` and` puid` authentication in the querystring.
    * AccessKey is the user credentials, corresponding to an account, please protect your own AccessKey.
    * Puid is the pool account id, used to distinguish between multiple subaccounts under an account.

* AccessKey and puid can go to the pool.btc.com login account and get it on the subaccount management page.

## Response

All response types are `application / json`, as follows:
   
``` json
{
    "data": ...,
    "err_no": 0,
    "err_msg": null 
}
```

In the response body, `data`, ` err_no` and `err_msg` are fixed fields. The meaning is as follows:

* `data`, Specific API response data.
* `error_no`, Error code, `0` for normal, not `0` is wrong, specifically view `error_msg` field.
* `error_msg`, Error message for debugging use. If there is no error, this field does not appear.


## Account

### account info

`GET /account/info`

#### Parameter

|name|type|note|
|---|----|----|
|access_key|str| |
|puid|int||

#### Response

```
{
    "err_no": 0,
    "data": {
        "user_id": 88888,
        "user_name": "spica",
        "address": "3NA8hsjfdgVkmmVS9moHmkZsVCoLxUkvvv ",
        "nmc_address": "",
        "rebates_address": "",
        "region": "America",
        "contact": {
            "mail": "",
            "phone": {
                "country": "86",
                "number": "133****3333"
            }
        },
        "alert": {
            "hashrate_max": "0",
            "hashrate_value": "0",
            "hashrate_unit": "T",
            "hashrate_alert": 0,
            "miner_max": "0",
            "miner_value": "0",
            "miner_alert": 0,
            "alert_interval": 6
        }
    }
}
```

### Account earn stats

`GET /account/earn-stats`

#### Parameter

|name|type|note|
|---|----|----|
|access_key|str| |
|puid|int||

#### Response

```
{
    "err_no": 0,
    "data": {
        "total_paid": "0",
        "pending_payouts": "0",
        "last_payment_time": "0",
        "earnings_today": "0",
        "earnings_yesterday": "0",
        "unpaid": "0"
    }
}
```

#### Account earn history

`GET /account/earn-history`

#### Parameter

|name|type|note|
|---|----|----|
|access_key|str| |
|puid|int||
|page|int||
|page_size|int|

#### Response

```
{
    "err_no": 0,
    "data": {
        "page": "1",
        "page_size": "50",
        "page_count": 1,
        "total_count": 50,
        "list": [
            {
                "date": 20170213,
                "earnings": 0,
                "payment_time": "0",
                "payment_tx": "",
                "address": "",
                "paid_amount": 0,
                "diff": 422170566884,
                "payment_mode": "PPS",
                "earnings_rate": 0
            },
            {
                "date": 20170212,
                "earnings": 1380002903,
                "payment_time": "2017-02-13 01:45:37",
                "payment_tx": "466af581cbf52af00dc0273ced28c17e8b7a7c6a92a4ce0ae104af4ff0d557c0",
                "address": "3NA8hsjfdgVkmmVS9moHmkZsVCoLxUkvvv",
                "paid_amount": 1380002903,
                "diff": 422170566884,
                "payment_mode": "PPS",
                "earnings_rate": 0.044
            },
            ...
        ]
    }
}
```

## Account HashRate

### Real-time hashrate
`GET /realtime/hashrate`

#### Parameter

|name|type|note|
|---|----|----|
|access_key|str| |
|puid|int||

#### Response

```
{

    "err_no": 0,
    "data": {
        "shares_15m": "22.88",
        "shares_15m_unit": "P",
        "shares_1d": "23.33",
        "shares_1d_unit": "P"
    }

}
```

### Real-time stats

`GET /worker/stats`

#### Parameter

|name|type|note|
|---|----|----|
|access_key|str| |
|puid|int||

#### Response

```
{
    "err_no": 0,
    "data": {
        "workers_active": 1999,
        "workers_inactive": 1,
        "workers_dead": 1,
        "shares_1m": "22.55",
        "shares_5m": "22.79",
        "shares_15m": "22.85",
        "workers_total": 2000,
        "shares_unit": "P"
    }
}
```