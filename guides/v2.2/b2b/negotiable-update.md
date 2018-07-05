---
group: b2b
subgroup: 10_REST
title: 更新协商报价
menu_title: 更新协商报价
menu_order: 33
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: nq
github_link: b2b/negotiable-update.md
functional_areas:
  - B2B
  - Integration
---

销售者和购买者可以在其周期中的不同的时间修改议价。可以使用`PUT /V1/negotiableQuote/:quoteId`调用更新报价，此接口定义在`quoteCartRepositoryV1`服务中，其功能与`PUT /V1/carts/mine`调用相似

`quote`对像现在包含一些`negotiable_quote`的扩展属性，它们可以被用于更新报价。

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
`quote_id` | 议价ID | integer | Required to create or update a negotiable quote
`is_regular_quote` | 议价标志 | boolean | 可选
`status` | 可以是`created`, `submitted_by_customer`, `submitted_by_admin`, `processing_by_customer`, `processing_by_admin`, `ordered`, `expired`之一 `declined`, `closed` | string | 可选
`negotiated_price_type` | 1-百分比折扣；2-固定价格；3-提议总价 | integer | 必须设置一个商议的价格
`negotiated_price_value` | 销售者定义的折扣总额 | number | 必须设置一个商议的价格
`shipping_price` | 销售者定义的自定义物流价格 | number | 可选
`quote_name` | 分配给议价名的称 | string | 可选
`expiration_period` | 报价的过期日期，格式必须是`YYYY-MM-DD`. | string | 可选
`email_notification_status`  | 最近已发送的通知 | integer | 可选
`has_unconfirmed_changes`  | 指示管理员现在有还没看到的修改 | boolean | 可选
`is_shipping_tax_changed`  | 指示物流税额是否发生改变 | boolean | 可选
`is_customer_price_changed`  | 指是产品的价格是否发生改变 | boolean | 可选
`notifications`  | 当前通知被保存的二进制掩码 | integer | 可选
`applied_rule_ids`  | 已应用的购物车规则 | string | 可选
`is_address_draft`  | 是否在结算未完成时移除地址 | boolean | 可选
`deleted_sku`  | 被删除产品的sku | string | 可选
`creator_id`  | 报价创建人的ID | integer | 可选
`creator_type`  | 1-集成者；2-管理员；3-客户；4-游客 | integer | 可选
`original_total_price`  | 原始总价 | number | 可选
`base_original_total_price`  | 基础原始总价 | number | 可选
`negotiated_total_price`  | 商议的总价 | number | 可选
`base_negotiated_total_price`  | 基础商议的总价 | number | 可选

### 设置商议的价格

在每一个成功的议价中，销售者必须设置商议价格。

`negotiated_price_type`可以是以面的值之一

`1`- 在报价上应用一个百分比折扣，`negotiated_price_value`参数指示这个百分比。

`2` - 在报价上应用一个固定的折扣价。`negotiated_price_value`参数指定这个折扣价

`3` - 设置整个报价单的提议价，`negotiated_price_value`参数指示这个价格

**服务名称**

`quoteCartRepositoryV1`

**样例用法**

`PUT /V1/negotiableQuote/6`

**载荷**

{% highlight json %}
{
  "quote": {
      "id": 6,
      "extension_attributes": {
        "negotiable_quote": {
         "negotiated_price_type": 1,
          "negotiated_price_value": 5
        }
      }
    }
}
{% endhighlight %}

### 添加一个报价项到议价中

在以下条件下，购买者可以从报价中添加，更新或删除项

* 报价处于以下的系统状态中：`created`, `processing_by_admin`, 或 `submitted_by_customer`.
* 报价还没有商议的价格

**样例用法**

`POST /V1/carts/mine/items`

**载荷**

{% highlight json %}
{
  "cartItem": {
    "sku": "24-MB01",
    "qty": 1,
    "quote_id": "7"
  }
}
{% endhighlight %}

**响应**

{% highlight json %}
{
    "item_id": 18,
    "sku": "24-MB01",
    "qty": 1,
    "name": "Joust Duffle Bag",
    "price": 34,
    "product_type": "simple",
    "quote_id": "7",
    "extension_attributes": {
        "negotiable_quote_item": {
            "item_id": 18,
            "original_price": 34,
            "original_tax_amount": 0,
            "original_discount_amount": 0
        }
    }
}
{% endhighlight %}


### 修改报价的过期日期

**样例用法**

`PUT /V1/negotiableQuote/6`

**载荷**

{% highlight json %}
{
  "quote": {
      "id": 6,
      "extension_attributes": {
        "negotiable_quote": {
         "expiration_period": "2017-09-30"
        }
      }
    }
}
{% endhighlight %}

**响应**

`[]`

## 相关信息

* [与NegotiableQuote模块集成]({{ page.baseurl }}/b2b/negotiable-quote.html)
* [管理协商报价]({{ page.baseurl }}/b2b/negotiable-manage.html)
* [协商报价结算]({{ page.baseurl }}/b2b/negotiable-checkout.html)
* [生成协商报价订单]({{ page.baseurl }}/b2b/negotiable-order-workflow.html)
