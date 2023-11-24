# 数据库表

> 广告域指标无ods层明细数据，Amazon Ads API直接给到report。

## ads_report_ad_advertised_product_di
### 基本信息
- 中文表名：
- 粒度：`ad_id`, `advertiserd_asin`, `advertiserd_sku`
- 聚合粒度：`ad_group_id`,`campaign_id`, `marketplace_id`
- Report type: `advertised product`
- Configuration: `sponsored products`
- reportTypeId: `spAdvertisedProduct`
- 说明：
- API：
- API文档链接：[https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/report-types/advertised-product#sponsored-products](https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/report-types/advertised-product#sponsored-products)
- git仓库链接：
- 重构前表名（2023-11之前）：`t_amazon_ads_sp_advertised_product`

### 表结构样例

| Field                                            | Sample               |
|--------------------------------------------------|----------------------|
|   date                                           |   2023-10-06         |
|   campaign_name                                  |   钻石项圈2pcs-自动  |
|   campaign_id                                    |   168175393820466    |
|   ad_group_name                                  |   钻石项圈2pcs       |
|   ad_group_id                                    |   28836703780103     |
|   ad_id                                          |   84353800887989     |
|   portfolio_id                                   |                      |
|   impressions                                    |   338                |
|   clicks                                         |   2                  |
|   cost_per_click                                 |   0.495              |
|   click_through_rate                             |   0.591715976331361  |
|   cost                                           |   0.99               |
|   spend                                          |   0.99               |
|   campaign_budget_currency_code                  |   CAD                |
|   campaign_budget_amount                         |   3.0                |
|   campaign_budget_type                           |   DAILY_BUDGET       |
|   campaign_status                                |   PAUSED             |
|   advertised_asin                                |   B09XTTN8MY         |
|   advertised_sku                                 |   CELA-20220413-3    |
|   purchases_1d                                   |   0                  |
|   purchases_7d                                   |   0                  |
|   purchases_14d                                  |   0                  |
|   purchases_30d                                  |   0                  |
|   purchases_same_sku_1d                          |   0                  |
|   purchases_same_sku_7d                          |   0                  |
|   purchases_same_sku_14d                         |   0                  |
|   purchases_same_sku_30d                         |   0                  |
|   units_sold_clicks_1d                           |   0                  |
|   units_sold_clicks_7d                           |   0                  |
|   units_sold_clicks_14d                          |   0                  |
|   units_sold_clicks_30d                          |   0                  |
|   sales_1d                                       |   0.0                |
|   sales_7d                                       |   0.0                |
|   sales_14d                                      |   0.0                |
|   sales_30d                                      |   0.0                |
|   attributed_sales_same_sku_1d                   |   0.0                |
|   attributed_sales_same_sku_7d                   |   0.0                |
|   attributed_sales_same_sku_14d                  |   0.0                |
|   attributed_sales_same_sku_30d                  |   0.0                |
|   sales_other_sku_7d                             |   0.0                |
|   units_sold_same_sku_1d                         |   0                  |
|   units_sold_same_sku_7d                         |   0                  |
|   units_sold_same_sku_14d                        |   0                  |
|   units_sold_same_sku_30d                        |   0                  |
|   units_sold_other_sku_7d                        |   0                  |
|   kindle_edition_normalized_pages_read_14d       |   0                  |
|   kindle_edition_normalized_pages_royalties_14d  |   0.0                |
|   acos_clicks_7d                                 |   0.0                |
|   acos_clicks_14d                                |   0.0                |
|   roas_clicks_7d                                 |   0.0                |
|   roas_clicks_14d                                |   0.0                |
|   marketplace_id                                 |   A2EUQ1WTGCTBG2     |

#### purchasesSameSku14d[](https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/columns#purchasessamesku14d)

**Type**: Integer

**Description**: Number of attributed conversion events occurring within 14 days of ad click where the purchased SKU was the same as the SKU advertised. Sponsored Products only. Same as puchasesPromoted.

**Report types**: [spCampaigns](https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/report-types/campaign), [spTargeting](https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/report-types/targeting), [spSearchTerm](https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/report-types/search-term), [spAdvertisedProduct](https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/report-types/advertised-product)

#### unitsSoldSameSku14d[](https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/columns#unitssoldsamesku14d)

**Type**: Integer

**Description**: Total number of units ordered within 14 days of ad click where the purchased SKU was the same as the SKU advertised.

**Report types**: [spCampaigns](https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/report-types/campaign), [spTargeting](https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/report-types/targeting), [spSearchTerm](https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/report-types/search-term), [spAdvertisedProduct](https://advertising.amazon.com/API/docs/en-us/guides/reporting/v3/report-types/advertised-product)

#### 备注
> 该report没有提供`purchasesOtherSku14d`字段（应该是缺失了），从业务逻辑出发，间接订单量用`sum(purchases_14d)-sum(purchases_same_sku_14d)`表达。
> 该report没有提供`salesOtherSku14d`字段（应该是缺失了），暂时使用`sales_other_sku_7d`代替，口径不算完全准确，需要补充`salesOtherSku14d`字段，或从跨表里拿该字段。


### 建表信息DDL

```sql
CREATE TABLE `ads_report_ad_advertised_product_di` (
    `date` date NOT NULL COMMENT '日期',
    `campaign_name` varchar(255) DEFAULT NULL COMMENT '广告活动名称',
    `campaign_id` bigint DEFAULT NULL COMMENT '广告活动 ID',
    `ad_group_name` varchar(255) DEFAULT NULL COMMENT '广告组名称',
    `ad_group_id` bigint DEFAULT NULL COMMENT '广告组 ID',
    `ad_id` bigint DEFAULT NULL COMMENT '广告 ID',
    `portfolio_id` varchar(255) DEFAULT NULL COMMENT '投资组合 ID',
    `impressions` int DEFAULT NULL COMMENT '展示次数',
    `clicks` int DEFAULT NULL COMMENT '点击次数',
    `cost_per_click` double DEFAULT NULL COMMENT '每次点击成本',
    `click_through_rate` double DEFAULT NULL COMMENT '点击率',
    `cost` double DEFAULT NULL COMMENT '成本',
    `spend` double DEFAULT NULL COMMENT '花费',
    `campaign_budget_currency_code` varchar(10) DEFAULT NULL COMMENT '广告活动预算货币代码',
    `campaign_budget_amount` double DEFAULT NULL COMMENT '广告活动预算金额',
    `campaign_budget_type` varchar(50) DEFAULT NULL COMMENT '广告活动预算类型',
    `campaign_status` varchar(50) DEFAULT NULL COMMENT '广告活动状态',
    `advertised_asin` varchar(50) NOT NULL COMMENT '广告 ASIN',
    `advertised_sku` varchar(50) DEFAULT NULL COMMENT '广告 SKU',
    `purchases_1d` int DEFAULT NULL COMMENT '1 天内购买次数',
    `purchases_7d` int DEFAULT NULL COMMENT '7 天内购买次数',
    `purchases_14d` int DEFAULT NULL COMMENT '14 天内购买次数',
    `purchases_30d` int DEFAULT NULL COMMENT '30 天内购买次数',
    `purchases_same_sku_1d` int DEFAULT NULL COMMENT '1 天内相同 SKU 购买次数',
    `purchases_same_sku_7d` int DEFAULT NULL COMMENT '7 天内相同 SKU 购买次数',
    `purchases_same_sku_14d` int DEFAULT NULL COMMENT '14 天内相同 SKU 购买次数',
    `purchases_same_sku_30d` int DEFAULT NULL COMMENT '30 天内相同 SKU 购买次数',
    `units_sold_clicks_1d` int DEFAULT NULL COMMENT '1 天内点击后售出数量',
    `units_sold_clicks_7d` int DEFAULT NULL COMMENT '7 天内点击后售出数量',
    `units_sold_clicks_14d` int DEFAULT NULL COMMENT '14 天内点击后售出数量',
    `units_sold_clicks_30d` int DEFAULT NULL COMMENT '30 天内点击后售出数量',
    `sales_1d` double DEFAULT NULL COMMENT '1 天内销售额',
    `sales_7d` double DEFAULT NULL COMMENT '7 天内销售额',
    `sales_14d` double DEFAULT NULL COMMENT '14 天内销售额',
    `sales_30d` double DEFAULT NULL COMMENT '30 天内销售额',
    `attributed_sales_same_sku_1d` double DEFAULT NULL COMMENT '1 天内相同 SKU 归因销售额',
    `attributed_sales_same_sku_7d` double DEFAULT NULL COMMENT '7 天内相同 SKU 归因销售额',
    `attributed_sales_same_sku_14d` double DEFAULT NULL COMMENT '14 天内相同 SKU 归因销售额',
    `attributed_sales_same_sku_30d` double DEFAULT NULL COMMENT '30 天内相同 SKU 归因销售额',
    `sales_other_sku_7d` double DEFAULT NULL COMMENT '7 天内其他 SKU 销售额',
    `units_sold_same_sku_1d` int DEFAULT NULL COMMENT '1 天内相同 SKU 售出数量',
    `units_sold_same_sku_7d` int DEFAULT NULL COMMENT '7 天内相同 SKU 售出数量',
    `units_sold_same_sku_14d` int DEFAULT NULL COMMENT '14 天内相同 SKU 售出数量',
    `units_sold_same_sku_30d` int DEFAULT NULL COMMENT '30 天内相同 SKU 售出数量',
    `units_sold_other_sku_7d` int DEFAULT NULL COMMENT '7 天内其他 SKU 售出数量',
    `kindle_edition_normalized_pages_read_14d` int DEFAULT NULL COMMENT '14 天内阅读的 Kindle 版归一化页数',
    `kindle_edition_normalized_pages_royalties_14d` double DEFAULT NULL COMMENT '14 天内 Kindle 版归一化页数的版税',
    `acos_clicks_7d` double DEFAULT NULL COMMENT '7 天内广告投入产出比（ACoS）',
    `acos_clicks_14d` double DEFAULT NULL COMMENT '14 天内广告投入产出比（ACoS）',
    `roas_clicks_7d` double DEFAULT NULL COMMENT '7 天内投资回报率（ROAS）',
    `roas_clicks_14d` double DEFAULT NULL COMMENT '14 天内投资回报率（ROAS）',
    `marketplace_id` varchar(50) NOT NULL COMMENT '市场id',
    PRIMARY KEY (`date`, `marketplace_id`, `advertised_asin`)
) ENGINE = InnoDB DEFAULT CHARSET = utf8 COMMENT = '广告产品报告:包含作为您的活动一部分进行广告的产品的效果数据, DAILY, groupBy advertiser'
```

### API字段说明


## ads_report_ad_campaign_adgroup_di

### 基本信息
- 中文表名：
- 粒度：`ad_group_id`
- 聚合粒度: `campaign_id`, `marketplace_id`
- Report Types: `campaign`
- Configuration: `Sponsored Products`
- reportTpyeId: `spCampaigns`
- 重构前表名（2023-11之前）：`t_amazon_ads_report_products_campaigns_adgroup_daily`

### 表结构样例

| Field                                            | Sample               |
|--------------------------------------------------|----------------------|
|   date                                           |   2023-10-18         |
|   marketplace_id                                 |   A2EUQ1WTGCTBG2     |
|   campaign_id                                    |   168175393820466    |
|   campaign_name                                  |   钻石项圈2pcs-自动  |
|   campaign_status                                |   PAUSED             |
|   campaign_bidding_strategy                      |   legacy             |
|   campaign_budget_type                           |   DAILY_BUDGET       |
|   campaign_budget_amount                         |   3.0                |
|   campaign_budget_currency_code                  |   CAD                |
|   campaign_rule_based_budget_amount              |   0.0                |
|   campaign_applicable_budget_rule_id             |   0                  |
|   campaign_applicable_budget_rule_name           |                      |
|   ad_group_id                                    |   28836703780103     |
|   ad_group_name                                  |   钻石项圈2pcs       |
|   ad_status                                      |   ENABLED            |
|   impressions                                    |   517                |
|   clicks                                         |   0                  |
|   click_through_rate                             |   0.0                |
|   cost                                           |   0.0                |
|   cost_per_click                                 |   0.0                |
|   units_sold_clicks_1d                           |   0                  |
|   units_sold_clicks_7d                           |   0                  |
|   units_sold_clicks_14d                          |   0                  |
|   units_sold_clicks_30d                          |   0                  |
|   attributed_sales_same_sku_1d                   |   0.0                |
|   attributed_sales_same_sku_7d                   |   0.0                |
|   attributed_sales_same_sku_14d                  |   0.0                |
|   attributed_sales_same_sku_30d                  |   0.0                |
|   purchases_same_sku_1d                          |   0                  |
|   purchases_same_sku_7d                          |   0                  |
|   purchases_same_sku_14d                         |   0                  |
|   purchases_same_sku_30d                         |   0                  |
|   units_sold_same_sku_1d                         |   0                  |
|   units_sold_same_sku_7d                         |   0                  |
|   units_sold_same_sku_14d                        |   0                  |
|   units_sold_same_sku_30d                        |   0                  |
|   sales_1d                                       |   0.0                |
|   sales_7d                                       |   0.0                |
|   sales_14d                                      |   0.0                |
|   sales_30d                                      |   0.0                |
|   purchases_1d                                   |   0                  |
|   purchases_7d                                   |   0                  |
|   purchases_14d                                  |   0                  |
|   purchases_30d                                  |   0                  |
|   kindle_edition_normalized_pages_read_14d       |   0                  |
|   kindle_edition_normalized_pages_royalties_14d  |   0.0                |


### 建表信息DDL
```sql
CREATE TABLE `ads_report_ad_campaign_adgroup_di` (
    `date` date NOT NULL COMMENT '日期',
    `marketplace_id` varchar(50) NOT NULL COMMENT '市场id',
    `campaign_id` bigint NOT NULL COMMENT '广告活动ID',
    `campaign_name` varchar(255) DEFAULT NULL COMMENT '广告活动名称',
    `campaign_status` varchar(255) DEFAULT NULL COMMENT '广告活动状态',
    `campaign_bidding_strategy` varchar(255) DEFAULT NULL COMMENT '广告活动出价策略',
    `campaign_budget_type` varchar(255) DEFAULT NULL COMMENT '广告活动预算类型',
    `campaign_budget_amount` float DEFAULT NULL COMMENT '广告活动预算金额',
    `campaign_budget_currency_code` varchar(255) DEFAULT NULL COMMENT '广告活动预算货币代码',
    `campaign_rule_based_budget_amount` float DEFAULT NULL COMMENT '基于规则的广告活动预算金额',
    `campaign_applicable_budget_rule_id` bigint DEFAULT NULL COMMENT '适用的广告活动预算规则ID',
    `campaign_applicable_budget_rule_name` varchar(255) DEFAULT NULL COMMENT '适用的广告活动预算规则名称',
    `ad_group_id` bigint NOT NULL COMMENT '广告组ID',
    `ad_group_name` varchar(255) DEFAULT NULL COMMENT '广告组名称',
    `ad_status` varchar(255) DEFAULT NULL COMMENT '广告状态',
    `impressions` int DEFAULT NULL COMMENT '展示次数',
    `clicks` int DEFAULT NULL COMMENT '点击次数',
    `click_through_rate` float DEFAULT NULL COMMENT '点击率',
    `cost` float DEFAULT NULL COMMENT '成本',
    `cost_per_click` float DEFAULT NULL COMMENT '每次点击成本',
    `units_sold_clicks_1d` int DEFAULT NULL COMMENT '1天内点击单位销售额',
    `units_sold_clicks_7d` int DEFAULT NULL COMMENT '7天内点击单位销售额',
    `units_sold_clicks_14d` int DEFAULT NULL COMMENT '14天内点击单位销售额',
    `units_sold_clicks_30d` int DEFAULT NULL COMMENT '30天内点击单位销售额',
    `attributed_sales_same_sku_1d` float DEFAULT NULL COMMENT '1天内相同SKU的归因销售额',
    `attributed_sales_same_sku_7d` float DEFAULT NULL COMMENT '7天内相同SKU的归因销售额',
    `attributed_sales_same_sku_14d` float DEFAULT NULL COMMENT '14天内相同SKU的归因销售额',
    `attributed_sales_same_sku_30d` float DEFAULT NULL COMMENT '30天内相同SKU的归因销售额',
    `purchases_same_sku_1d` int DEFAULT NULL COMMENT '1天内相同SKU的购买次数',
    `purchases_same_sku_7d` int DEFAULT NULL COMMENT '7天内相同SKU的购买次数',
    `purchases_same_sku_14d` int DEFAULT NULL COMMENT '14天内相同SKU的购买次数',
    `purchases_same_sku_30d` int DEFAULT NULL COMMENT '30天内相同SKU的购买次数',
    `units_sold_same_sku_1d` int DEFAULT NULL COMMENT '1天内相同SKU的单位销售额',
    `units_sold_same_sku_7d` int DEFAULT NULL COMMENT '7天内相同SKU的单位销售额',
    `units_sold_same_sku_14d` int DEFAULT NULL COMMENT '14天内相同SKU的单位销售额',
    `units_sold_same_sku_30d` int DEFAULT NULL COMMENT '30天内相同SKU的单位销售额',
    `sales_1d` float DEFAULT NULL COMMENT '1天内销售额',
    `sales_7d` float DEFAULT NULL COMMENT '7天内销售额',
    `sales_14d` float DEFAULT NULL COMMENT '14天内销售额',
    `sales_30d` float DEFAULT NULL COMMENT '30天内销售额',
    `purchases_1d` int DEFAULT NULL COMMENT '1天内购买次数',
    `purchases_7d` int DEFAULT NULL COMMENT '7天内购买次数',
    `purchases_14d` int DEFAULT NULL COMMENT '14天内购买次数',
    `purchases_30d` int DEFAULT NULL COMMENT '30天内购买次数',
    `kindle_edition_normalized_pages_read_14d` int DEFAULT NULL COMMENT '14天内Kindle版规格化页面阅读次数',
    `kindle_edition_normalized_pages_royalties_14d` float DEFAULT NULL COMMENT '14天内Kindle版规格化页面版税',
    PRIMARY KEY (
        `date`,
        `marketplace_id`,
        `campaign_id`,
        `ad_group_id`
    )
) ENGINE = InnoDB DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_0900_ai_ci COMMENT = '广告活动报告：按广告活动为主体，天粒度统计活动效果数据'
```


