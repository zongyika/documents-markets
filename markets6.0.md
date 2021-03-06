# 行情频道改版需求

## 文档控制

### 修改历史

| 修改人 | 修改日期 | 修改描述 |
| :-: | :-: | :-- |
| MOUSE | 2018.03.07 | 初稿 |
| MOUSE | 2018.04.27 | 增加各页面接口 |

### 审核记录

| 审核人 | 审核日期 | 角色 | 说明 |
| :-: | :-: | :-: | :-: |
| | | |

## 1. 需求概述

### 1.1 目标

1. 重构行情频道 PC 页面
2. 港股行情接入
3. 数字货币行情优化
4. 行情相关资讯匹配主题化资讯列表

### 1.2 功能清单

| 优先级 | 模块 | 功能描述 |
| :-: | :-- | :-- |
| P0 | 页面重构 - 首页 |  |
| P0 | 页面重构 - 列表页 | |
| P0 | 页面重构 - 品种详情页 | |
| P0 | 页面重构 - 自选页 | |
| P1 | 港股行情 | |
| P1 | 非 A 股相关资讯 | 按主题标签选取对应资讯列表内容接入 |
| P1 | A 股相关资讯 | 选股宝对应的「个股动态」内容、公告、研报接入 |
| P2 | 数字货币行情 | 从小葱 APP 接入的行情中挑选部分替换当前接口数据 |
| P2 | 港股相关资讯 | 资讯、公告、研报（摘要） |


### 1.3 项目计划

| 项目阶段 | 预期时间 | 备注 |
| :-: | :-: | :-: |
| 开发 | | |
| 测试 | | |
| 上线 | | |

## 2. 流程

### 2.1
### 2.2

## 3. 功能设计

### 3.1 页面重构 - 首页

1. 首页行情分类和所含品种

| 分类 | 品种 | 字段 |
| :-- | :-- | :-- |
| 主要资产 | 上证指数，标普500指数，欧元/美元，黄金，布伦特原油，离岸人民币，比特币/美元 | 最新价，涨跌，涨跌幅 |
| 外汇 | 美元指数，欧元/美元，英镑/美元，澳元/美元，美元/日元，美元/加元，美元/瑞郎，离岸人民币，在岸人民币 | 最新价，涨跌，涨跌幅 |
| 商品 | 黄金，白银，布伦特原油，WTI 原油，纽约铜，天然气，玉米，小麦 | 最新价，涨跌，涨跌幅 |
| 股指 | 上证指数，深圳成指，创业板指，恒生指数，标普500指数，道琼斯指数，纳斯达克指数，英国富士100指数，欧洲 Stoxx50指数 | 最新价，涨跌，涨跌幅 |
| 数字货币 | 比特币/美元，以太币/美元，瑞波币/美元，比特币现金/美元，莱特币/美元 | 最新价，涨跌，涨跌幅 |
| 债券 | 中国10年期国债，美国10年期国债，日本10年期国债，英国10年期国债，德国10年期国债 | 收益率，涨跌，涨跌幅 |
| 选股宝主题库涨幅榜 | 最新涨幅居前的 6 个主题板块 | 板块涨跌幅，领涨股，领涨股的涨跌幅 |
| 选股宝主题库跌幅榜 | 最新跌幅居前的 6 个主题板块 | 板块涨跌幅，领跌股，领跌股的涨跌幅 |
| 港股热门榜 |  | 最新价，涨跌，涨跌幅 |

2. 接口：

* 主要资产：https://forexdata.wallstreetcn.com/real?en_prod_code=000001.SS,SPX500INDEX,EURUSD,XAUUSD,UKOIL,USDCNH,BTCUSD&fields=prod_name,last_px,px_change,px_change_rate

* 外汇：https://forexdata.wallstreetcn.com/real?en_prod_code=USDOLLARINDEX,EURUSD,GBPUSD,AUDUSD,USDJPY,USDCAD,USDCHF,USDCNH,USDCNY&fields=prod_name,last_px,px_change,px_change_rate

* 商品：https://forexdata.wallstreetcn.com/real?en_prod_code=XAUUSD,XAGUSD,UKOIL,USDOIL,COPPER,NGAS,CORN,WHEAT&fields=prod_name,last_px,px_change,px_change_rate

* 股指：https://forexdata.wallstreetcn.com/real?en_prod_code=000001.SS,399001.SZ,399006.SZ,HSI,SPX500INDEX,US30INDEX,NASINDEX,UK100INDEX,EUSTX50INDEX&fields=prod_name,last_px,px_change,px_change_rate

* 数字货币：https://forexdata.wallstreetcn.com/real?en_prod_code=BTCUSD,ETHUSD,XRPUSD,BCCUSD,LTCUSD&fields=prod_name,last_px,px_change,px_change_rate

* 债券：https://forexdata.wallstreetcn.com/real?en_prod_code=CHINA10YEAR,US10YEAR,JAPAN10YEAR,UK10YEAR,GERMANY10YEAR&fields=prod_name,last_px,px_change,px_change_rate

* 选股宝主题库涨幅榜：https://wows-api.wallstreetcn.com/v3/aioria/plates/pool?count=6&is_asc=false&rank_type=core_pcp_rank

* 选股宝主题库跌幅榜：https://wows-api.wallstreetcn.com/v3/aioria/plates/pool?count=6&is_asc=true&rank_type=core_pcp_rank

3. 右侧部件

* 我的自选
* 实时资讯
* 资产相关性（数据频道，暂时不做）
* 财经日历
* 央行利率

### 3.2 页面重构 - 列表页

1. 列表页行情分类、子分类、右侧部件

| 分类 | 子分类 | 右侧部件 |
| :-- | :-- | :-- |
| 主要 | 全部，外汇，商品，股指，债券，数字货币 | 实时资讯、资产相关性、财经日历 |
| 外汇 | 全部，美洲，欧非中东，亚洲 | 实时资讯、资产相关性、财经日历 |
| 商品 | 全部，贵金属，能源，基本金属，农产品 | 实时资讯、资产相关性、财经日历 |
| 股指 | 全部，美洲，欧非中东，亚洲，股指期货 | 实时资讯、资产相关性、财经日历 |
| 债券 | 全部，美洲，欧非中东，亚洲 | 实时资讯、资产相关性、财经日历 |
| 沪深 * | 全部，沪市，深市主板，创业板 | 实时资讯 - A股配置、智能盯盘 |
| 港股 * | 全部，主板，创业板，AH股 |  实时资讯 - A股配置、智能盯盘 |
| 数字货币 | 法币，币币 | 实时资讯、资产相关性、财经日历 |

备注：* 用配置的方式不可行

2. 列表字段

* 资产（名称、代码）
* 最新价（价格、更新时间）
* 涨跌
* 涨跌幅
* 日内区间（最低、最高）
* 52 周区间（最低、最高）
* 自选按钮（加自选、删自选）

3. 列表页排序

* 按资产代码排序（默认）
* 按涨跌幅排序

4. 接口

* 外汇：https://forexdata.wallstreetcn.com/real_list?fields=prod_name,last_px,update_time,px_change,px_change_rate,low_px,high_px,week_52_low,week_52_high,price_precision&type=forex&page=1&limit=15

### 3.3 页面重构 - 品种详情页

#### 通用设置

* 蜡烛图红涨绿跌（默认），可切换
* 一字板涨停用红色（默认）
* 一字板跌停用绿色（默认）
* 十字光标定位，日图以上周期横轴显示格式为：`MM/DD`，日图以下周期横轴显示格式为：`MM/DD hh:mm`

#### 除 A 股、港股外的品种

* 图表周期及 K 线收盘价取用规则：

| 图表周期 | K 线收盘价取用规则 |
| :-- | :-- |
| 1D | 5 分钟线的收盘价，290 个 |
| 5D | 30 分钟线的收盘价，240 个 |
| 1M | 1 小时线的收盘价，500 个 |
| 3M | 4 小时线的收盘价，400 个 |
| 6M | 4 小时线的收盘价，800 个 |
| 1Y | 日线的收盘价，250 个 |
| 5Y | 周线的收盘价，260 个 |

* 概览字段：昨收、今开、最高、最低、52周最高、52周最低
* 资讯：取用该资产品种所落主题标签的资讯列表，标题、发布时间、作者
* 右侧部件：我的自选、财经日历、资产相关性

* 交易状态：

  * 在设定的交易时间内 「交易中」
  * 在设定的交易时间外 「休市」

#### A 股品种

* 图表当前版本不动
* 增加所属选股宝主题板块，点击后新窗口打开选股宝主题库页面
* 资讯、公告、研报取用选股宝的内容，套用见闻资讯模板
* 右侧部件：我的自选、实时资讯 - A 股、智能盯盘

* 交易状态：

  * 09:15 - 09:30 「集合竞价」
  * 09:30 - 11:30 「交易中」
  * 11:30 - 13:00 「休盘」
  * 13:00 - 15:00 「交易中」
  * 其他时间 「已收盘」
  * 停牌个股 「停牌」

#### 港股品种

* 图表同 A 股
* 增加所属主题板块，点击后新窗口打开该主题页面
* 资讯取用所属主题资讯列表
* 公告、研报通过聚源数据库

* 交易状态：

  * 09:30 - 12:00 「交易中」
  * 12:00 - 13:00 「休盘」
  * 13:00 - 16:00 「交易中」
  * 其他时间 「已收盘」
  * 停牌个股 「停牌」

### 3.4 页面重构 - 自选页

#### 字段

* 资产（品种名称、代码）
* 最新价（价格、更新时间）
* 涨跌
* 涨跌幅
* 日内区间（最低、最高）
* 52 周区间（最低、最高）

#### 排序

* 默认按添加顺序排序（最新添加的置于最上方）
* 编辑模式下调整过排序的，按照编辑模式的排序
* 可按品种名称、涨跌幅排序（正序、逆序）
* 页面刷新后恢复默认或保存过的排序

#### 搜索框

* 可输入资产名称或代码，选择添加自选

#### 编辑

点击「编辑」按钮，同页面进入自选编辑状态

* 搜索框可输入资产名称或代码，选择添加自选
* 拖动资产名称前的排序图标可以对自选列表进行排序
* 点击最右的「×」可删除自选
* 点击「完成」按钮返回自选页
