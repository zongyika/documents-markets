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
| importances |          | int64  | 重要性，1-3，以英文逗号隔开 |

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
| importance          | int64   | 重要性，1-3，重要性由低到高 |
| mark                | string  | 来源备注 |
| push_status         | boolean | 是否已发布 |
| flag_uri            | string  | 国家旗帜地址 |
| calendar_key        | string  | 事件标识 |
| actual              | string  | 实际值 |
| forecast            | string  | 预测值 |
| previous            | string  | 前值 |
| revised             | string  | 修正值 |
| period              | string  | 数据公布周期 |
| calendar_type       | string  | 日历类型，FD=经济指标，FE=财经大事，FH=假期日历 |
| subscribe_status    | boolean | 订阅状态 |

#### Example

**请求示例**

`GET api-prod.wallstreetcn.com/apiv1/finance/macrodatas?start=1527177600&end=1527263999`

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
| importances |          | int64  | 重要性，1-3，以英文逗号隔开 |

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
| importance          | int64   | 重要性，1-3，重要性由低到高 |
| mark                | string  | 来源备注 |
| push_status         | boolean | 是否已发布 |
| flag_uri            | string  | 国家旗帜地址 |
| calendar_key        | string  | 事件标识 |
| actual              | string  | 实际值 |
| forecast            | string  | 预测值 |
| previous            | string  | 前值 |
| revised             | string  | 修正值 |
| period              | string  | 数据公布周期 |
| calendar_type       | string  | 日历类型 |
| subscribe_status    | boolean | 订阅状态 |

#### Example

**请求示例**

`GET api-prod.wallstreetcn.com/apiv1/finance/indicator/search?title=非农就业人口变动&country=US&limit=3`

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

### 3.3 获取财经日历指标详情

利用该接口，可通过 `wscn_ticker` 和 `ticker_type` 两个字段获取财经指标的一些相关信息。

`GET /finance/indicator/detail?wscn_ticker={}&ticker_type={}`

#### Request Parameters

| Name        | Required |  Type  | Description |
| :---------- | :------: | :----: | :---------- |
| wscn_ticker |   yes    | string | 唯一码 |
| ticker_type |   yes    | string | 指标类型，传 `finfo` |

#### Response

| Name                |  Type   | Description       |
| :------------------ | :-----: | :---------------- |
| country             | string  | 国家名称 |
| event               | string  | 事件名称 |
| unit                | string  | 单位 |
| quantity            | string  | 量 |
| period              | string  | 数据公布周期 |
| organization_name   | string  | 发布指标的机构名称 |
| paraphrase          | string  | 指标释义 |
| focus_reason        | string  | 关注原因 |
|  observation_date   | int64   | 数据参考时间 |
|  actual             | string  | 实际值 |
|  forecast           | string  | 预测值 |

#### Example

**请求示例**

`GET api-prod.wallstreetcn.com/apiv1/finance/indicator/detail?wscn_ticker=US121058&ticker_type=finfo`

**返回示例**

```json
{
  "code": 20000,
  "message": "OK",
  "data": {
    "country": "美国",
    "event": "非农就业人口变动",
    "unit": "万人",
    "quantity": "k",
    "period": "月",
    "organization_name": "",
    "paraphrase": "美国每月就业报告中的一项主要指标，记录跟踪了从事农业生产之外的企业和政府的兼职和全职雇员的数量变动情况。",
    "focus_reason": "非农就业人数变化反映出制造行业和服务行业的发展及其增长，数字减少便代表企业减低生产，经济步入萧条；在没有发生恶性通胀的情况下，如数字大幅增加，显示一个健康的经济状况，对美元应当有利，并可能预示着更将提高利率，也对美元有利。非农就业指数若增加，反映出经济发展的上升，反之则下降。",
    "data": {
      "observation_date": 1527811200,
      "actual": "21.3",
      "forecast": "19.5"
    }
  }
}
```

### 3.4 获取财经日历指标历史数据

利用该接口，可通过 `wscn_ticker` 获取对应经济指标过去 12 条历史数据的实际值和预期值，不含修正值。

`GET /finance/indicator/history/data?wscn_ticker={}`

#### Request Parameters

| Name        | Required |  Type  | Description |
| :---------- | :------: | :----: | :---------- |
| wscn_ticker |  yes     | string | 唯一码 |

#### Response

| Name                |  Type   | Description       |
| :------------------ | :-----: | :---------------- |
| observation_date    | int64   | 数据参考时间 |
| actual              | string  | 实际值 |
| forecast            | string  | 预测值 |

#### Example

**请求示例**

`GET api-prod.wallstreetcn.com/apiv1/finance/indicator/history/data?wscn_ticker=US121058`

**返回示例**

```json
{
  "code": 20000,
  "message": "OK",
  "data": {
    "items": [
      {
        "observation_date": 1498867200,
        "actual": "20.9",
        "forecast": "18"
      },
      {
        "observation_date": 1501545600,
        "actual": "15.6",
        "forecast": "18"
      },
      {
        "observation_date": 1504224000,
        "actual": "-3.3",
        "forecast": "8"
      },
      {
        "observation_date": 1506816000,
        "actual": "26.1",
        "forecast": "31.3"
      },
      {
        "observation_date": 1509494400,
        "actual": "22.8",
        "forecast": "19.5"
      },
      {
        "observation_date": 1512086400,
        "actual": "14.8",
        "forecast": "19"
      },
      {
        "observation_date": 1514764800,
        "actual": "20",
        "forecast": "18"
      },
      {
        "observation_date": 1517443200,
        "actual": "31.3",
        "forecast": "20.5"
      },
      {
        "observation_date": 1519862400,
        "actual": "10.3",
        "forecast": "18.5"
      },
      {
        "observation_date": 1522540800,
        "actual": "16.4",
        "forecast": "19.2"
      },
      {
        "observation_date": 1525132800,
        "actual": "22.3",
        "forecast": "19"
      },
      {
        "observation_date": 1527811200,
        "actual": "21.3",
        "forecast": "19.5"
      }
    ]
  }
}
```
