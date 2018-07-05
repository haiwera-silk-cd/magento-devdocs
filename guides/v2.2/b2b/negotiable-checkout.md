---
group: b2b
subgroup: 10_REST
title: 协商报价结算
menu_title: 协商报价结算
menu_order: 34
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: nq
github_link: b2b/negotiable-checkout.md
functional_areas:
  - B2B
  - Integration
---

当销售者和购买者用户接受报价产品和它们的价格时，商议报价即准备好转成订单。

在标准结算过程中，Magento刷新并重新计算所有产品和物流的价格以及税费。此过程与有商议价格(销售者提供折扣)的报价不同，系统保持报价，但检查税额。如果税额过期，Magento重新计算它们更新总报价。税额调整可以改变订单的总价。订单和发票随重新计算而创建。所有其它价格保持不变。

相同的规则也被应用于当报价有提供物流价格并且物流价格在结算时发生了改变时。购买者支付更新后的价格，但这并不会影响其的报价金额。

下图说明了{{site.data.var.b2b}}商议报价结算的工作流程：

![结算过程]({{ page.baseurl }}/b2b/images/quote-checkout-process.png)

## 管理物流地址

议价可以在没有物流地址的情况下启动。然而在定单被确认前，物流地址必须提供。

**REST接口**

{% highlight json %}
POST /V1/negotiable-carts/:cartId/estimate-shipping-methods
POST /V1/negotiable-carts/:cartId/estimate-shipping-methods-by-address-id
POST /V1/negotiable-carts/:cartId/shipping-information
{% endhighlight %}

### 估计物流指定地址的花费

此调用拿一个完整的物流地址作为输入来估算运费。它返回一个物流方式的列表。

**服务名称**

`negotiableQuoteShipmentEstimationV1`

**样例用法**

`POST /V1/negotiable-carts/86/estimate-shipping-methods`

**载荷**

{% highlight json %}
{
  "address": {
  "street": [
      "100 Big Tree Avenue"
    ],
  "city": "San Francisco",
  "country_id": "US",
  "region": "California",
  "region_id": "12",
  "postcode": "99999",
  "telephone": "4155551212",
  "firstname": "John",
  "lastname": "Doe"
  }
}
{% endhighlight %}

**响应**

{% highlight json %}
[
  {
    "carrier_code": "flatrate",
    "method_code": "flatrate",
    "carrier_title": "Flat Rate",
    "method_title": "Fixed",
    "amount": 5,
    "base_amount": 5,
    "available": true,
    "error_message": "",
    "price_excl_tax": 5,
    "price_incl_tax": 5
  }
]

{% endhighlight %}

### 估计指定地址ID物流花费

此调用拿一个地址ID作为输入估算运费。它返回一个物流方式的列表。

**服务名称**

`negotiableQuoteShippingMethodManagementV1`

**样例用法**

`POST /V1/negotiable-carts/86/estimate-shipping-methods-by-address-id`

**载荷**

{% highlight json %}
{
  "addressId": 2
}
{% endhighlight %}

**响应**

{% highlight json %}
[
  {
    "carrier_code": "flatrate",
    "method_code": "flatrate",
    "carrier_title": "Flat Rate",
    "method_title": "Fixed",
    "amount": 5,
    "base_amount": 5,
    "available": true,
    "error_message": "",
    "price_excl_tax": 5,
    "price_incl_tax": 5
  }
]

{% endhighlight %}

### 设置物流和账单信息

在此调用中，指定物流和账单地址及选择`shipping_carrier_code` 和 `shipping_method_code`。Magento返回一个支付选项列表和算出的订单总价。

**服务名称**

`negotiableQuoteShippingMethodManagementV1`

**样例用法**

`POST /V1/negotiable-carts/86/shipping-information`

**载荷**

{% highlight json %}
{  "addressInformation": {
	  "shipping_address": {
       "region": "California",
       "region_id": 12,
       "country_id": "US",
       "street": [
      "100 Big Tree Avenue"
      ],
      "postcode": "99999",
      "city": "San Francisco",
      "telephone": "512-555-1111",
      "firstname": "Jane",
      "lastname": "Doe"
  },
  "billing_address": {
  	"region": "New York",
    "region_id": 43,
    "region_code": "NY",
    "country_id": "US",
    "street": [
      "123 Oak Ave"
    ],
    "postcode": "10577",
    "city": "Purchase",
    "firstname": "Jane",
    "lastname": "Doe",
    "email": "jdoe@example.com",
    "telephone": "512-555-1111"
  },
  "shipping_carrier_code": "flatrate",
  "shipping_method_code": "flatrate"
  }
}
{% endhighlight %}

**响应**

{% collapsible Show code sample %}
{% highlight json %}
{
  "payment_methods": [
    {
      "code": "checkmo",
      "title": "Check / Money order"
    }
  ],
  "totals": {
    "grand_total": 5.95,
    "base_grand_total": 5.95,
    "subtotal": 0.95,
    "base_subtotal": 0.95,
    "discount_amount": 0,
    "base_discount_amount": 0,
    "subtotal_with_discount": 0.95,
    "base_subtotal_with_discount": 0.95,
    "shipping_amount": 5,
    "base_shipping_amount": 5,
    "shipping_discount_amount": 0,
    "base_shipping_discount_amount": 0,
    "tax_amount": 0,
    "base_tax_amount": 0,
    "weee_tax_applied_amount": null,
    "shipping_tax_amount": 0,
    "base_shipping_tax_amount": 0,
    "subtotal_incl_tax": 0.95,
    "shipping_incl_tax": 5,
    "base_shipping_incl_tax": 5,
    "base_currency_code": "USD",
    "quote_currency_code": "USD",
    "items_qty": 1,
    "items": [
      {
        "item_id": 13,
        "price": 0.95,
        "base_price": 0.95,
        "qty": 1,
        "row_total": 0.95,
        "base_row_total": 0.95,
        "row_total_with_discount": 0,
        "tax_amount": 0,
        "base_tax_amount": 0,
        "tax_percent": 0,
        "discount_amount": 0,
        "base_discount_amount": 0,
        "discount_percent": 0,
        "price_incl_tax": 0.95,
        "base_price_incl_tax": 0.95,
        "row_total_incl_tax": 0.95,
        "base_row_total_incl_tax": 0.95,
        "options": "[]",
        "weee_tax_applied_amount": null,
        "weee_tax_applied": null,
        "extension_attributes": {
          "negotiable_quote_item_totals": {
            "cost": 0,
            "catalog_price": 0.95,
            "base_catalog_price": 0.95,
            "catalog_price_incl_tax": 0.95,
            "base_catalog_price_incl_tax": 0.95,
            "cart_price": 0.95,
            "base_cart_price": 0.95,
            "cart_tax": 0,
            "base_cart_tax": 0,
            "cart_price_incl_tax": 0.95,
            "base_cart_price_incl_tax": 0.95
          }
        },
        "name": "Simple Product 2"
      }
    ],
    "total_segments": [
      {
        "code": "subtotal",
        "title": "Subtotal",
        "value": 0.95
      },
      {
        "code": "giftwrapping",
        "title": "Gift Wrapping",
        "value": null,
        "extension_attributes": {
          "gw_item_ids": [],
          "gw_price": "0.00",
          "gw_base_price": "0.00",
          "gw_items_price": "0.00",
          "gw_items_base_price": "0.00",
          "gw_card_price": "0.00",
          "gw_card_base_price": "0.00",
          "gw_base_tax_amount": "0.00",
          "gw_tax_amount": "0.00",
          "gw_items_base_tax_amount": "0.00",
          "gw_items_tax_amount": "0.00",
          "gw_card_base_tax_amount": "0.00",
          "gw_card_tax_amount": "0.00",
          "gw_price_incl_tax": "0.00",
          "gw_base_price_incl_tax": "0.00",
          "gw_card_price_incl_tax": "0.00",
          "gw_card_base_price_incl_tax": "0.00",
          "gw_items_price_incl_tax": "0.00",
          "gw_items_base_price_incl_tax": "0.00"
        }
      },
      {
        "code": "shipping",
        "title": "Shipping & Handling (Flat Rate - Fixed)",
        "value": 5
      },
      {
        "code": "tax",
        "title": "Tax",
        "value": 0,
        "extension_attributes": {
          "tax_grandtotal_details": []
        }
      },
      {
        "code": "grand_total",
        "title": "Grand Total",
        "value": 5.95,
        "area": "footer"
      },
      {
        "code": "customerbalance",
        "title": "Store Credit",
        "value": 0
      },
      {
        "code": "reward",
        "title": "0 Reward points",
        "value": 0
      }
    ],
    "extension_attributes": {
      "negotiable_quote_totals": {
        "items_count": 1,
        "quote_status": "submitted_by_admin",
        "created_at": "2017-05-30 20:41:00",
        "updated_at": "2017-05-30 20:41:00",
        "customer_group": 10,
        "base_to_quote_rate": 1,
        "cost_total": 0,
        "base_cost_total": 0,
        "original_total": 0.95,
        "base_original_total": 0.95,
        "original_tax": 0,
        "base_original_tax": 0,
        "original_price_incl_tax": 0.95,
        "base_original_price_incl_tax": 0.95,
        "negotiated_price_type": null,
        "negotiated_price_value": null
      },
      "reward_points_balance": 0,
      "reward_currency_amount": 0,
      "base_reward_currency_amount": 0
    }
  }
}
{% endhighlight %}
{% endcollapsible %}

## 管理账单地址

如果账单地址没有通过其它调用提供，可以使用`POST /V1/negotiable-carts/:cartId/billing-address`调用来指定。

**服务名称**

`negotiableQuoteBillingAddressManagementV1`

**REST接口**

{% highlight json %}
POST /V1/negotiable-carts/:cartId/billing-address
GET /V1/negotiable-carts/:cartId/billing-address
{% endhighlight %}

### 设置账单地址

此调用分配账单地址到指定的议价中。

**样例用法**

`POST /V1/negotiable-carts/86/billing-address`

**载荷**

{% highlight json %}
{  "address": {
      "region": "New York",
      "region_id": 43,
      "region_code": "NY",
      "country_id": "US",
      "street": [
        "123 Oak Ave"
        ],
      "postcode": "10577",
      "city": "Purchase",
      "firstname": "Jane",
      "lastname": "Doe",
      "customer_id": 4,
      "email": "jdoe@example.com",
      "telephone": "(512) 555-1111",
      "same_as_billing": 1
  }
}
{% endhighlight %}

**响应**

[]

### 返回账单地址

此调用返回指定议价的账单地址

**示例用法**

`GET /V1/negotiable-carts/86/billing-address`

**载荷**

不适用

**响应**

{% highlight json %}
{
  "id": 192,
  "region": "New York",
  "region_id": 43,
  "region_code": "NY",
  "country_id": "US",
  "street": [
    "123 Oak Ave"
  ],
  "telephone": "(512) 555-1111",
  "postcode": "10577",
  "city": "Purchase",
  "firstname": "Jane",
  "lastname": "Doe",
  "customer_id": 1,
  "email": "jdoe@example.com",
  "same_as_billing": 0,
  "save_in_address_book": 0
}
{% endhighlight %}

## 管理优惠券

B2B允许在支付时使用优惠券

**服务名称**

`negotiableQuoteCouponManagementV1`

**REST接口**

{% highlight json %}
PUT /V1/negotiable-carts/:cartId/coupons/:couponCode
DELETE /V1/negotiable-carts/:cartId/coupons
{% endhighlight %}

### 在议价中应用优惠券

如果初始的报价应用了一个优惠券到总价上，在转化报价到议价时Magento忽略此优惠券。然而你可以在结算的时候应用优惠券。

**样例用法**

PUT /V1/negotiable-carts/6/coupons/SAVE5

**载荷**

不适用

**响应**

`true`,指示请求成功

## 管理礼品卡

B2B允许支付时使用礼品卡

**服务名称**

`negotiableQuoteGiftCardAccountManagementV1`

**REST接口**

{% highlight json %}
POST /V1/negotiable-carts/:cartId/giftCards
DELETE /V1/negotiable-carts/:cartId/giftCards/:giftCardCode
{% endhighlight %}

### 应用礼品卡到议价中

如果报价初始在总价上有礼品卡，在报价转化为议价时Magento会忽略它。然而你可以在结算的时候应用礼品卡。

**样例用法**

`POST /V1/negotiable-carts/6/giftCards`

**载荷**

{% highlight json %}
{
  "giftCardAccountData": {
    "gift_cards": [
      "00HELHQED6RV"
    ]
  }
}
{% endhighlight %}

**响应**

`true`

### 结算时删除礼品卡

此调用移除已经应用在议价上的礼品卡。

**样例用法**

`DELETE /V1/negotiable-carts/6/giftCards/00HELHQED6RV`

**载荷**

不适用

**响应**

`true`,指示请求成功

## 管理支付信息

当你提交支付信息时，Magento创建一个定单并发送订单确认给购买者。

**服务名称**

`negotiableQuotePaymentInformationManagementV1`

**REST接口**

{% highlight json %}
POST /V1/negotiable-carts/:cartId/payment-information
GET /V1/negotiable-carts/:cartId/payment-information
POST /V1/negotiable-carts/:cartId/set-payment-information
{% endhighlight %}

### 不确认定单设置支付信息

此调用设置议价的支付信息及账单地址。然而,完成之后Magento不一并创建订单。

**样例用法**

`POST /V1/negotiable-carts/86/set-payment-information`

**载荷**

{% highlight json %}
{  "paymentMethod": {
   "po_number": "A123456",
   "method": "checkmo"
  },
  "billing_address": {
  	"region": "New York",
    "region_id": 43,
    "region_code": "NY",
    "country_id": "US",
    "street": [
      "123 Oak Ave"
    ],
    "postcode": "10577",
    "city": "Purchase",
    "firstname": "Jane",
    "lastname": "Doe",
    "email": "jdoe@example.com",
    "telephone": "512-555-1111"
  }
}
{% endhighlight %}

**响应**

`true`, 指示支付信息设置成功

### 设置支付信息并确认订单

此调用为议价设置支付信息及账单地址并一并创建订单。

**样例用法**

`POST /V1/negotiable-carts/86/payment-information`

**载荷**

{% highlight json %}
{  "paymentMethod": {
    "po_number": "A123456",
    "method": "checkmo"
  },
  "billing_address": {
  	"region": "New York",
    "region_id": 43,
    "region_code": "NY",
    "country_id": "US",
    "street": [
      "123 Oak Ave"
    ],
    "postcode": "10577",
    "city": "Purchase",
    "firstname": "Jane",
    "lastname": "Doe",
    "email": "jdoe@example.com",
    "telephone": "512-555-1111"
  }
}
{% endhighlight %}

**响应**

订单ID，比如`83`

### 返回支付信息

此调用返回支付信息及`totals`对象的所有信息

**样例用法**

`GET /V1/negotiable-carts/86/payment-information`

**载荷**

不适用

**响应**

{% collapsible Show code sample %}
{% highlight json %}
{
  "payment_methods": [
    {
      "code": "checkmo",
      "title": "Check / Money order"
    }
  ],
  "totals": {
    "grand_total": 5.95,
    "base_grand_total": 5.95,
    "subtotal": 0.95,
    "base_subtotal": 0.95,
    "discount_amount": 0,
    "base_discount_amount": 0,
    "subtotal_with_discount": 0.95,
    "base_subtotal_with_discount": 0.95,
    "shipping_amount": 5,
    "base_shipping_amount": 5,
    "shipping_discount_amount": 0,
    "base_shipping_discount_amount": 0,
    "tax_amount": 0,
    "base_tax_amount": 0,
    "weee_tax_applied_amount": null,
    "shipping_tax_amount": 0,
    "base_shipping_tax_amount": 0,
    "subtotal_incl_tax": 0.95,
    "shipping_incl_tax": 5,
    "base_shipping_incl_tax": 5,
    "base_currency_code": "USD",
    "quote_currency_code": "USD",
    "items_qty": 1,
    "items": [
      {
        "item_id": 13,
        "price": 0.95,
        "base_price": 0.95,
        "qty": 1,
        "row_total": 0.95,
        "base_row_total": 0.95,
        "row_total_with_discount": 0,
        "tax_amount": 0,
        "base_tax_amount": 0,
        "tax_percent": 0,
        "discount_amount": 0,
        "base_discount_amount": 0,
        "discount_percent": 0,
        "price_incl_tax": 0.95,
        "base_price_incl_tax": 0.95,
        "row_total_incl_tax": 0.95,
        "base_row_total_incl_tax": 0.95,
        "options": "[]",
        "weee_tax_applied_amount": null,
        "weee_tax_applied": null,
        "extension_attributes": {
          "negotiable_quote_item_totals": {
            "cost": 0,
            "catalog_price": 0.95,
            "base_catalog_price": 0.95,
            "catalog_price_incl_tax": 0.95,
            "base_catalog_price_incl_tax": 0.95,
            "cart_price": 0.95,
            "base_cart_price": 0.95,
            "cart_tax": 0,
            "base_cart_tax": 0,
            "cart_price_incl_tax": 0.95,
            "base_cart_price_incl_tax": 0.95
          }
        },
        "name": "Simple Product 2"
      }
    ],
    "total_segments": [
      {
        "code": "subtotal",
        "title": "Subtotal",
        "value": 0.95
      },
      {
        "code": "giftwrapping",
        "title": "Gift Wrapping",
        "value": null,
        "extension_attributes": {
          "gw_item_ids": [],
          "gw_price": "0.00",
          "gw_base_price": "0.00",
          "gw_items_price": "0.00",
          "gw_items_base_price": "0.00",
          "gw_card_price": "0.00",
          "gw_card_base_price": "0.00",
          "gw_base_tax_amount": "0.00",
          "gw_tax_amount": "0.00",
          "gw_items_base_tax_amount": "0.00",
          "gw_items_tax_amount": "0.00",
          "gw_card_base_tax_amount": "0.00",
          "gw_card_tax_amount": "0.00",
          "gw_price_incl_tax": "0.00",
          "gw_base_price_incl_tax": "0.00",
          "gw_card_price_incl_tax": "0.00",
          "gw_card_base_price_incl_tax": "0.00",
          "gw_items_price_incl_tax": "0.00",
          "gw_items_base_price_incl_tax": "0.00"
        }
      },
      {
        "code": "shipping",
        "title": "Shipping & Handling (Flat Rate - Fixed)",
        "value": 5
      },
      {
        "code": "tax",
        "title": "Tax",
        "value": 0,
        "extension_attributes": {
          "tax_grandtotal_details": []
        }
      },
      {
        "code": "grand_total",
        "title": "Grand Total",
        "value": 5.95,
        "area": "footer"
      },
      {
        "code": "customerbalance",
        "title": "Store Credit",
        "value": 0
      },
      {
        "code": "reward",
        "title": "0 Reward points",
        "value": 0
      }
    ],
    "extension_attributes": {
      "negotiable_quote_totals": {
        "items_count": 1,
        "quote_status": "submitted_by_admin",
        "created_at": "2017-05-30 20:41:00",
        "updated_at": "2017-06-09 20:26:49",
        "customer_group": 10,
        "base_to_quote_rate": 1,
        "cost_total": 0,
        "base_cost_total": 0,
        "original_total": 0.95,
        "base_original_total": 0.95,
        "original_tax": 0,
        "base_original_tax": 0,
        "original_price_incl_tax": 0.95,
        "base_original_price_incl_tax": 0.95,
        "negotiated_price_type": null,
        "negotiated_price_value": null
      },
      "reward_points_balance": 0,
      "reward_currency_amount": 0,
      "base_reward_currency_amount": 0
    }
  }
}
{% endhighlight %}
{% endcollapsible %}

## 浏览购物车总价

此调用与`GET /V1/negotiable-carts/:cartId/payment-information`类似，但不返回支付信息

**服务名称**

`negotiableQuoteCartTotalRepositoryV1`

**REST接口**

{% highlight json %}
GET /V1/negotiable-carts/:cartId/totals
{% endhighlight %}

**样例用法**

`GET /V1/negotiable-carts/86/totals`

**载荷**

不适用

**响应**

{% collapsible Show code sample %}
{% highlight json %}
{
  "totals": {
    "grand_total": 5.95,
    "base_grand_total": 5.95,
    "subtotal": 0.95,
    "base_subtotal": 0.95,
    "discount_amount": 0,
    "base_discount_amount": 0,
    "subtotal_with_discount": 0.95,
    "base_subtotal_with_discount": 0.95,
    "shipping_amount": 5,
    "base_shipping_amount": 5,
    "shipping_discount_amount": 0,
    "base_shipping_discount_amount": 0,
    "tax_amount": 0,
    "base_tax_amount": 0,
    "weee_tax_applied_amount": null,
    "shipping_tax_amount": 0,
    "base_shipping_tax_amount": 0,
    "subtotal_incl_tax": 0.95,
    "shipping_incl_tax": 5,
    "base_shipping_incl_tax": 5,
    "base_currency_code": "USD",
    "quote_currency_code": "USD",
    "items_qty": 1,
    "items": [
      {
        "item_id": 13,
        "price": 0.95,
        "base_price": 0.95,
        "qty": 1,
        "row_total": 0.95,
        "base_row_total": 0.95,
        "row_total_with_discount": 0,
        "tax_amount": 0,
        "base_tax_amount": 0,
        "tax_percent": 0,
        "discount_amount": 0,
        "base_discount_amount": 0,
        "discount_percent": 0,
        "price_incl_tax": 0.95,
        "base_price_incl_tax": 0.95,
        "row_total_incl_tax": 0.95,
        "base_row_total_incl_tax": 0.95,
        "options": "[]",
        "weee_tax_applied_amount": null,
        "weee_tax_applied": null,
        "extension_attributes": {
          "negotiable_quote_item_totals": {
            "cost": 0,
            "catalog_price": 0.95,
            "base_catalog_price": 0.95,
            "catalog_price_incl_tax": 0.95,
            "base_catalog_price_incl_tax": 0.95,
            "cart_price": 0.95,
            "base_cart_price": 0.95,
            "cart_tax": 0,
            "base_cart_tax": 0,
            "cart_price_incl_tax": 0.95,
            "base_cart_price_incl_tax": 0.95
          }
        },
        "name": "Simple Product 2"
      }
    ],
    "total_segments": [
      {
        "code": "subtotal",
        "title": "Subtotal",
        "value": 0.95
      },
      {
        "code": "giftwrapping",
        "title": "Gift Wrapping",
        "value": null,
        "extension_attributes": {
          "gw_item_ids": [],
          "gw_price": "0.00",
          "gw_base_price": "0.00",
          "gw_items_price": "0.00",
          "gw_items_base_price": "0.00",
          "gw_card_price": "0.00",
          "gw_card_base_price": "0.00",
          "gw_base_tax_amount": "0.00",
          "gw_tax_amount": "0.00",
          "gw_items_base_tax_amount": "0.00",
          "gw_items_tax_amount": "0.00",
          "gw_card_base_tax_amount": "0.00",
          "gw_card_tax_amount": "0.00",
          "gw_price_incl_tax": "0.00",
          "gw_base_price_incl_tax": "0.00",
          "gw_card_price_incl_tax": "0.00",
          "gw_card_base_price_incl_tax": "0.00",
          "gw_items_price_incl_tax": "0.00",
          "gw_items_base_price_incl_tax": "0.00"
        }
      },
      {
        "code": "shipping",
        "title": "Shipping & Handling (Flat Rate - Fixed)",
        "value": 5
      },
      {
        "code": "tax",
        "title": "Tax",
        "value": 0,
        "extension_attributes": {
          "tax_grandtotal_details": []
        }
      },
      {
        "code": "grand_total",
        "title": "Grand Total",
        "value": 5.95,
        "area": "footer"
      },
      {
        "code": "customerbalance",
        "title": "Store Credit",
        "value": 0
      },
      {
        "code": "reward",
        "title": "0 Reward points",
        "value": 0
      }
    ],
    "extension_attributes": {
      "negotiable_quote_totals": {
        "items_count": 1,
        "quote_status": "submitted_by_admin",
        "created_at": "2017-05-30 20:41:00",
        "updated_at": "2017-06-09 20:26:49",
        "customer_group": 10,
        "base_to_quote_rate": 1,
        "cost_total": 0,
        "base_cost_total": 0,
        "original_total": 0.95,
        "base_original_total": 0.95,
        "original_tax": 0,
        "base_original_tax": 0,
        "original_price_incl_tax": 0.95,
        "base_original_price_incl_tax": 0.95,
        "negotiated_price_type": null,
        "negotiated_price_value": null
      },
      "reward_points_balance": 0,
      "reward_currency_amount": 0,
      "base_reward_currency_amount": 0
    }
  }
}

{% endhighlight %}
{% endcollapsible %}

## 相关信息

* [与NegotiableQuote模块集成]({{ page.baseurl }}/b2b/negotiable-quote.html)
* [管理协商报价]({{ page.baseurl }}/b2b/negotiable-manage.html)
* [更新协商报价]({{ page.baseurl }}/b2b/negotiable-update.html)
* [生成协商报价订单]({{ page.baseurl }}/b2b/negotiable-order-workflow.html)
