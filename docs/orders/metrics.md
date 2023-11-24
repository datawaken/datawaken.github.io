
# 订单域指标库

## 订单量
### metric name(english)
`order_cnt`

### SQL表达式
`count(if(order_status <> "canceled",1,null))`

### 业务概念
用户下单操作，与平台发生的交易行为，生成一笔订单。


### 口径说明（数觉BI）
实际发生的订单总量，不含已取消的订单。



## 订单金额
### metric name(english)
`order_amt`

### SQL表达式

`sum(item_price_amount +  shipping_price_amount + gift_wrap_price_amount + item_tax_amount + shipping_tax_amount + gift_wrap_tax_amount)`

> 对应API字段
> `sum(ItemPrice +  ShippingPrice + GiftWrapPrice + ItemTax + + ShippingTax + GiftWrapTax)`

~~`sum(item_price - item_promotion_discount + shipping_price - ship_promotion_discount + gift_wrap_price + item_tax + shipping_tax + gift_wrap_tax + Shipping_Discount_Tax + Promotion_Discount_Tax)`~~

### 口径说明（数觉BI）
实际成交订单交易总额GMV，包含运费、包装费、税费；不含下单未支付订单，不含已取消订单，不含促销折扣。

!> 这里需要确认，selling price是否包含promotion discount. 就目前已知的信息来看，是不含的；
!>ItemPrice: The selling price of the order item. Note that an order item is an item and a quantity. This means that **the value of ItemPrice is equal to the selling price of the item multiplied by the quantity ordered.** Note that ItemPrice excludes ShippingPrice and GiftWrapPrice.

?> 遗留事项（非紧急）：确认包装费、运费、折扣的税费是否包含在ItemPrice中。

## 销量

### metric name
`order_item_cnt`

### SQL表达式
`sum(quantity_ordered)`

> 对应API字段：`quantity`

### 口径说明



## 销售额
### metric name
`order_amt_actual`

### SQL表达式
`sum(item_price_amount)`

### 口径说明（数觉BI）
实际发生订单中的商品销售金额总和，商品销售金额总和是指商品数量与商品单价的乘积


## 每单平均销量
### metric name
order_item_cnt_avg

### SQL表达式
`sum(quantity)/count(if(order_status <> "canceled",1,null))`


## 平均单品销售额
### metric name
`item_price_avg`

### SQL表达式
`sum(item_price)/sum(quantity)`


## 多渠道销量



## FBA销量


## FBM销量


