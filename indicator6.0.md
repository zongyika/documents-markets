# 数据频道改版需求

## 文档控制

### 修改历史

| 修改人 | 修改日期 | 修改描述 |
| :-- | :-- | :-- |
| MOUSE | 2018-03-14 | 初稿 |

### 审核记录

| 审核人 | 审核日期 | 角色 | 说明 |
| :-: | :-: | :-: | :-: |
| | | |

## 1. 需求概述

### 1.1 目标

1. 页面布局和样式调整，与 PC6.0 新版保持整体协调
2. 增加资产相关性模块
3. 优化数据频道图形化的展现形式

### 1.2 功能清单

| 优先级 | 模块 | 功能描述 |
| :-- | :-- | :-- |
| P0 | 页面重构 | 数据频道首页、国家列表页、数据详情页的布局、样式调整 |
| P0 | 资产相关性 | 根据各资产品种相关性计算规则，建立跨资产相关性的数据计算、储存、图形化展示 |
| P1 | 图形化模块 | 多指标的组合型图表展示 |

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

### 3.1 页面重构

#### 3.1.1 首页

1. 第一屏呈现四篇数据频道文章，第一篇带摘要
2. 全球资产相关性图（1个月）：折线图，5年跨度
3. 跨区域 vs 跨资产相关性图（1个月）：双折线图，5年跨度
4. 标普500 vs 10年期美债收益率相关性图（1个月）：双折线图，5年跨度
5. 跨资产相关性热力图：19 个品种，-1至1 分成 10 档颜色，右侧边栏为使用释义（具体规则见3.2）
6. 保留原来的全球经济概览，剔除导航，表格各项均可点击，点击国家至「国家列表页」，点击数值到「数据详情页」

#### 3.1.2 国家列表页

1. 第一屏左侧表格指标列同首页全球经济概览中该国的主要指标
2. 右侧三张图表为所选国家的主要股指、主要国债收益率、货币汇率
3. 下方指标图表，为配置（初期可写死）的组合式指标图表，每个国家的量大致在 10-16 个

#### 3.1.3 数据详情页

1. 图表默认柱状图，12根
2. 点 `1年`、`5年`、`10年`、`全部` ，自动切换成折线图
3. 横轴刻度按时间跨度标记，不按数据点个数标记
4. 图表类型：柱状图、折线图、面积图
5. 鼠标点击比较搜索框，弹出下拉框，默认展示 5 个该国、该分类、权重最高的指标，点击「更多」浮层展示搜索
6. 比较图默认展示双折线图，单位相同用单Y轴，单位不同用双Y轴，主数据 R，对比数据 L
7. 右侧边栏的展示逻辑与原有保持一致

### 3.2 资产相关性

1. 相关系数的计算：

  * sum((x-mean(x)) * (y-mean(y)))  //分子
  * (sum((x-mean(x))^2)^0.5) * (sum((y-mena(y))^2)^0.5)  //分母

2. 日涨跌幅 - 1 个月相关性

  * 日 K 涨幅
  * 往前推 30 日（不含当日）

3. 周涨跌幅 - 1 年相关性

  * 周 K 涨幅
  * 往前推 52 周（不含当周）

4. 相关性指数

  * 相反数：- X
  * 长期均值为 10 年的 1 个月相关性均值
  * 偏离值不取绝对值，存在正负号

5. 矩阵显示阶梯色块

  * 按照 -1 到 1 的范围，展示 10 档阶梯色块

6. 品种

| 名称 | 代码 |
| :-- | :-- |
| 标普500指数 |  |
| 沪深300指数 |  |
| 恒生指数 |  |
| 日经225指数 |  |
| 德国DAX指数 |  |
| 10年期美债收益率 |  |
| 10年期中债收益率 |  |
| 10年期日债收益率 |  |
| 10年期德债收益率 |  |
| 美元指数 |  |
| 在岸人民币 | USDCNY |
| 欧元/美元 | EURUSD |
| 美元/日元 | USDJPY |
| 英镑/美元 | GBPUSD |
| 小麦期货 |  |
| WTI原油 |  |
| 纽约期铜 |  |
| 纽约期金 |  |
| 3个月LIBOR |  |

### 3.3 图形化展示需求

 