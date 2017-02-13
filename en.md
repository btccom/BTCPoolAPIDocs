# BTC.COM Pool API Doc

Your application can use BTC.COM provided mining pool API, real-time access to BTC.COM Pool
get status and user account details.

## API structure

The API is made up of `Domain`, `Version` and `Path`.
eg: `https://us-pool.api.btc.com/public/v1/pool/stats`

* domain: There are two nodes in China and the United States `cn-pool.api.btc.com` and `us-pool.api.btc.com`. Unless explicitly stated, the return result contains only the current node data.
* version: Current version v1
* Calling the user-related interface need to provide AccessKey and puid authentication, AccessKey is one of the important credentials, please protect your own AccessKey.
    * AccessKey and puid can go to the pool.btc.com login account and get it on the subaccount management page.
* All response types are `application / json`, as follows:
   
```
{
    "data": ...,        -- Specific API response results
    "err_no": 0,
    "err_msg": null 
}
```

* In the response body, `data`,` err_no` and `err_msg` are fixed fields. The meaning is as follows:
    * `data`，Specific API response data
    * `error_no`，Error code, `0` for normal, not `0` is wrong, specifically view `error_msg` field
    * `error_msg`，Error message for debugging use. If there is no error, this field does not appear.


## Pool interface

### Pool Stats

current node data： `GET https://us-pool.api.btc.com/public/v1/pool/stats`

all node data： `GET https://us-pool.api.btc.com/public/v1/pool/stats/merge`

##### Response：
```
{
    "err_no": 0,
    "data": {
        "shares": {
            "shares_1m": 114.6,
            "shares_5m": 115.6,
            "shares_15m": 115.8,
            "shares_unit": "P"
        },
        "reject": {
            "1m": 0,
            "5m": 0,
            "15m": 0.0007
        },
        "workers": 15424,
        "users": 555
    }
}
```


## Account

### account info

`GET https://us-pool.api.btc.com/v1/account/info`

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

`GET https://us-pool.api.btc.com/v1/account/earn-stats`

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

`GET https://us-pool.api.btc.com/v1/account/earn-history`

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
`GET https://us-pool.api.btc.com/v1/realtime/hashrate`

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

`GET https://us-pool.api.btc.com/v1/worker/stats`

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