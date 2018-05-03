# 财经日历 6.1 需求文档

## 文档控制

### 修改历史

| 修改人 | 修改日期 | 修改描述 |
| :-- | :-- | :-- |
| MOUSE | 2018-04-20 | 初稿 |

### 审核记录

| 审核人 | 审核日期 | 角色 | 说明 |
| :-- | :-- | :-- | :-- |
| | | |

## 1. 需求概述

### 1.1 目标

* 完成经济指标、财经大事、企业财报、IPO上市、会议活动、假期日历的分类接入、展示

### 1.2 功能清单

| 优先级 | 模块 | 功能描述 |
| :-- | :-- | :-- |
| P0 | 后端表单重构 | 当前财经日历项目后端表单重构，满足分类及后续扩展需求 |
| P0 | juicy后台录入 | 所有日历后台的增删改、导入 |
| P0 | 接口的重构 | 财经日历相关接口的重构 |
| P0 | 客户端修改 | 财经日历页面在客户端的修改（前端展示、接口调整）|
| P0 | 企业财报 | 数据接入：A股、港股接口，美股爬虫 |
| P0 | IPO上市 | 数据接入：A股、港股接口，美股爬虫 |
| P0 | 会议活动 | 数据接入：A股、港股、美股，手动导入 |
| P1 | 假期日历 | 数据接入：手动导入 |

### 1.3 项目计划

| 项目阶段 | 预期时间 | 备注 |
| :-- | :-- | :-- |
| 开发 | | |
| 测试 | | |
| 上线 | | |

## 2. 流程

### 2.1
### 2.2

## 3. 功能设计

### 3.1 Backend

#### 3.1.1 企业财报

港股：从恒生聚源 `HK_SpecialNotice` 表获得数据

| 字段 | 释义 | 对应表字段 |
| :-- | :-- | :-- |
| id | | |
| code | 证券代码 | SecuCode |
| company_name | 证券简称 | SecuAbbr |
| exchange_code | 交易所代码 | 暂时为空 |
| country_id | 国家代码 | HK |
| observation_date | 财报类型，需要处理 | Content，截取第一个逗号前的内容 |
| public_date | 发布日期，需转换成时间戳 | NoticeStartDate |
| currency | 货币单位 | 暂时为空 |
| earnings_call_time | 财报时间类型 BMO：盘前、AMC：盘后、TNS：待定、TAS：已定，默认 TNS |  |
| eps_estimate | 预期 EPS，如有值需手填 |  |
| reported_eps | 实际 EPS，如有值需手填 |  |
| visible | 前端是否可见，0：不可见、1：可见，默认 0 |  |
| is_delete | 是否已删除，0：未删除、1：已删除，默认 0 |  |
| updated_at | 更新时间 |  |

美股：从 https://finance.yahoo.com/calendar/earnings 爬取落库。

| 字段 | 释义 | 对应表字段 |
| :-- | :-- | :-- |
| id | | |
| code | 证券代码 | ticker |
| company_name | 证券简称 | companyshortname |
| exchange_code | 交易所代码 | 暂时为空 |
| country_id | 国家代码 | US |
| observation_date | 财报类型，暂时需要手填 |  |
| public_date | 发布日期，需转换成时间戳 | startdatetime |
| currency | 货币单位 | USD |
| earnings_call_time | 财报时间类型 BMO：盘前、AMC：盘后、TNS：待定、TAS：已定 | startdatetimetype |
| eps_estimate | 预期 EPS | epsestimate |
| reported_eps | 实际 EPS | epsactual |
| visible | 前端是否可见，0：不可见、1：可见，默认 0 |  |
| is_delete | 是否已删除，0：未删除、1：已删除，默认 0 |  |
| updated_at | 更新时间 |  |

#### 3.1.2 IPO

港股：从恒生聚源 `HK_ShareIPO` 和 `HK_SecuMain` 表获得数据，其中「证券代码」和「公司简称」通过 InnerCode 字段联表获取，并令 `HK_ShareIPO.IssueType = 1`，查询当前日期之后的所有拟上市公司数据。

| 字段 | 释义 | 对应表字段 |
| :-- | :-- | :-- |
| id |  |  |
| code | 证券代码 | HK_SecuMain.SecuCode |
| company_name | 公司简称，通过 HK_ShareIPO.InnerCode 联表获取 | HK_SecuMain.SecuAbbr |
| exchange_code | 交易所代码 | 暂时为空 |
| country_id | 国家代码 | HK |
| public_date | 上市日期，时间戳 | HK_ShareIPO.ProposedListDate |
| price_upper | 价格区间上限 | HK_ShareIPO.IssuePriceCeiling |
| price_floor | 价格区间下限 | HK_ShareIPO.IssuePriceFloor |
| listed_price | 上市定价 | HK_ShareIPO.IssuePrice |
| currency | 货币单位 | HKD |
| shares | 上市股本(百万) | HK_ShareIPO.IssueVol |
| market_value | 拟筹资金额(百万) | HK_ShareIPO.ProceedsPlanned |
| status | 上市状态，0：预计、1：已上市，默认 0 |  |
| visible | 前端是否可见，0：不可见、1：可见，默认 0 |  |
| is_delete | 是否已删除，0：未删除、1：已删除，默认 0 |  |
| updated_at | 更新时间 |  |

美股：从 https://www.iposcoop.com/ipo-calendar/ 爬取。

| 字段 | 释义 | 对应表字段 |
| :-- | :-- | :-- |
| id |  |  |
| code | 证券代码 | Symbol proposed |
| company_name | 公司简称，暂时手动录入处理 |  |
| company_name_en | 公司名称 | Company |
| exchange_code | 交易所代码 | 暂时为空 |
| country_id | 国家代码 | US |
| public_date | 上市日期，时间戳 | Expected to Trade，暂时截取日期，定位到美东时间08:30的时间戳 |
| price_upper | 价格区间上限 | Price High |
| price_floor | 价格区间下限 | Price Low |
| listed_price | 上市定价 | 如果 Price High = Price Low，则写入定价字段 |
| currency | 货币单位 | 美元 |
| shares | 上市股本(百万) | Est. $ Volume ，需截取纯数字部分|
| market_value | 拟筹资金额(百万) | Shares(Millions) |
| status | 上市状态，0：预计、1：已上市，默认 0 |  |
| visible | 前端是否可见，0：不可见、1：可见，默认 0 |  |
| is_delete | 是否已删除，0：未删除、1：已删除，默认 0 |  |
| updated_at | 更新时间 |  |

A股：

#### 3.1.3 会议活动

港股：从恒生聚源 `HK_SpecialNotice` 表获得数据

| 字段 | 释义 | 对应表字段 |
| :-- | :-- | :-- |
| id |  |  |
| code | 证券代码 | SecuCode |
| company_name | 公司简称 | SecuAbbr |
| exchange_code | 交易所代码 | 暂时为空 |
| country_id | 国家代码 | HK |
| meeting_date | 会议日期，时间戳 | NoticeStartDate |
| meeting_type | 会议类型，业绩会、股东大会、特别股东大会 | NoticeType = 200,21010,22010 |
| meeting_address | 手动录入 | 从经济通网站或 88Meeting |
| contact | 手动录入 | 联系方式，暂时为空 |
| website | 手动录入 | 公司网站，暂时为空 |
| visible | 前端是否可见，0：不可见、1：可见，默认 0 |  |
| is_delete | 是否已删除，0：未删除、1：已删除，默认 0 |  |
| updated_at | 更新时间 |  |

美股：后台手动录入

A股：

#### 3.1.4 宏观日历

* 后端将经济指标、财经大事、假期日历三个类型分表处理
* 前端继续保持合并状态显示，切换到新的接口

### 3.2 Juicy

* 调整财经日历分类，进行细分
* 新增各相关项的增删改功能
* 新增按条件搜索功能

### 3.3 Web

* 「日历」页面里改为四个 TAB 的分类日历，含删选功能
* 样式修改

### 3.4 App

* 「快讯」页面顶部做成双层导航，将「快讯」和「日历」分开
* 去掉日历里原有的「2018年04月」的小字
* 样式修改
* 去掉原来财经日历的指标详情页面
