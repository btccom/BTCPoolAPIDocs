# BTC.COM 矿池API文档

您的应用可以使用 BTC.COM 提供的矿池API， 实时获取 BTC.COM Pool的运行状态以及用户的帐号详情。

## API结构

本API由Domain,Version和Path构成。 
例如： `https://cn-pool.api.btc.com/public/v1/pool/stats`

* Domain： 目前有中国和美国两个节点 `cn-pool.api.btc.com` 和 `us-pool.api.btc.com`。 除非明确声明，返回结果只包含当前节点数据。
* Version： 目前版本 v1。
* 调用用户相关接口时需要提供 AccessKey 和 puid 等相关参数鉴权, AccessKey是身份凭据之一, 请用户保管好自己的AccessKey。
    * AccessKey 和 puid 可以到 pool.btc.com 登录账户，在子账户管理页获取
* 所有的响应类型均为`application/json`，如下：
   
```
{
    "data": ...,        -- 具体的 API 响应结果
    "err_no": 0,
    "err_msg": null 
}
```

* 响应体中的`data`、`err_no`和`err_msg`为固定字段，含义如下：
    * `data`，具体 API 响应的数据
    * `error_no`，错误码，`0`为正常，非`0`为错误，具体查看`error_msg` 字段
    * `error_msg`，错误信息，供调试使用。如果没有错误，则此字段不出现。


## 矿池接口

### 矿池状态

当前节点： `GET https://cn-pool.api.btc.com/public/v1/pool/stats`

全部节点： `GET https://cn-pool.api.btc.com/public/v1/pool/stats/merge`

##### 响应：
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


## 帐号

### 用户信息

`GET https://cn-pool.api.btc.com/v1/account/info`

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

`GET https://cn-pool.api.btc.com/v1/account/earn-stats`

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

`GET https://cn-pool.api.btc.com/v1/account/earn-history`

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
`GET https://cn-pool.api.btc.com/v1/realtime/hashrate`

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

`GET https://cn-pool.api.btc.com/v1/worker/stats`

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