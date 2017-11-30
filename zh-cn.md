# BTC.com 矿池API文档

使用 BTC 矿池提供的 API，实时获取矿池运行状态及用户帐号信息。

## API 结构

调用路径如下：

`https://${Endpoint}/${Version}/${Path}`

其中：

* Endpoint：
    * 中国 `cn-pool.api.btc.com`
    * 美国 `us-pool.api.btc.com`
    * 深证 `sz-pool.api.btc.com`
    * 欧洲 `eu-pool.api.btc.com`

* Version： `v1`
* Path: 具体的 API 路径，参见下文定义。

## 鉴权
* 调用用户相关接口时需要在querystring提供 `access_key` 和 `puid` 鉴权。
    * AccessKey 是用户身份凭据，对应一个账户， 请用户保管好自己的AccessKey。
    * puid 是矿池子帐户id， 用来区分一个帐户下的多个子帐户。
* AccessKey 和 puid 可以到 pool.btc.com 登录账户，在子账户管理页获取。

## 响应

所有的响应类型均为`application/json`，如下：

``` json
{
    "data": ...,
    "err_no": 0,
    "err_msg": null 
}
```

响应体中的`data`、`err_no`和`err_msg`为固定字段，含义如下：
* `data`，具体 API 响应的数据。
* `error_no`，错误码，`0`为正常，非`0`为错误，具体查看`error_msg` 字段。
* `error_msg`，错误信息，供调试使用。如果没有错误，则此字段不出现。


## 帐号

### 用户信息

`GET /account/info`

#### 参数

|名称|类型|说明|
|---|----|----|
|access_key|str| |
|puid|int||

#### 响应

```
{
    "err_no": 0,
    "data": {
        "user_id": 88888,
        "user_name": "spica",
        "address": "3NA8hsjfdgVkmmVS9moHmkZsVCoLxUkvvv ",
        "nmc_address": "",
        "rebates_address": "",
        "region": "中国",
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

### 账户收益状态

`GET /account/earn-stats`

#### 参数

|名称|类型|说明|
|---|----|----|
|access_key|str| |
|puid|int||

#### 响应

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

#### 账户收益历史

`GET /account/earn-history`

#### 参数

|名称|类型|说明|
|---|----|----|
|access_key|str| |
|puid|int||
|page|int||
|page_size|int|

#### 响应

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

## 用户算力

### 实时算力

`GET /realtime/hashrate`

#### 参数

|名称|类型|说明|
|---|----|----|
|access_key|str| |
|puid|int||

#### 响应

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

### 实时统计

`GET /worker/stats`

#### 参数

|名称|类型|说明|
|---|----|----|
|access_key|str| |
|puid|int||

#### 响应

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