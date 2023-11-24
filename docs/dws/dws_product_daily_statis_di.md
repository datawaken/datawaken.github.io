
# dws_product_daily_statis_di


### 建表脚本

```python
import sys
import pymysql



# 创建数据库连接
cnx = get_db_connection(db_host, db_port, db_user, db_password, db_name)
cursor = cnx.cursor() 

delete_query = f"DELETE FROM dws_product_daily_statis_di WHERE statis_day = '{startDate}'"
print(delete_query)
cursor.execute(delete_query)
cnx.commit()

sql = """
INSERT INTO dws_product_daily_statis_di
(
    date
    , product_name
    , asin
    , marketplace_id
    , store_name
    , fn_sku
    , seller_sku
    , product_condition
    , fulfillable_quantity
    , inbound_working_quantity
    , inbound_shipped_quantity
    , inbound_receiving_quantity
    , total_reserved_quantity
    , pending_customer_order_quantity
    , pending_transshipment_quantity
    , fc_processing_quantity
    , total_researching_quantity
    , researching_quantity_breakdown
    , total_unfulfillable_quantity
    , customer_damaged_quantity
    , warehouse_damaged_quantity
    , distributor_damaged_quantity
    , carrier_damaged_quantity
    , defective_quantity
    , expired_quantity
    , last_updated_time
    , total_quantity
    , is_followed
    , status
    , product_description_value
    , product_type
    , browse_classification_display_name
    , operator
    , remote_delivery
    , classification_ranks
    , display_group_ranks
    , fulfillment_channel
    , avg_item_price_amount
    , quantity_sales_day
    , quantity_ordered_day
    , multi_channel_count_day
    , item_price_amount_day
    , fbm_sales_volume
    , fba_sales_volume
    , purchase_button_win_rate
    , ordered_product_count
    , total_ordered_product_count
    , quantity_refunded_day
    , quantity_refunded_amount_day
    , quantity_refunded_order_day
    , refunded_rate_day
    , session_count_pc
    , session_count_mobile
    , session_count_total
    , session_percentage_pc
    , session_percentage_mobile
    , session_percentage_total
    , product_session_percentage
    , page_views_pc_day
    , page_views_mobile_day
    , page_views_total_day
    , page_views_ad_day
    , page_views_nature_day
    , page_views_ad_percentage_today
    , page_views_nature_percentage_today
    , conversion_rate_day
    , impressions
    , clicks
    , cost_per_click
    , click_through_rate
    , cost
    , spend
    , campaign_budget_currency_code
    , campaign_budget_amount
    , campaign_budget_type
    , campaign_status
    , purchases_1d
    , purchases_7d
    , purchases_14d
    , purchases_30d
    , purchases_same_sku_1d
    , purchases_same_sku_7d
    , purchases_same_sku_14d
    , purchases_same_sku_30d
    , units_sold_clicks_1d
    , units_sold_clicks_7d
    , units_sold_clicks_14d
    , units_sold_clicks_30d
    , sales_1d
    , sales_7d
    , sales_14d
    , sales_30d
    , attributed_sales_same_sku_1d
    , attributed_sales_same_sku_7d
    , attributed_sales_same_sku_14d
    , attributed_sales_same_sku_30d
    , sales_other_sku_7d
    , units_sold_same_sku_1d
    , units_sold_same_sku_7d
    , units_sold_same_sku_14d
    , units_sold_same_sku_30d
    , units_sold_other_sku_7d
    , kindle_edition_normalized_pages_read_14d
    , kindle_edition_normalized_pages_royalties_14d
    , acos_clicks_7d
    , acos_clicks_14d
    , roas_clicks_7d
    , roas_clicks_14d
    , ad_sales_percentage
    , total_revenue
    , total_expenses
    , gross_profit
    , gross_profit_margin
    , remarks
)
select
    '{startDate}' as date
    , a.product_name
    , a.asin
    , a.marketplace_id
    , a.store_name
    , c.fn_sku
    , c.seller_sku
    , c.product_condition
    , c.fulfillable_quantity
    , c.inbound_working_quantity
    , c.inbound_shipped_quantity
    , c.inbound_receiving_quantity
    , c.total_reserved_quantity
    , c.pending_customer_order_quantity
    , c.pending_transshipment_quantity
    , c.fc_processing_quantity
    , c.total_researching_quantity
    , c.researching_quantity_breakdown
    , c.total_unfulfillable_quantity
    , c.customer_damaged_quantity
    , c.warehouse_damaged_quantity
    , c.distributor_damaged_quantity
    , c.carrier_damaged_quantity
    , c.defective_quantity
    , c.expired_quantity
    , c.last_updated_time
    , c.total_quantity
    , null as is_followed
    , null as status
    , a.product_description_value
    , a.product_type
    , a.browse_classification_display_name
    , null as operator
    , null remote_delivery
    , a.classification_rank
    , a.display_group_rank
    , b.fulfillment_channel
    , b.avg_item_price_amount
    , b.quantity_sales_day
    , b.quantity_ordered_day
    , b.multi_channel_count_day
    , b.item_price_amount_day
    , b.fbm_sales_volume
    , b.fba_sales_volume
    , b.purchase_button_win_rate
    , b.ordered_product_count
    , b.total_ordered_product_count
    , b.quantity_refunded_day
    , b.quantity_refunded_amount_day
    , b.quantity_refunded_order_day
    , b.refunded_rate_day
    , d.session_count_pc
    , d.session_count_mobile
    , d.session_count_total
    , d.session_percentage_pc
    , d.session_percentage_mobile
    , d.session_percentage_total
    , d.product_session_percentage
    , d.page_views_pc_day
    , d.page_views_mobile_day
    , d.page_views_total_day
    , e.impressions as page_views_ad_day
    , d.page_views_total_day as page_views_nature_day
    , e.impressions/d.page_views_total_day as page_views_ad_percentage_day
    , 1 - e.impressions/d.page_views_total_day as page_views_nature_percentage_day
    , e.conversion_rate as conversion_rate_day
    , e.impressions
    , e.clicks
    , e.cost_per_click
    , e.click_through_rate
    , e.cost
    , e.spend
    , e.campaign_budget_currency_code
    , e.campaign_budget_amount
    , e.campaign_budget_type
    , e.campaign_status
    , e.purchases_1d
    , e.purchases_7d
    , e.purchases_14d
    , e.purchases_30d
    , e.purchases_same_sku_1d
    , e.purchases_same_sku_7d
    , e.purchases_same_sku_14d
    , e.purchases_same_sku_30d
    , e.units_sold_clicks_1d
    , e.units_sold_clicks_7d
    , e.units_sold_clicks_14d
    , e.units_sold_clicks_30d
    , e.sales_1d
    , e.sales_7d
    , e.sales_14d
    , e.sales_30d
    , e.attributed_sales_same_sku_1d
    , e.attributed_sales_same_sku_7d
    , e.attributed_sales_same_sku_14d
    , e.attributed_sales_same_sku_30d
    , e.sales_other_sku_7d
    , e.units_sold_same_sku_1d
    , e.units_sold_same_sku_7d
    , e.units_sold_same_sku_14d
    , e.units_sold_same_sku_30d
    , e.units_sold_other_sku_7d
    , e.kindle_edition_normalized_pages_read_14d
    , e.kindle_edition_normalized_pages_royalties_14d
    , e.acos_clicks_7d
    , e.acos_clicks_14d
    , e.roas_clicks_7d
    , e.roas_clicks_14d
    , ifnull(if(b.item_price_amount_day=0,0,e.sales_1d/b.item_price_amount_day),0) as ad_sales_percentage
    , null as total_revenue
    , null as total_expenses
    , null as gross_profit
    , null as gross_profit_margin
    , null as remarks
from
(
    select
        asin
        , marketplace_id
        , item_name_value as product_name
        , marketplace_id as store_name
        , product_description_value
        , product_type
        , browse_classification_display_name
        , null as operator  -- 口径不清楚，可能是船长bi的属性
        , null as remote_delivery -- 无此项
        , json_extract(classification_ranks,'$[0].title') as classification_title
        , json_extract(classification_ranks,'$[0].rank') as classification_rank
        , json_extract(display_group_ranks,'$[0].title') as display_group_title
        , json_extract(display_group_ranks,'$[0].rank') as display_group_rank
    from ods_product_detail_data_di

) a
left join
(
    select
        asin
        , marketplace_id
        , fulfillment_channel
        , quantity_sales_day
        , quantity_ordered_day
        , multi_channel_count_day
        , item_price_amount_day
        , fbm_sales_volume
        , fba_sales_volume
        , purchase_button_win_rate
        , ordered_product_count
        , total_ordered_product_count
        , quantity_refunded_day
        , quantity_refunded_amount_day
        , quantity_refunded_order_day
        , refunded_rate_day
        , if(quantity_ordered_day= 0, 0,item_price_amount_day / quantity_sales_day)  as avg_item_price_amount
    from (
             select asin
                  , marketplace_id
                  , max(fulfillment_channel) as fulfillment_channel
                  , sum(if(order_status in ('Refunded', 'Pending', 'Canceled', 'PendingAvailability'), 0,
                           quantity_ordered))                                                           as quantity_sales_day    -- 完成交易的销量
                  , sum(quantity_ordered)                                                               as quantity_ordered_day  -- 接收交易的量
                  , null                                                                                as multi_channel_count_day
                  , sum(if(order_status in ('Refunded', 'Pending', 'Canceled', 'PendingAvailability'), 0,
                           item_price_amount))                                                          as item_price_amount_day -- 完成交易的天销售额
                  , sum(if(fulfillment_channel = 'MFN',
                           if(order_status in ('Refunded', 'Pending', 'Canceled', 'PendingAvailability'), 0,
                              quantity_ordered),
                           0))                                                                          as fbm_sales_volume
                  , sum(if(fulfillment_channel = 'AFN',
                           if(order_status in ('Refunded', 'Pending', 'Canceled', 'PendingAvailability'), 0,
                              quantity_ordered),
                           0))                                                                          as fba_sales_volume
                  , null                                                                                as purchase_button_win_rate
                  , null                                                                                as ordered_product_count
                  , null                                                                                as total_ordered_product_count
                  , sum(if(order_status = 'Refunded', quantity_ordered, 0))                             as quantity_refunded_day
                  , sum(if(order_status = 'Refunded', item_price_amount, 0))                            as quantity_refunded_amount_day
                  , count(distinct if(order_status = 'Refunded', amazon_order_id, 0))                   as quantity_refunded_order_day
                  , if(sum(quantity_ordered) = 0, 0, sum(if(order_status = 'Refunded', quantity_ordered, 0)) /
                                                     sum(quantity_ordered))                             as refunded_rate_day

             from (
                      select b2.asin
                           , b1.amazon_order_id
                           , b1.marketplace_id
                           , b1.fulfillment_channel
                           , b1.order_total_amount -- 订单总费用
                           , b2.quantity_ordered   -- '订单中的商品数量',
                           , b2.quantity_shipped   --  '已发货的商品数量',
                           , b2.number_of_items    --  'ASIN中包含的商品总数',
                           , b2.item_price_amount  -- '订单项的销售价格的金额'
                           , b1.order_status
                      from ods_order_orders_list_di b1
                               join ods_order_items_di b2
                                    on
                                        b1.amazon_order_id = b2.amazon_order_id
                      where substr(b1.purchase_date, 1, 10) = '{startDate}'
                  ) tmp
             group by asin
                    , marketplace_id
         ) tmp2
)  b
on
    a.asin = b.asin
    and a.marketplace_id = b.marketplace_id
left join
(
    select
        asin
        , marketplace_id
        , fn_sku
        , seller_sku
        , product_condition
        , fulfillable_quantity
        , inbound_working_quantity
        , inbound_shipped_quantity
        , inbound_receiving_quantity
        , total_reserved_quantity
        , pending_customer_order_quantity
        , pending_transshipment_quantity
        , fc_processing_quantity
        , total_researching_quantity
        , researching_quantity_breakdown
        , total_unfulfillable_quantity
        , customer_damaged_quantity
        , warehouse_damaged_quantity
        , distributor_damaged_quantity
        , carrier_damaged_quantity
        , defective_quantity
        , expired_quantity
        , last_updated_time
        , total_quantity
    from ods_fba_inventory_data_di
) c
on
    a.asin = c.asin
    and a.marketplace_id = c.marketplace_id

left join
(
    select
        child_asin as asin
        , marketplace_id
        , browser_sessions as session_count_pc
        , mobile_app_sessions as session_count_mobile
        , sessions as session_count_total
        , browser_session_percentage as session_percentage_pc
        , mobile_app_session_percentage as session_percentage_mobile
        , session_percentage as session_percentage_total
        , if(sum(sessions)over()=0,0,sessions/sum(sessions)over()) as product_session_percentage
        , browser_page_views as page_views_pc_day
        , mobile_page_views as page_views_mobile_day
        , page_views as page_views_total_day
    from ads_report_sp_sales_and_traffic_data_di
    where date = '{startDate}'

) d
on
    a.asin = d.asin
    and a.marketplace_id = d.marketplace_id
left join
(
    select
        advertised_asin as asin
        , marketplace_id
        , if(clicks=0,0,units_sold_clicks_1d/clicks) as conversion_rate   --   '天转化率',
        , impressions  --   '展示次数',
        , clicks  --   '点击次数',
        , cost_per_click  --   '每次点击成本',
        , click_through_rate  --   '点击率',
        , cost  --   '成本',
        , spend  --   '花费',
        , campaign_budget_currency_code  --   '广告活动预算货币代码',
        , campaign_budget_amount  --   '广告活动预算金额',
        , campaign_budget_type  --   '广告活动预算类型',
        , campaign_status  --   '广告活动状态',
        , purchases_1d  --   1  天内购买次数',
        , purchases_7d  --   '7  天内购买次数',
        , purchases_14d  --   '14  天内购买次数',
        , purchases_30d  --   '30  天内购买次数',
        , purchases_same_sku_1d  --   '1  天内相同  SKU  购买次数',
        , purchases_same_sku_7d  --   '7  天内相同  SKU  购买次数',
        , purchases_same_sku_14d  --   '14  天内相同  SKU  购买次数',
        , purchases_same_sku_30d  --   '30  天内相同  SKU  购买次数',
        , units_sold_clicks_1d  --   '1  天内点击后售出数量',
        , units_sold_clicks_7d  --   '7  天内点击后售出数量',
        , units_sold_clicks_14d  --   '14  天内点击后售出数量',
        , units_sold_clicks_30d  --   '30  天内点击后售出数量',
        , sales_1d  --   '1  天内销售额',
        , sales_7d  --   '7  天内销售额',
        , sales_14d  --   '14  天内销售额',
        , sales_30d  --   '30  天内销售额',
        , attributed_sales_same_sku_1d  --   '1  天内相同  SKU  归因销售额',
        , attributed_sales_same_sku_7d  --   '7  天内相同  SKU  归因销售额',
        , attributed_sales_same_sku_14d  --   '14  天内相同  SKU  归因销售额',
        , attributed_sales_same_sku_30d  --   '30  天内相同  SKU  归因销售额',
        , sales_other_sku_7d  --   '7  天内其他  SKU  销售额',
        , units_sold_same_sku_1d  --   '1  天内相同  SKU  售出数量',
        , units_sold_same_sku_7d  --   '7  天内相同  SKU  售出数量',
        , units_sold_same_sku_14d  --   '14  天内相同  SKU  售出数量',
        , units_sold_same_sku_30d  --   '30  天内相同  SKU  售出数量',
        , units_sold_other_sku_7d  --   '7  天内其他  SKU  售出数量',
        , kindle_edition_normalized_pages_read_14d  --   '14  天内阅读的  Kindle  版归一化页数',
        , kindle_edition_normalized_pages_royalties_14d  --   '14  天内  Kindle  版归一化页数的版税',
        , acos_clicks_7d  --   '7  天内广告投入产出比（ACoS）',
        , acos_clicks_14d  --   '14  天内广告投入产出比（ACoS）',
        , roas_clicks_7d  --   '7  天内投资回报率（ROAS）',
        , roas_clicks_14d  --   '14  天内投资回报率（ROAS）',
    from ads_report_ad_advertised_product_di
    where date =  '{startDate}'
) e
on a.asin = e.asin
where b.asin is not null
or d.asin is not null
or e.asin is not null
""".format(startDate=startDate)
cursor.execute(sql)
cnx.commit()
```


### 建表信息DDL
```sql
CREATE TABLE `dws_product_daily_statis_di` (
    `date` date DEFAULT NULL COMMENT '统计日期',
    `product_name` varchar(500) DEFAULT NULL COMMENT '商品名称',
    `asin` varchar(50) DEFAULT NULL COMMENT '商品的亚马逊标准识别号码（ASIN）',
    `marketplace_id` varchar(50) DEFAULT NULL COMMENT '市场id',
    `store_name` varchar(50) DEFAULT NULL COMMENT '店铺名称',
    `fn_sku` varchar(100) DEFAULT NULL COMMENT '亚马逊物流网络SKU标识符',
    `seller_sku` varchar(100) DEFAULT NULL COMMENT '卖家SKU',
    `product_condition` varchar(255) DEFAULT NULL COMMENT '卖家描述的商品状况（例如，全新商品）',
    `fulfillable_quantity` int DEFAULT NULL COMMENT '可供拣选、打包和发货的商品数量',
    `inbound_working_quantity` int DEFAULT NULL COMMENT '已通知亚马逊的入库货件数量',
    `inbound_shipped_quantity` int DEFAULT NULL COMMENT '已通知亚马逊并提供跟踪号的入库货件数量',
    `inbound_receiving_quantity` int DEFAULT NULL COMMENT '尚未在亚马逊配送中心接收处理，但已有部分入库货件接收处理的数量',
    `total_reserved_quantity` int DEFAULT NULL COMMENT '亚马逊配送网络中当前正在拣选、打包和发货，或因测量、抽样等内部流程而暂时搁置的商品总数量',
    `pending_customer_order_quantity` int DEFAULT NULL COMMENT '预留给客户订单的商品数量',
    `pending_transshipment_quantity` int DEFAULT NULL COMMENT '正从一个配送中心转移到另一个配送中心的商品数量',
    `fc_processing_quantity` int DEFAULT NULL COMMENT '在配送中心暂时搁置以进行额外处理的商品数量',
    `total_researching_quantity` int DEFAULT NULL COMMENT '亚马逊配送网络中当前正在研究的商品总数量',
    `researching_quantity_breakdown` text COMMENT '当前正在研究的商品数量明细（数组）',
    `total_unfulfillable_quantity` int DEFAULT NULL COMMENT '亚马逊配送网络中不可售商品的总数量',
    `customer_damaged_quantity` int DEFAULT NULL COMMENT '客户损坏状态的商品数量',
    `warehouse_damaged_quantity` int DEFAULT NULL COMMENT '仓库损坏状态的商品数量',
    `distributor_damaged_quantity` int DEFAULT NULL COMMENT '分销商损坏状态的商品数量',
    `carrier_damaged_quantity` int DEFAULT NULL COMMENT '运输商损坏状态的商品数量',
    `defective_quantity` int DEFAULT NULL COMMENT '缺陷状态的商品数量',
    `expired_quantity` int DEFAULT NULL COMMENT '过期状态的商品数量',
    `last_updated_time` varchar(255) DEFAULT NULL COMMENT '最后更新任何数量的日期和时间',
    `total_quantity` int DEFAULT NULL COMMENT '入库货件或亚马逊配送中心中的商品总数量',
    `is_followed` tinyint(1) DEFAULT NULL COMMENT '是否关注',
    `status` varchar(50) DEFAULT NULL COMMENT '状态',
    `product_description_value` text COMMENT '产品描述值',
    `product_type` varchar(255) DEFAULT NULL COMMENT '产品类型',
    `browse_classification_display_name` varchar(255) DEFAULT NULL COMMENT '浏览分类显示名称',
    `operator` varchar(50) DEFAULT NULL COMMENT '操作员',
    `remote_delivery` varchar(50) DEFAULT NULL COMMENT '偏远配送',
    `classification_ranks` json DEFAULT NULL COMMENT '按商品类别的销售排名',
    `display_group_ranks` json DEFAULT NULL COMMENT '按网站显示组划分的销售排名',
    `fulfillment_channel` varchar(50) DEFAULT NULL COMMENT '订单履行渠道（亚马逊履行或卖家履行）',
    `avg_item_price_amount` double DEFAULT NULL COMMENT '天平均销售单价',
    `quantity_sales_day` int DEFAULT NULL COMMENT '天销量',
    `quantity_ordered_day` int DEFAULT NULL COMMENT '天订单量',
    `multi_channel_count_day` int DEFAULT NULL COMMENT '天多渠道数量',
    `item_price_amount_day` double DEFAULT NULL COMMENT '天销售额',
    `fbm_sales_volume` int DEFAULT NULL COMMENT 'FBM 销量',
    `fba_sales_volume` int DEFAULT NULL COMMENT 'FBA 销量',
    `purchase_button_win_rate` double DEFAULT NULL COMMENT '购买按钮赢得率',
    `ordered_product_count` int DEFAULT NULL COMMENT '已订购产品数量',
    `total_ordered_product_count` int DEFAULT NULL COMMENT '总已订购产品数量',
    `quantity_refunded_day` int DEFAULT NULL COMMENT '天退款量',
    `quantity_refunded_amount_day` int DEFAULT NULL COMMENT '天退款量',
    `quantity_refunded_order_day` int DEFAULT NULL COMMENT '天退款订单数',
    `refunded_rate_day` double DEFAULT NULL COMMENT '天退款率',
    `session_count_pc` int DEFAULT NULL COMMENT 'PC 端会话次数',
    `session_count_mobile` int DEFAULT NULL COMMENT '移动端会话次数',
    `session_count_total` int DEFAULT NULL COMMENT '总会话次数',
    `session_percentage_pc` double DEFAULT NULL COMMENT 'PC 端会话百分比',
    `session_percentage_mobile` double DEFAULT NULL COMMENT '移动端会话百分比',
    `session_percentage_total` double DEFAULT NULL COMMENT '总会话百分比',
    `product_session_percentage` double DEFAULT NULL COMMENT '产品会话百分比',
    `page_views_pc_day` int DEFAULT NULL COMMENT '天pc端流量',
    `page_views_mobile_day` int DEFAULT NULL COMMENT '天移动端流量',
    `page_views_total_day` int DEFAULT NULL COMMENT '天总计流量',
    `page_views_ad_day` int DEFAULT NULL COMMENT '天广告流量',
    `page_views_nature_day` int DEFAULT NULL COMMENT '天自然流量',
    `page_views_ad_percentage_today` double DEFAULT NULL COMMENT '天广告流量占比',
    `page_views_nature_percentage_today` double DEFAULT NULL COMMENT '天自然流量占比',
    `conversion_rate_day` double DEFAULT NULL COMMENT '天转化率',
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
    `ad_sales_percentage` double DEFAULT NULL COMMENT '广告销售百分比',
    `total_revenue` double DEFAULT NULL COMMENT '总收入',
    `total_expenses` double DEFAULT NULL COMMENT '总支出',
    `gross_profit` double DEFAULT NULL COMMENT '毛利润',
    `gross_profit_margin` double DEFAULT NULL COMMENT '毛利率',
    `remarks` varchar(500) CHARACTER SET utf8 COLLATE utf8_general_ci DEFAULT NULL COMMENT '备注'
) ENGINE = InnoDB DEFAULT CHARSET = utf8 COMMENT = '亚马逊商品宽表，从ods表计算得来。以商品为主体，按天粒度统计广告、销售等数据'
```