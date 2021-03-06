# 财经日历外部接口文档（新）

## 1. 简介

华尔街见闻财经日历对外接口文档（新版）

## 2. 修改记录

| Version | Release date | Comments |
| :-- | :-- | :-- |
| v1.0 | 2018-05-15 |  |

## 3. 调用

### 3.1 获取宏观日历列表

通过开始、结束日期的时间戳来获取财经日历列表，最大时间跨度为 1 日。

`GET  /finance/macrodatas?start={timestamp}&end={timestamp}`

#### Request Parameters

| Name        | Required |  Type  | Description     |
| :---------- | :------: | :----: | :-------------- |
| start       |   yes    | int64  | 开始日期：时间戳 |
| end         |   yes    | int64  | 结束日期：时间戳 |
| importances |          | string | 重要性，1-3，以英文逗号隔开 |

#### Response

| Name                |  Type   | Description       |
| :------------------ | :-----: | :---------------- |
| id                  | int64   | id |
| public_date         | int64   | 数据发布时间，时间戳，转换后显示为北京时间12:02的数据为公布时间待定的事件 |
| observation_date    | string  | 数据参考时间 |
| wscn_ticker         | string  | 唯一码 |
| country             | string  | 国家名称 |
| title               | string  | 标题 |
| event               | string  | 事件名称 |
| country_id          | string  | 国家 id |
| quantity            | string  | 量 |
| unit                | string  | 单位 |
| importance          | string  | 重要性，1-3，重要性由低到高 |
| mark                | string  | 来源备注 |
| push_status         | boolean | 是否已发布 |
| flag_uri            | string  | 国家旗帜地址 |
| calendar_key        | string  | 事件标识 |
| actual              | int64   | 实际值 |
| forecast            | int64   | 预测值 |
| previous            | int64   | 前值 |
| revised             | int64   | 修正值 |
| period              | string  | 数据公布周期 |
| calendar_type       | string  | 日历类型，FD=经济指标，FE=财经大事，FH=假期日历 |
| subscribe_status    | boolean | 订阅状态 |

#### Example

**请求示例**

`GET /finance/macrodatas?start=1527177600&end=1527263999`

**返回示例**

```json
{
  "code": 20000,
  "message": "OK",
  "data": {
    "items": [
      {
        "id": 59662,
        "public_date": 1527204600,
        "observation_date": "2018-05-01",
        "wscn_ticker": "JP111741",
        "country": "日本",
        "title": "5月东京CPI(除生鲜食品及能源)同比",
        "event": "东京CPI(除生鲜食品及能源)同比",
        "country_id": "JP",
        "quantity": "",
        "unit": "%",
        "importance": 1,
        "mark": "BB",
        "push_status": true,
        "flag_uri": "https://wpimg.wallstcn.com/84/39/2c/japan-2x.png",
        "calendar_key": "ea80b2aa147760b40325487bc4af471b",
        "actual": "0.20",
        "forecast": "0.30",
        "previous": "0.30",
        "revised": "",
        "period": "月",
        "calendar_type": "FD",
        "subscribe_status": false
      },
      {
        "id": 59661,
        "public_date": 1527204600,
        "observation_date": "2018-05-01",
        "wscn_ticker": "JP111740",
        "country": "日本",
        "title": "5月东京CPI(除生鲜食品)同比",
        "event": "东京CPI(除生鲜食品)同比",
        "country_id": "JP",
        "quantity": "",
        "unit": "%",
        "importance": 3,
        "mark": "BB",
        "push_status": true,
        "flag_uri": "https://wpimg.wallstcn.com/84/39/2c/japan-2x.png",
        "calendar_key": "61815d0fe0810695fb64f93ea31332c4",
        "actual": "0.50",
        "forecast": "0.60",
        "previous": "0.60",
        "revised": "",
        "period": "月",
        "calendar_type": "FD",
        "subscribe_status": false
      },
      {
        "id": 59660,
        "public_date": 1527204600,
        "observation_date": "2018-05-01",
        "wscn_ticker": "JP111739",
        "country": "日本",
        "title": "5月东京CPI同比",
        "event": "东京CPI同比",
        "country_id": "JP",
        "quantity": "",
        "unit": "%",
        "importance": 2,
        "mark": "BB",
        "push_status": true,
        "flag_uri": "https://wpimg.wallstcn.com/84/39/2c/japan-2x.png",
        "calendar_key": "666f952303b8965ccfff6a27ddad5114",
        "actual": "0.40",
        "forecast": "0.50",
        "previous": "0.50",
        "revised": "",
        "period": "月",
        "calendar_type": "FD",
        "subscribe_status": false
      }
    ]
  }
}
```
### 3.2 经济指标搜索接口

利用该接口，可通过 `limit` 字段配合相关条件，获取特定经济指标（FD）列表。时间为可选参数，但必须保证 `start_time` 和 `end_time` 同时传参，且 `start_time` < `end_time`。

`GET /finance/indicator/search?limit={}`

#### Request Parameters

| Name        | Required |  Type  | Description |
| :---------- | :------: | :----: | :---------- |
| title       |          | string | 指标名称关键词，模糊搜索 |
| country     |          | string | 国家代码 |
| start_time  |          | int64  | 起始时间，时间戳 |
| end_time    |          | int64  | 截至时间，时间戳 |
| cursor      |          | int64  | 游标 |
| limit       |    yes   | int64  | 数量，每页限制最多 100 条 |
| importances |          | string | 重要性，1-3，以英文逗号隔开 |

#### Response

| Name                |  Type   | Description       |
| :------------------ | :-----: | :---------------- |
| id                  | int64   | id |
| public_date         | int64   | 数据发布时间，时间戳。转换后显示为北京时间 12:02 的数据为公布时间待定的事件 |
| observation_date    | string  | 数据参考时间 |
| wscn_ticker         | string  | 唯一码 |
| country             | string  | 国家名称 |
| title               | string  | 标题 |
| event               | string  | 事件名称 |
| country_id          | string  | 国家 id |
| quantity            | string  | 量 |
| unit                | string  | 单位 |
| importance          | string  | 重要性，1-3，重要性由低到高 |
| mark                | string  | 来源备注 |
| push_status         | boolean | 是否已发布 |
| flag_uri            | string  | 国家旗帜地址 |
| calendar_key        | string  | 事件标识 |
| actual              | int64   | 实际值 |
| forecast            | int64   | 预测值 |
| previous            | int64   | 前值 |
| revised             | int64   | 修正值 |
| period              | string  | 数据公布周期 |
| calendar_type       | string  | 日历类型 |
| subscribe_status    | boolean | 订阅状态 |

#### Example

**请求示例**

`GET /finance/indicator/search?title=非农就业人口变动&country=US&limit=3`

**返回示例**

```json
{
  "code": 20000,
  "message": "OK",
  "data": {
    "items": [
      {
        "id": 751,
        "public_date": 1452288600,
        "observation_date": "2015-12-01",
        "wscn_ticker": "US121058",
        "country": "美国",
        "title": "12月非农就业人口变动(万人)",
        "event": "非农就业人口变动",
        "country_id": "US",
        "quantity": "k",
        "unit": "万人",
        "importance": 2,
        "mark": "BB",
        "push_status": false,
        "flag_uri": "https://wpimg.wallstcn.com/32/75/86/usa-2x.png",
        "calendar_key": "ac62ae595cfcc3fc40fe8c5d7193d50a",
        "actual": "27.50",
        "forecast": "20.10",
        "previous": "19.70",
        "revised": "27.90",
        "period": "月",
        "calendar_type": "FD",
        "subscribe_status": false
      },
      {
        "id": 1230,
        "public_date": 1454707800,
        "observation_date": "2016-01-01",
        "wscn_ticker": "US121058",
        "country": "美国",
        "title": "1月非农就业人口变动(万人)",
        "event": "非农就业人口变动",
        "country_id": "US",
        "quantity": "k",
        "unit": "万人",
        "importance": 2,
        "mark": "BB",
        "push_status": false,
        "flag_uri": "https://wpimg.wallstcn.com/32/75/86/usa-2x.png",
        "calendar_key": "9479f89490f8d072ac1bf284d2cd022d",
        "actual": "15.80",
        "forecast": "18.00",
        "previous": "27.50",
        "revised": "25.90",
        "period": "月",
        "calendar_type": "FD",
        "subscribe_status": false
      },
      {
        "id": 1706,
        "public_date": 1457127000,
        "observation_date": "2016-02-01",
        "wscn_ticker": "US121058",
        "country": "美国",
        "title": "2月非农就业人口变动(万人)",
        "event": "非农就业人口变动",
        "country_id": "US",
        "quantity": "k",
        "unit": "万人",
        "importance": 2,
        "mark": "BB",
        "push_status": false,
        "flag_uri": "https://wpimg.wallstcn.com/32/75/86/usa-2x.png",
        "calendar_key": "78dc1bcec2b83b86cb3da09c6a2c3873",
        "actual": "23.00",
        "forecast": "19.00",
        "previous": "15.80",
        "revised": "15.50",
        "period": "月",
        "calendar_type": "FD",
        "subscribe_status": false
      }
    ],
    "next_cursor": 1,
    "total_count": 31
  }
}
```

### 3.3 获取新股上市日历列表

通过开始、结束日期的时间戳来获取新股上市日历列表，最大时间跨度为 1 日。

`GET  /finance/ipodatas?start={timestamp}&end={timestamp}`

#### Request Parameters

| Name        | Required |  Type  | Description |
| :---------- | :------: | :----: | :---------- |
| start       |   yes    | int64  | 开始日期：时间戳 |
| end         |   yes    | int64  | 结束日期：时间戳 |

#### Response

| Name                |  Type   | Description       |
| :------------------ | :-----: | :---------------- |
| id                  | int64   | id |
| code                | string  | 股票代码 |
| company_name        | string  | 公司名称 |
| company_name_en     | string  | 公司名称（英文） |
| country             | string  | 国家 |
| country_id          | string  | 国家代码 |
| flag_uri            | string  | 国旗 |
| exchange_code       | string  | 交易所代码 |
| public_date         | int64   | 上市日期 |
| price_upper         | string  | 价格区间上限 |
| price_floor         | string  | 价格区间下限 |
| listed_price        | string  | 上市定价 |
| currency            | string  | 货币代码 |
| currency_name       | string  | 货币名称 |
| shares              | string  | 拟上市股本（单位：百万） |
| market_value        | string  | 拟筹资金额（单位：百万） |
| status              | string  | 上市状态，0=未上市，1=已上市 |
| visible             | boolean | //忽略 |


#### Example

**请求示例**

`GET /finance/ipodatas?start=1527091200&end=1527177599`

**返回示例**

```json
{
  "code": 20000,
  "message": "OK",
  "data": {
    "items": [
      {
        "id": 35,
        "code": "CLPS",
        "company_name": "华钦科技",
        "company_name_en": "",
        "country": "美国",
        "country_id": "US",
        "flag_uri": "https://wpimg.wallstcn.com/32/75/86/usa-2x.png",
        "exchange_code": "",
        "public_date": 1527165000,
        "price_upper": "5.25",
        "price_floor": "5.25",
        "listed_price": "5.25",
        "currency": "USD",
        "currency_name": "美元",
        "shares": "2.0",
        "market_value": "10.5",
        "status": "1",
        "visible": false
      }
    ]
  }
}
```

### 3.4 获取会议活动日历列表

通过开始、结束日期的时间戳来获取会议活动日历列表，最大时间跨度为 1 日。

`GET  /finance/meetings?start={timestamp}&end={timestamp}`

#### Request Parameters

| Name        | Required |  Type  | Description |
| :---------- | :------: | :----: | :---------- |
| start       |   yes    | int64  | 开始日期：时间戳 |
| end         |   yes    | int64  | 结束日期：时间戳 |

#### Response

| Name                |  Type   | Description       |
| :------------------ | :-----: | :---------------- |
| id                  | int64   | id |
| code                | string  | 股票代码 |
| company_name        | string  | 公司名称 |
| country             | string  | 国家 |
| country_id          | string  | 国家代码 |
| flag_uri            | string  | 国旗 |
| exchange_code       | string  | 交易所代码 |
| meeting_date        | int64   | 会议日期 |
| meeting_type        | string  | 会议类型，如「业绩会」、「股东大会」 |
| meeting_address     | string  | 会议地址 |
| contact             | string  | 联系方式 |
| website             | string  | 官网地址 |
| visible             | boolean | //忽略 |

#### Example

**请求示例**

`GET /finance/meetings?start=1527091200&end=1527177599`

**返回示例**

```json
{
  "code": 20000,
  "message": "OK",
  "data": {
    "items": [
      {
        "id": 1447,
        "code": "BILI",
        "company_name": "哔哩哔哩",
        "country": "美国",
        "country_id": "US",
        "flag_uri": "https://wpimg.wallstcn.com/32/75/86/usa-2x.png",
        "exchange_code": "",
        "meeting_date": 1527123600,
        "meeting_type": "业绩会",
        "meeting_address": "https://edge.media-server.com/m6/p/rnryh7jq",
        "contact": "",
        "website": "",
        "visible": true
      },
      {
        "id": 1449,
        "code": "TOUR",
        "company_name": "途牛",
        "country": "美国",
        "country_id": "US",
        "flag_uri": "https://wpimg.wallstcn.com/32/75/86/usa-2x.png",
        "exchange_code": "",
        "meeting_date": 1527163200,
        "meeting_type": "业绩会",
        "meeting_address": "http://mms.prnasia.com/tour/20180524/",
        "contact": "",
        "website": "",
        "visible": true
      }
    ]
  }
}
```

### 3.5 获取财报日历列表

通过开始、结束日期的时间戳来获取财报日历列表，最大时间跨度为 1 日。

`GET  /finance/reports?start={timestamp}&end={timestamp}`

#### Request Parameters

| Name        | Required |  Type  | Description |
| :---------- | :------: | :----: | :---------- |
| start       |   yes    | int64  | 开始日期：时间戳 |
| end         |   yes    | int64  | 结束日期：时间戳 |

#### Response

| Name                |  Type   | Description       |
| :------------------ | :-----: | :---------------- |
| id                  | int64   | id |
| code                | string  | 股票代码 |
| company_name        | string  | 公司名称 |
| company_name_en     | string  | 公司名称（英文） |
| country             | string  | 国家 |
| country_id          | string  | 国家代码 |
| observation_date    | string  | 财报类型 |
| public_date         | int64   | 发布时间，时间戳 |
| currency            | string  | 货币代码 |
| currency_name       | string  | 货币名称 |
| earnings_call_time  | string  | 发布时间类型，AMC=盘后，BMO=盘前，TAS=时间确定，TNS=时间待定 |
| eps_estimate        | string  | 预期 EPS |
| reported_eps        | string  | 实际 EPS |
| surprise            | string  | //忽略 |
| exchange_code       | string  | 交易所代码 |
| flag_uri            | string  | 国旗 |
| visible             | boolean | //忽略 |

#### Example

**请求示例**

`GET /finance/reports?start=1527091200&end=1527177599`

**返回示例**

```json
{
  "code": 20000,
  "message": "OK",
  "data": {
    "items": [
      {
        "id": 873,
        "code": "BILI",
        "company_name": "哔哩哔哩",
        "company_name_en": "Bilibili Inc",
        "country": "美国",
        "country_id": "US",
        "observation_date": "2018年一季度",
        "public_date": 1527105600,
        "currency": "USD",
        "currency_name": "美元",
        "earnings_call_time": "AMC",
        "eps_estimate": "-0.09",
        "reported_eps": "-0.94",
        "surprise": "",
        "exchange_code": "",
        "flag_uri": "https://wpimg.wallstcn.com/32/75/86/usa-2x.png",
        "visible": true
      },
      {
        "id": 506,
        "code": "00992",
        "company_name": "联想集团",
        "company_name_en": "",
        "country": "香港",
        "country_id": "HK",
        "observation_date": "末期业绩/股息",
        "public_date": 1527120000,
        "currency": "HKD",
        "currency_name": "港元",
        "earnings_call_time": "TNS",
        "eps_estimate": "",
        "reported_eps": "",
        "surprise": "",
        "exchange_code": "",
        "flag_uri": "https://wpimg.wallstcn.com/05/c0/05/hongkong-2x.png",
        "visible": true
      },
      {
        "id": 990,
        "code": "TOUR",
        "company_name": "途牛",
        "company_name_en": "Tuniu Corp",
        "country": "美国",
        "country_id": "US",
        "observation_date": "2018年一季度",
        "public_date": 1527165000,
        "currency": "USD",
        "currency_name": "美元",
        "earnings_call_time": "BMO",
        "eps_estimate": "-0.03",
        "reported_eps": "-0.03",
        "surprise": "",
        "exchange_code": "",
        "flag_uri": "https://wpimg.wallstcn.com/32/75/86/usa-2x.png",
        "visible": true
      }
    ]
  }
}
```
