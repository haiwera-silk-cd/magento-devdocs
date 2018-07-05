---
group: b2b
subgroup: 10_REST
title: 生成协商报价订单
menu_title: 生成协商报价订单
menu_order: 35
version: 2.2
ee_only: true
level3_menu_node: level3child
level3_subgroup: nq
github_link: b2b/negotiable-order-workflow.md
---

本节描述如何如用REST调用能将产品项放入购物车，启动和完成此议价过程及在收到支付后报销购买者的信用额

## 先决条件

* 你已经[安装并启用了]({{ page.baseurl }}/comp-mgr/install-extensions/b2b-installation.html) {{site.data.var.b2b}}.
* 你已经[创建了一个公司]({{ page.baseurl }}/b2b/company-object.html)及一个[公司用户]({{ page.baseurl }}/b2b/company-object.html).
* 你有一个集成或[管理员授权令牌]({{ page.baseurl }}/get-started/order-tutorial/order-admin-token.html)来发起代表销售者的调用，以及[客户令牌]({{ page.baseurl }}/get-started/order-tutorial/order-create-customer.html#get-token)发起代表公司用户的调用

## 准备定单

本节这些步骤与[使用REST API的订单处理教程]({{ page.baseurl }}/get-started/order-tutorial/order-intro.html)类似，除了不同产品被添加到购物车之外。

### 创建购物车

在本例中，客户是一个公司用户(购买者)

**接口**

`POST /V1/carts/mine`

**请求头**

```
Content-Type application/json
Authorization Bearer <customer token>
```

**载荷**

无

**响应**

响应是`quoteId`,这里是`5`

### 添加产品项

本例添加15个Pursuit Lumaflex Tone Bands和10个 Harmony Lumaflex Strength Band Kits到购物车，你要发起两次调用来添加这些产品。

**接口**

`POST V1/carts/mine`

**请求头**

```
Content-Type application/json
Authorization Bearer <customer token>
```

**载荷 1**
{% highlight json %}
{
  "cartItem": {
    "sku": "24-UG02",
    "qty": 15,
    "quote_id": "5"
  }
}
{% endhighlight %}

**响应1**

{% highlight json %}
{
    "item_id": 12,
    "sku": "24-UG02",
    "qty": 15,
    "name": "Pursuit Lumaflex&trade; Tone Band",
    "price": 16,
    "product_type": "simple",
    "quote_id": "5"
}
{% endhighlight %}

**载荷 2**

{% highlight json %}
{
  "cartItem": {
    "sku": "24-UG03",
    "qty": 10,
    "quote_id": "5"
  }
}
{% endhighlight %}


**响应2**

{% highlight json %}
{
    "item_id": 13,
    "sku": "24-UG03",
    "qty": 10,
    "name": "Harmony Lumaflex&trade; Strength Band Kit ",
    "price": 22,
    "product_type": "simple",
    "quote_id": "5"
}
{% endhighlight %}

### 设置物流地址

你可以在启动议价后决定物流花费，但现在要提供更多最终花费的细节图片给购买者。如果你延后到议价创建之后设置物流地址，请调用`/V1/negotiable-carts/:cartId/estimate-shipping-methods`

**接口**

`POST V1/carts/mine/estimate-shipping-methods`

**请求头**

```
Content-Type application/json
Authorization Bearer <customer token>
```

**载荷**

{% highlight json %}
{  "address": {
      "region": "California",
      "region_id": 12,
      "region_code": "CA",
      "country_id": "US",
      "street": [
        "100 Big Tree Avenue"
        ],
      "postcode": "99999",
      "city": "San Francisco",
      "firstname": "Melanie",
      "lastname": "Shaw",
      "customer_id": 2,
      "email": "mshaw@example.com",
      "telephone": "(415) 555-1212",
      "same_as_billing": 1
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
        "amount": 125,
        "base_amount": 125,
        "available": true,
        "error_message": "",
        "price_excl_tax": 125,
        "price_incl_tax": 125
    },
    {
        "carrier_code": "tablerate",
        "method_code": "bestway",
        "carrier_title": "Best Way",
        "method_title": "Table Rate",
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

你也可以在启动报价后设置物流和帐单信息，使用`POST /V1/negotiable-carts/:cartId/shipping-information`接口.

**接口**

`POST /V1/carts/mine/shipping-information`

**载荷**

{% highlight json %}
{
"addressInformation": {
  "shipping_address": {
  	"region": "California",
    "region_id": 12,
    "region_code": "CA",
    "country_id": "US",
    "street": [
      "100 Big Tree Avenue"
    ],
    "postcode": "99999",
    "city": "San Francisco",
    "firstname": "Melanie",
    "lastname": "Shaw",
    "email": "mshaw@example.com",
    "telephone": "415-555-1212"
  },
  "billing_address": {
  	"region": "California",
    "region_id": 12,
    "region_code": "CA",
    "country_id": "US",
    "street": [
      "100 Big Tree Avenue"
    ],
    "postcode": "99999",
    "city": "San Francisco",
    "firstname": "Melanie",
    "lastname": "Shaw",
    "email": "mshaw@example.com",
    "telephone": "415-555-1212"
  },
  "shipping_carrier_code": "tablerate",
  "shipping_method_code": "bestway"
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
        },
        {
            "code": "companycredit",
            "title": "Payment on Account"
        }
    ],
    "totals": {
        "grand_total": 373,
        "base_grand_total": 373,
        "subtotal": 460,
        "base_subtotal": 460,
        "discount_amount": -92,
        "base_discount_amount": -92,
        "subtotal_with_discount": 368,
        "base_subtotal_with_discount": 368,
        "shipping_amount": 5,
        "base_shipping_amount": 5,
        "shipping_discount_amount": 0,
        "base_shipping_discount_amount": 0,
        "tax_amount": 0,
        "base_tax_amount": 0,
        "weee_tax_applied_amount": null,
        "shipping_tax_amount": 0,
        "base_shipping_tax_amount": 0,
        "subtotal_incl_tax": 460,
        "shipping_incl_tax": 5,
        "base_shipping_incl_tax": 5,
        "base_currency_code": "USD",
        "quote_currency_code": "USD",
        "items_qty": 25,
        "items": [
            {
                "item_id": 12,
                "price": 16,
                "base_price": 16,
                "qty": 15,
                "row_total": 240,
                "base_row_total": 240,
                "row_total_with_discount": 0,
                "tax_amount": 0,
                "base_tax_amount": 0,
                "tax_percent": 0,
                "discount_amount": 48,
                "base_discount_amount": 48,
                "discount_percent": 20,
                "price_incl_tax": 16,
                "base_price_incl_tax": 16,
                "row_total_incl_tax": 240,
                "base_row_total_incl_tax": 240,
                "options": "[]",
                "weee_tax_applied_amount": null,
                "weee_tax_applied": null,
                "name": "Pursuit Lumaflex&trade; Tone Band"
            },
            {
                "item_id": 13,
                "price": 22,
                "base_price": 22,
                "qty": 10,
                "row_total": 220,
                "base_row_total": 220,
                "row_total_with_discount": 0,
                "tax_amount": 0,
                "base_tax_amount": 0,
                "tax_percent": 0,
                "discount_amount": 44,
                "base_discount_amount": 44,
                "discount_percent": 20,
                "price_incl_tax": 22,
                "base_price_incl_tax": 22,
                "row_total_incl_tax": 220,
                "base_row_total_incl_tax": 220,
                "options": "[]",
                "weee_tax_applied_amount": null,
                "weee_tax_applied": null,
                "name": "Harmony Lumaflex&trade; Strength Band Kit "
            }
        ],
        "total_segments": [
            {
                "code": "subtotal",
                "title": "Subtotal",
                "value": 460
            },
            {
                "code": "giftwrapping",
                "title": "Gift Wrapping",
                "value": null,
                "extension_attributes": {
                    "gw_item_ids": [],
                    "gw_price": "0.0000",
                    "gw_base_price": "0.0000",
                    "gw_items_price": "0.0000",
                    "gw_items_base_price": "0.0000",
                    "gw_card_price": "0.0000",
                    "gw_card_base_price": "0.0000"
                }
            },
            {
                "code": "shipping",
                "title": "Shipping & Handling (Best Way - Table Rate)",
                "value": 5
            },
            {
                "code": "discount",
                "title": "Discount",
                "value": -92
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
                "value": 373,
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
            "reward_points_balance": 0,
            "reward_currency_amount": 0,
            "base_reward_currency_amount": 0
        }
    }
}
{% endhighlight %}
{% endcollapsible %}

### 浏览购物车

这是一个可选的步骤，在你开始议价过程之前查看购物车状态

**接口**

`GET /V1/carts/mine`

**请求头**

```
Content-Type application/json
Authorization Bearer <customer token>
```

**载荷**

无

**响应**

{% collapsible Show code sample %}
{% highlight json %}

{
    "id": 5,
    "created_at": "2017-09-14 21:14:15",
    "updated_at": "2017-09-15 16:15:54",
    "is_active": true,
    "is_virtual": false,
    "items": [
        {
            "item_id": 12,
            "sku": "24-UG02",
            "qty": 15,
            "name": "Pursuit Lumaflex&trade; Tone Band",
            "price": 16,
            "product_type": "simple",
            "quote_id": "5"
        },
        {
            "item_id": 13,
            "sku": "24-UG03",
            "qty": 10,
            "name": "Harmony Lumaflex&trade; Strength Band Kit ",
            "price": 22,
            "product_type": "simple",
            "quote_id": "5"
        }
    ],
    "items_count": 2,
    "items_qty": 25,
    "customer": {
        "id": 2,
        "group_id": 1,
        "default_billing": "2",
        "default_shipping": "2",
        "created_at": "2017-09-11 17:55:52",
        "updated_at": "2017-09-14 19:05:40",
        "created_in": "Default Store View",
        "email": "mshaw@example.com",
        "firstname": "Melanie",
        "lastname": "Shaw",
        "gender": 3,
        "store_id": 1,
        "website_id": 1,
        "addresses": [
            {
                "id": 2,
                "customer_id": 2,
                "region": {
                    "region_code": "CA",
                    "region": "California",
                    "region_id": 12
                },
                "region_id": 12,
                "country_id": "US",
                "street": [
                    "100 Big Tree Avenue"
                ],
                "telephone": "(415) 555-1212",
                "postcode": "99999",
                "city": "San Francisco",
                "firstname": "Melanie",
                "lastname": "Shaw",
                "default_shipping": true,
                "default_billing": true
            }
        ],
        "disable_auto_group_change": 0,
        "extension_attributes": {
            "company_attributes": {
                "customer_id": 2,
                "company_id": 1,
                "status": 1
            }
        }
    },
    "billing_address": {
        "id": 12,
        "region": "California",
        "region_id": 12,
        "region_code": "CA",
        "country_id": "US",
        "street": [
            "100 Big Tree Avenue"
        ],
        "telephone": "415-555-1212",
        "postcode": "99999",
        "city": "San Francisco",
        "firstname": "Melanie",
        "lastname": "Shaw",
        "customer_id": 2,
        "email": "mshaw@example.com",
        "same_as_billing": 0,
        "save_in_address_book": 0
    },
    "orig_order_id": 0,
    "currency": {
        "global_currency_code": "USD",
        "base_currency_code": "USD",
        "store_currency_code": "USD",
        "quote_currency_code": "USD",
        "store_to_base_rate": 0,
        "store_to_quote_rate": 0,
        "base_to_global_rate": 1,
        "base_to_quote_rate": 1
    },
    "customer_is_guest": false,
    "customer_note_notify": true,
    "customer_tax_class_id": 3,
    "store_id": 1,
    "extension_attributes": {
        "shipping_assignments": [
            {
                "shipping": {
                    "address": {
                        "id": 13,
                        "region": "California",
                        "region_id": 12,
                        "region_code": "CA",
                        "country_id": "US",
                        "street": [
                            "100 Big Tree Avenue"
                        ],
                        "telephone": "415-555-1212",
                        "postcode": "99999",
                        "city": "San Francisco",
                        "firstname": "Melanie",
                        "lastname": "Shaw",
                        "customer_id": 2,
                        "email": "mshaw@example.com",
                        "same_as_billing": 0,
                        "save_in_address_book": 0
                    },
                    "method": "tablerate_bestway"
                },
                "items": [
                    {
                        "item_id": 12,
                        "sku": "24-UG02",
                        "qty": 15,
                        "name": "Pursuit Lumaflex&trade; Tone Band",
                        "price": 16,
                        "product_type": "simple",
                        "quote_id": "5"
                    },
                    {
                        "item_id": 13,
                        "sku": "24-UG03",
                        "qty": 10,
                        "name": "Harmony Lumaflex&trade; Strength Band Kit ",
                        "price": 22,
                        "product_type": "simple",
                        "quote_id": "5"
                    }
                ]
            }
        ],
        "negotiable_quote": {
            "quote_id": null,
            "is_regular_quote": null,
            "status": null,
            "negotiated_price_type": null,
            "negotiated_price_value": null,
            "shipping_price": null,
            "quote_name": null,
            "expiration_period": null,
            "email_notification_status": null,
            "has_unconfirmed_changes": null,
            "is_shipping_tax_changed": null,
            "is_customer_price_changed": null,
            "notifications": null,
            "applied_rule_ids": null,
            "is_address_draft": null,
            "deleted_sku": null,
            "creator_id": null,
            "creator_type": null
        }
    }
}

{% endhighlight %}
{% endcollapsible %}


## 完成议价

在本例中，购买者请求一个可商议的报价单。销售者应用折扣到报价单上并将其返回给购买者。购买者接受折扣并完成此订单。

<div class="bs-callout bs-callout-info" id="info" markdown="1">
所有的议价调用需要一个管理员授权令牌。
</div>

### 启动议价

在本例中，购买者启动议价，请求2.5%的折扣。

启动议价其状态为`processing_by_admin`

**接口**

`POST V1/negotiableQuote/request`

**请求头**

```
Content-Type application/json
Authorization Bearer <admin token>
```

**载荷**

{% highlight json %}
{
  "quoteId": 5,
  "quoteName": "Discount request",
  "comment": "Requesting a 2.5% discount"
}
{% endhighlight %}

**响应**

`true`

### 调整议价

销售者接受购买者的2.5%折扣的请求。`negotiated_price_type`状态的值为`1`指示是一个百分比的折扣。

**请求头**

```
Content-Type application/json
Authorization Bearer <admin token>
```

**接口**

`PUT /V1/negotiableQuote/5`

**载荷**

{% highlight json %}
{
  "quote": {
      "id": 5,
      "extension_attributes": {
        "negotiable_quote": {
         "negotiated_price_type": 1,
          "negotiated_price_value": 2.5
        }
      }
    }
}
{% endhighlight %}

**响应**

`[]`

### 返回议价给购买者

现在销售者已经更新了报价，它必须被返回到购买者。购买者然后能接受此提议并开始结算过程，也能请求更进一步的议价。

此调用报价会置为`submitted_by_admin`状态

**请求头**

```
Content-Type application/json
Authorization Bearer <admin token>
```

**接口**

`POST /V1/negotiableQuote/submitToCustomer`

**载荷**

{% highlight json %}
{
  "quoteId": 5,
  "comment": "We have applied a 2.5% discount to your order."
}
{% endhighlight %}

**响应**

`true`

### 获取新的价格的报价

每一项的价格都已经减少了2.5个百份点，此外响应中的`negotiable_quote`里的值已经被更新

**请求头**

```
Content-Type application/json
Authorization Bearer <admin token>
```

**接口**

`GET` /V1/carts/5

**载荷**

无

**响应**

{% collapsible Show code sample %}
{% highlight json %}

{
    "id": 4,
    "created_at": "2017-09-14 20:30:38",
    "updated_at": "2017-09-14 20:46:20",
    "is_active": true,
    "is_virtual": false,
    "items": [
        {
            "item_id": 10,
            "sku": "24-UG02",
            "qty": 15,
            "name": "Pursuit Lumaflex&trade; Tone Band",
            "price": 12.48,
            "product_type": "simple",
            "quote_id": "4",
            "extension_attributes": {
                "negotiable_quote_item": {
                    "item_id": 10,
                    "original_price": 16,
                    "original_tax_amount": 0,
                    "original_discount_amount": 3.2
                }
            }
        },
        {
            "item_id": 11,
            "sku": "24-UG03",
            "qty": 10,
            "name": "Harmony Lumaflex&trade; Strength Band Kit ",
            "price": 17.16,
            "product_type": "simple",
            "quote_id": "4",
            "extension_attributes": {
                "negotiable_quote_item": {
                    "item_id": 11,
                    "original_price": 22,
                    "original_tax_amount": 0,
                    "original_discount_amount": 4.4
                }
            }
        }
    ],
    "items_count": 2,
    "items_qty": 25,
    "customer": {
        "id": 2,
        "group_id": 1,
        "default_billing": "2",
        "default_shipping": "2",
        "created_at": "2017-09-11 17:55:52",
        "updated_at": "2017-09-14 19:05:40",
        "created_in": "Default Store View",
        "email": "mshaw@example.com",
        "firstname": "Melanie",
        "lastname": "Shaw",
        "gender": 3,
        "store_id": 1,
        "website_id": 1,
        "addresses": [
            {
                "id": 2,
                "customer_id": 2,
                "region": {
                    "region_code": "CA",
                    "region": "California",
                    "region_id": 12
                },
                "region_id": 12,
                "country_id": "US",
                "street": [
                    "100 Big Tree Avenue"
                ],
                "telephone": "(415) 555-1212",
                "postcode": "99999",
                "city": "San Francisco",
                "firstname": "Melanie",
                "lastname": "Shaw",
                "default_shipping": true,
                "default_billing": true
            }
        ],
        "disable_auto_group_change": 0,
        "extension_attributes": {
            "company_attributes": {
                "customer_id": 2,
                "company_id": 1,
                "status": 1
            }
        }
    },
    "billing_address": {
        "id": 7,
        "region": null,
        "region_id": null,
        "region_code": null,
        "country_id": null,
        "street": [
            ""
        ],
        "telephone": null,
        "postcode": null,
        "city": null,
        "firstname": null,
        "lastname": null,
        "customer_id": 2,
        "email": "mshaw@example.com",
        "same_as_billing": 0,
        "save_in_address_book": 0
    },
    "orig_order_id": 0,
    "currency": {
        "global_currency_code": "USD",
        "base_currency_code": "USD",
        "store_currency_code": "USD",
        "quote_currency_code": "USD",
        "store_to_base_rate": 0,
        "store_to_quote_rate": 0,
        "base_to_global_rate": 1,
        "base_to_quote_rate": 1
    },
    "customer_is_guest": false,
    "customer_note_notify": true,
    "customer_tax_class_id": 3,
    "store_id": 1,
    "extension_attributes": {
        "shipping_assignments": [
            {
                "shipping": {
                    "address": {
                        "id": 8,
                        "region": null,
                        "region_id": null,
                        "region_code": null,
                        "country_id": null,
                        "street": [
                            ""
                        ],
                        "telephone": null,
                        "postcode": null,
                        "city": null,
                        "firstname": null,
                        "lastname": null,
                        "customer_id": 2,
                        "email": "mshaw@example.com",
                        "same_as_billing": 1,
                        "save_in_address_book": 0
                    },
                    "method": null
                },
                "items": [
                    {
                        "item_id": 10,
                        "sku": "24-UG02",
                        "qty": 15,
                        "name": "Pursuit Lumaflex&trade; Tone Band",
                        "price": 12.48,
                        "product_type": "simple",
                        "quote_id": "4",
                        "extension_attributes": {
                            "negotiable_quote_item": {
                                "item_id": 10,
                                "original_price": 16,
                                "original_tax_amount": 0,
                                "original_discount_amount": 3.2
                            }
                        }
                    },
                    {
                        "item_id": 11,
                        "sku": "24-UG03",
                        "qty": 10,
                        "name": "Harmony Lumaflex&trade; Strength Band Kit ",
                        "price": 17.16,
                        "product_type": "simple",
                        "quote_id": "4",
                        "extension_attributes": {
                            "negotiable_quote_item": {
                                "item_id": 11,
                                "original_price": 22,
                                "original_tax_amount": 0,
                                "original_discount_amount": 4.4
                            }
                        }
                    }
                ]
            }
        ],
        "negotiable_quote": {
            "quote_id": 4,
            "is_regular_quote": true,
            "status": "processing_by_admin",
            "negotiated_price_type": 1,
            "negotiated_price_value": 2.5,
            "shipping_price": null,
            "quote_name": "Discount request",
            "expiration_period": null,
            "email_notification_status": 0,
            "has_unconfirmed_changes": false,
            "is_shipping_tax_changed": false,
            "is_customer_price_changed": false,
            "notifications": null,
            "applied_rule_ids": "2,3",
            "is_address_draft": false,
            "deleted_sku": null,
            "creator_id": 1,
            "creator_type": 2,
            "original_total_price": 368,
            "base_original_total_price": 368,
            "negotiated_total_price": 358.8,
            "base_negotiated_total_price": 358.8
        }
    }
}

{% endhighlight %}
{% endcollapsible %}

### 设置支付信息并确认订单

购买者现在已经完成了购买。因为购买者已经指定了账单地址，只有`paymentMethod`信息必须要被包含：

**请求头**

```
Content-Type application/json
Authorization Bearer <admin token>
```

**接口**

`/V1/negotiable-carts/3/payment-information`

**载荷**

{% highlight json %}
{  "paymentMethod": {
    "po_number": "12345",
    "method": "companycredit"
  }
}
{% endhighlight %}

**响应**

响应是订单`id`: `4`

## 报销公司信用额

现在，议价已经被转化为了订单，你以和标准B2C订单一样的方式为其可以发布发票及创建物流。然而，当公司支付了订单，公司的未结余额必须在授信额之内。

在本例中，`companyId`是`1`.

**请求头**

```
Content-Type application/json
Authorization Bearer <admin token>
```


**接口**

`POST /V1/companyCredits/1/increaseBalance`

**载荷**

{% highlight json %}
{
  "value": 363.80,
  "currency": "USD",
  "operationType": 4,
  "comment": "Order #3 reimbursed"
}
{% endhighlight %}

**响应**

`true`,指示报销成功应用，Magento会发送邮件到购买者。

## 相关信息

* [使用REST API的订单处理教程]({{ page.baseurl }}/get-started/order-tutorial/order-intro.html)
* [与NegotiableQuote模块集成]({{ page.baseurl }}/b2b/negotiable-quote.html)
* [管理协商报价]({{ page.baseurl }}/b2b/negotiable-manage.html)
* [更新协商报价]({{ page.baseurl }}/b2b/negotiable-update.html)
* [协商报价结算]({{ page.baseurl }}/b2b/negotiable-checkout.html)
