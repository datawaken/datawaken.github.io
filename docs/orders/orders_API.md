# Amazon API

## 概述
The [Selling Partner API for Orders](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference) helps you **programmatically retrieve order information**. These APIs let you develop fast, flexible, custom applications in areas like order synchronization, order research, and demand-based decision support tools. The Orders API supports orders that are **two years old or less**. Orders more than two years old will not show in the API response.

_Note:_ The Orders API supports orders from 2016 and after for the JP, AU, and SG marketplaces.


## API列表(v0)

### PATH
- [GET /orders/v0/orders](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#get-ordersv0orders)
- [GET /orders/v0/orders/{orderId}](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#get-ordersv0ordersorderid)
- [GET /orders/v0/orders/{orderId}/buyerInfo](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#get-ordersv0ordersorderidbuyerinfo)
- [GET /orders/v0/orders/{orderId}/address](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#get-ordersv0ordersorderidaddress)
- [GET /orders/v0/orders/{orderId}/orderItems](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#get-ordersv0ordersorderidorderitems)
- [GET /orders/v0/orders/{orderId}/orderItems/buyerInfo](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#get-ordersv0ordersorderidorderitemsbuyerinfo)
- [POST /orders/v0/orders/{orderId}/shipment](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#post-ordersv0ordersorderidshipment)
- [GET /orders/v0/orders/{orderId}/regulatedInfo](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#get-ordersv0ordersorderidregulatedinfo)
- [PATCH /orders/v0/orders/{orderId}/regulatedInfo](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#patch-ordersv0ordersorderidregulatedinfo)
- [POST /orders/v0/orders/{orderId}/shipmentConfirmation](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#post-ordersv0ordersorderidshipmentconfirmation)
- [Error Responses and Schemas](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#error-responses-and-schemas)

### Operations
[getOrders](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#getorders)  
[getOrder](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#getorder)  
[getOrderBuyerInfo](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#getorderbuyerinfo)  
[getOrderAddress](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#getorderaddress)  
[getOrderItems](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#getorderitems)  
[getOrderItemsBuyerInfo](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#getorderitemsbuyerinfo)  
[updateShipmentStatus](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#updateshipmentstatus)  
[getOrderRegulatedInfo](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#getorderregulatedinfo)  
[updateVerificationStatus](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#updateverificationstatus)  
[confirmShipment](https://developer-docs.amazon.com/sp-api/docs/orders-api-v0-reference#confirmshipment)

---
