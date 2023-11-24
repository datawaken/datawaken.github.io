
# 数据库表

## ads_report_sp_sales_and_traffic_data_di


### 基本信息
- 重构前表名（2023-11之前）：t_amazon_ods_report_sales_and_traffic_data
- API文档链接：[https://developer-docs.amazon.com/sp-api/docs/seller-retail-reports-attributes](https://developer-docs.amazon.com/sp-api/docs/seller-retail-reports-attributes)
- 

### 表结构样例

|   Field                                    |   Sample          |
|--------------------------------------------|-------------------|
|   date                                     |   2023-10-06      |
|   parent_asin                              |   B0B1CKPWT2      |
|   child_asin                               |   B09XTR21P7      |
|   sku                                      |                   |
|   units_ordered                            |   0               |
|   units_ordered_b2b                        |   0               |
|   ordered_product_sales_amount             |   0.00            |
|   ordered_product_sales_currency_code      |   CAD             |
|   ordered_product_sales_b2b_amount         |   0.00            |
|   ordered_product_sales_b2b_currency_code  |   CAD             |
|   total_order_items                        |   0               |
|   total_order_items_b2b                    |   0               |
|   browser_sessions                         |   1               |
|   browser_sessions_b2b                     |   1               |
|   mobile_app_sessions                      |   0               |
|   mobile_app_sessions_b2b                  |   0               |
|   sessions                                 |   1               |
|   sessions_b2b                             |   1               |
|   browser_session_percentage               |   25.00           |
|   browser_session_percentage_b2b           |   100.00          |
|   mobile_app_session_percentage            |   0.00            |
|   mobile_app_session_percentage_b2b        |   0.00            |
|   session_percentage                       |   5.88            |
|   session_percentage_b2b                   |   100.00          |
|   browser_page_views                       |   2               |
|   browser_page_views_b2b                   |   1               |
|   mobile_page_views                        |   0               |
|   mobile_page_views_b2b                    |   0               |
|   page_views                               |   2               |
|   page_views_b2b                           |   1               |
|   browser_page_views_percentage            |   33.33           |
|   browser_page_views_percentage_b2b        |   100.00          |
|   mobile_page_views_percentage             |   0.00            |
|   mobile_page_views_percentage_b2b         |   0.00            |
|   page_views_percentage                    |   10.00           |
|   page_views_percentage_b2b                |   100.00          |
|   buy_box_percentage                       |   100.00          |
|   buy_box_percentage_b2b                   |   0.00            |
|   unit_session_percentage                  |   0.00            |
|   unit_session_percentage_b2b              |   0.00            |
|   marketplace_id                           |   A2EUQ1WTGCTBG2  |


### 建表信息DDL

```sql
CREATE TABLE `ads_report_sp_sales_and_traffic_data_di` (
    `date` date NOT NULL COMMENT '日期',
    `parent_asin` varchar(255) DEFAULT NULL COMMENT '父 ASIN',
    `child_asin` varchar(255) NOT NULL COMMENT '子 ASIN',
    `sku` varchar(255) DEFAULT NULL COMMENT 'SKU',
    `units_ordered` int DEFAULT NULL COMMENT '订购数量',
    `units_ordered_b2b` int DEFAULT NULL COMMENT 'B2B 订购数量',
    `ordered_product_sales_amount` decimal(10, 2) DEFAULT NULL COMMENT '订购产品销售额',
    `ordered_product_sales_currency_code` varchar(10) DEFAULT NULL COMMENT '订购产品销售货币代码',
    `ordered_product_sales_b2b_amount` decimal(10, 2) DEFAULT NULL COMMENT 'B2B 订购产品销售额',
    `ordered_product_sales_b2b_currency_code` varchar(10) DEFAULT NULL COMMENT 'B2B 订购产品销售货币代码',
    `total_order_items` int DEFAULT NULL COMMENT '总订单项',
    `total_order_items_b2b` int DEFAULT NULL COMMENT 'B2B 总订单项',
    `browser_sessions` int DEFAULT NULL COMMENT '浏览器会话',
    `browser_sessions_b2b` int DEFAULT NULL COMMENT 'B2B 浏览器会话',
    `mobile_app_sessions` int DEFAULT NULL COMMENT '移动应用会话',
    `mobile_app_sessions_b2b` int DEFAULT NULL COMMENT 'B2B 移动应用会话',
    `sessions` int DEFAULT NULL COMMENT '会话',
    `sessions_b2b` int DEFAULT NULL COMMENT 'B2B 会话',
    `browser_session_percentage` decimal(10, 2) DEFAULT NULL COMMENT '浏览器会话百分比',
    `browser_session_percentage_b2b` decimal(10, 2) DEFAULT NULL COMMENT 'B2B 浏览器会话百分比',
    `mobile_app_session_percentage` decimal(10, 2) DEFAULT NULL COMMENT '移动应用会话百分比',
    `mobile_app_session_percentage_b2b` decimal(10, 2) DEFAULT NULL COMMENT 'B2B 移动应用会话百分比',
    `session_percentage` decimal(10, 2) DEFAULT NULL COMMENT '会话百分比',
    `session_percentage_b2b` decimal(10, 2) DEFAULT NULL COMMENT 'B2B 会话百分比',
    `browser_page_views` int DEFAULT NULL COMMENT '浏览器页面浏览量',
    `browser_page_views_b2b` int DEFAULT NULL COMMENT 'B2B 浏览器页面浏览量',
    `mobile_page_views` int DEFAULT NULL COMMENT '移动页面浏览量',
    `mobile_page_views_b2b` int DEFAULT NULL COMMENT 'B2B 移动页面浏览量',
    `page_views` int DEFAULT NULL COMMENT '页面浏览量',
    `page_views_b2b` int DEFAULT NULL COMMENT 'B2B 页面浏览量',
    `browser_page_views_percentage` decimal(10, 2) DEFAULT NULL COMMENT '浏览器页面浏览量百分比',
    `browser_page_views_percentage_b2b` decimal(10, 2) DEFAULT NULL COMMENT 'B2B 浏览器页面浏览量百分比',
    `mobile_page_views_percentage` decimal(10, 2) DEFAULT NULL COMMENT '移动页面浏览量百分比',
    `mobile_page_views_percentage_b2b` decimal(10, 2) DEFAULT NULL COMMENT 'B2B 移动页面浏览量百分比',
    `page_views_percentage` decimal(10, 2) DEFAULT NULL COMMENT '页面浏览量百分比',
    `page_views_percentage_b2b` decimal(10, 2) DEFAULT NULL COMMENT 'B2B 页面浏览量百分比',
    `buy_box_percentage` decimal(10, 2) DEFAULT NULL COMMENT '购物车百分比',
    `buy_box_percentage_b2b` decimal(10, 2) DEFAULT NULL COMMENT 'B2B 购物车百分比',
    `unit_session_percentage` decimal(10, 2) DEFAULT NULL COMMENT '单位会话百分比',
    `unit_session_percentage_b2b` decimal(10, 2) DEFAULT NULL COMMENT 'B2B 单位会话百分比',
    `marketplace_id` varchar(50) NOT NULL COMMENT '市场id',
    PRIMARY KEY (`date`, `marketplace_id`, `child_asin`)
) ENGINE = InnoDB DEFAULT CHARSET = utf8 COMMENT = 'SP卖家零售分析报告：GET_SALES_AND_TRAFFIC_REPORT，包含销售指标和流量指标'
```


