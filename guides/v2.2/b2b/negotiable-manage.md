---
group: b2b
subgroup: 10_REST
title: 管理协商报价
menu_title: 管理协商报价
menu_order: 32
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: nq
github_link: b2b/negotiable-manage.md
functional_areas:
  - B2B
  - Integration
---

本节描述启动议价及准备将其转化为订单须要的调用。

<div class="bs-callout bs-callout-info" id="info" markdown="1">
所有的议价调用需要一个管理员授权令牌。
</div>

**REST接口**

{% highlight http %}
POST /V1/negotiableQuote/request
POST /V1/negotiableQuote/submitToCustomer
POST /V1/negotiableQuote/decline
POST /V1/negotiableQuote/pricesUpdated
GET /V1/negotiableQuote/:quoteId/comments
GET /V1/negotiableQuote/attachmentContent
PUT /V1/negotiableQuote/:quoteId/shippingMethod
{% endhighlight %}

**NegotiableQuoteManagementInterface Parameters**

下面的表格列出了`CompanyInterface`的参数定义

名称 | 描述 | 格式 | 要求
--- | --- | --- |---
`quoteId`	| 指操作的目标报价	| integer	| 必需
`quoteName`	| 要创建的报价的名称	| string	| 必需
`comment`	| 添加到报价的说明	| string | 可选
`files` | 添加到报价的文件数组 | array | 可选

购买者或销售者可以选择最多关联10个文件来提供报价的细节。每个文件必须被转为base64

`文件`数组包含下面的参数

名称 | 描述 | 格式 | 要求
--- | --- | --- |---
`base64_encoded_data` | 定义了添加文件内容的base64字符串。| string | 必需
`type` | 定义文件类型，像`text/plain`或`application/pdf`| string | 可选
`name` | 将被上传的文件名，像 `quote.txt`或`quote.pdf`. | string | 必需


### 请求议价

在议价能被开始前，以下的条件必须具备：

* 一个正确的Magento报价已经创建(`POST /V1/customers/:customerId/carts`或`POST /V1/customers/carts/mine`)
* 报价包含了项(`POST /V1/carts/:quoteId/items`)

如果议价需要一个物流地址(为商议和税额计算)，你可以在启动议价前添加它到标准报价中 (`POST /V1/carts/:cartId/shipping-information`)

<div class="bs-callout bs-callout-info" id="info" markdown="1">
请求一个议价需要管理员令牌。
</div>

**服务名称**

`negotiableQuoteNegotiableQuoteManagementV1`

**样例用法**

`POST V1/negotiableQuote/request`

**载荷**

{% highlight json %}
{
  "quoteId": 3,
  "quoteName": "First quote",
  "comment": "Requesting a 5% discount",
  "files": [
    {
      "base64_encoded_data": "VGhhbmsgeW91IGZvciByZWFkaW5nIHRoZSBNYWdlbnRvIEIyQiBkb2N1bWVudGF0aW9uLg==",
      "name": "quote.txt"
    }
  ]
}
{% endhighlight %}

**响应**

`true`,指示请求成功

Magento创建议价为`Created`状态。

### 提交议价到购买者

当你提交一个议价到购买者时，对于购买者此状态改为"Updated"。购买者随后可以编辑和修改这个报价。

销售者可以发送一个请求来提交报价到购买者。请求仅可以在报价是以下系统状态时被提交

* 已创建
* 管理员处理中
* 管理员已提交

当报价被提交到购买者时：

* Magento检查产品目录的价格(每项的价格)，购物车规则及折扣然后重新计算价格和税额。物流价格和商议价格不受影响(如果它们在报价中).
* 对于此购买者不活动或不再有效的项会被从报价中移除并重新计算价格。
* 报价状态改为"管理员已提交"

**服务名称**

`negotiableQuoteNegotiableQuoteManagementV1`

**样例用法**

`POST /V1/negotiableQuote/submitToCustomer`

**载荷**

{% highlight json %}
{
  "quoteId": 3,
  "comment": "It'd be our pleasure. Please proceed with your order."
}
{% endhighlight %}

**响应**

`true`,指示请求成功

### 更新报价

使用`PUT /V1/negotiableQuote/:quoteId`调用来更新报价。参考[更新协商报价]({{ page.baseurl }}/b2b/negotiable-update.html)了解使用方法

### 重新计算价格

完成议价的过程可能要几天或更长时间。在这期间，报价中每项的价格可能会直接或间接地发生变化。例如，有人修改了共享产品目录的价格或调整了价格规则，这样，报价中的价格就不再适用了。此调用更新议价中的项的价格、税额、折扣、购物车规则。锁定的报价对销售者来说是不可更改的。

此请求能在同一时间被应用在一个或多个报价中

**样例用法**

`POST /V1/negotiableQuote/pricesUpdated`

**载荷**

{% highlight json %}
{
  "quoteIds": [3]
}
{% endhighlight %}

**响应**

`true`,指示请求成功

### 设置物流方式

要设置物流方式，报价必须在`created`、`processing_by_admin`或`submitted_by_customer`.状态，此外，报价必须拥有物流地址但没有物流方式和物流价格。

**样例用法**

`PUT /V1/negotiableQuote/3/shippingMethod`

**载荷**

{% highlight json %}
{
  "shippingMethod": "fixedrate"
}
{% endhighlight %}

**响应**


### 拒绝一个报价

销售者可以发送一个请求来拒绝此报价。这个请求仅能在报价在以下状态时被提交：

* 已创建
* 管理员处理中
* 管理员已提交

当你拒绝一个报价时，报价的所有的客户出价将被移除。购买者仍可以使用标准产品目录价格和折扣确认定单。

**服务名称**

`negotiableQuoteNegotiableQuoteManagementV1`

**样例用法**

`POST /V1/negotiableQuote/decline`

**载荷**

{% highlight json %}
{
  "quoteId": 80,
  "reason": "Your order is too large. "
}
{% endhighlight %}

**响应**

`true`,指示请求成功

## 杂项操作

这些工作对完成议价来说不是必要的，但可能有用。

### 列出报价的所有评论信息

Magento列出所有的与指定报价ID相关的评论信息。评论按时间排序，最老的列在最前面。`creator_type`值为3表示是购买者发表的评论；为2表示是销售者发表的。

**样例用法**

`GET /V1/negotiableQuote/87/comments`

**载荷**

不适用

**响应**

{% highlight json %}
[
  {
    "entity_id": 6,
    "parent_id": 87,
    "creator_type": 3,
    "is_decline": 0,
    "is_draft": 0,
    "creator_id": 1,
    "comment": "Requesting a 5% discount",
    "created_at": "2017-06-01 21:14:51",
    "attachments": [
    {
      "attachment_id": 1,
      "comment_id": 12,
      "file_name": "hello.txt",
      "file_path": "/h/e/hello.txt",
      "file_type": null
    }
    ]
  },
  {
    "entity_id": 7,
    "parent_id": 87,
    "creator_type": 2,
    "is_decline": 0,
    "is_draft": 0,
    "creator_id": 1,
    "comment": "We cannot discount Configurable Product 1, because the price is already discounted. We can adjust the overall price so the remaining items are discounted 5%. Please let us know whether this is acceptable. ",
    "created_at": "2017-06-01 21:29:15",
    "attachments": []
  },
  {
    "entity_id": 8,
    "parent_id": 87,
    "creator_type": 3,
    "is_decline": 0,
    "is_draft": 0,
    "creator_id": 1,
    "comment": "That is fine. Please apply the discounts to our order.",
    "created_at": "2017-06-01 21:30:30",
    "attachments": []
  },
  {
    "entity_id": 9,
    "parent_id": 87,
    "creator_type": 2,
    "is_decline": 0,
    "is_draft": 0,
    "creator_id": 1,
    "comment": "We&#039;re taking $27.50 off your quote total. That&#039;s 5% of the cost of the other items in your cart.",
    "created_at": "2017-06-01 21:40:19",
    "attachments": []
  },
  {
    "entity_id": 10,
    "parent_id": 87,
    "creator_type": 3,
    "is_decline": 0,
    "is_draft": 0,
    "creator_id": 1,
    "comment": "Added a shipping address",
    "created_at": "2017-06-01 21:43:03",
    "attachments": []
  },
  {
    "entity_id": 11,
    "parent_id": 87,
    "creator_type": 2,
    "is_decline": 0,
    "is_draft": 0,
    "creator_id": 1,
    "comment": "OK",
    "created_at": "2017-06-01 21:44:16",
    "attachments": []
  }
]
{% endhighlight %}


### 接收议价附件

使用`attachmentContent`调用来接收关联到议价的(base64编码了的)文件。

`negotiableQuoteAttachmentContentManagementV1`

**样例用法**

`GET /V1/negotiableQuote/attachmentContent`

**载荷**

不适用

**响应**

{% highlight json %}
{
  "quoteId": 2,
  "quoteName": "First quote",
  "files": [
    {
      "base64_encoded_data": "VGhhbmsgeW91IGZvciByZWFkaW5nIHRoZSBNYWdlbnRvIEIyQiBkb2N1bWVudGF0aW9uLg==",
      "name": "quote.txt"
    }
  ]
}
{% endhighlight %}
## 相关信息

* [与NegotiableQuote模块集成]({{ page.baseurl }}/b2b/negotiable-quote.html)
* [更新协商报价]({{ page.baseurl }}/b2b/negotiable-update.html)
* [协商报价结算]({{ page.baseurl }}/b2b/negotiable-checkout.html)
* [生成协商报价订单]({{ page.baseurl }}/b2b/negotiable-order-workflow.html)
