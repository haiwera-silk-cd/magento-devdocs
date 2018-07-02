---
group: b2b
subgroup: 10_REST
title: 管理公司信用帐户
menu_title: 管理公司信用帐户
menu_order: 18
level3_menu_node: level3child
level3_subgroup: credit
version: 2.2
ee_only: True
github_link: b2b/credit-manage.md
functional_areas:
  - B2B
  - Integration
---

公司信用实体操作以下属性

* 信用限额
* 可用额度
* 未结余额

信用限额由销售者分配，而可用额度和未结余额由系统基于购买者的交易（确认订单、退货）和销售者的交易（退款、报销、更新信用限额及取消订单）自动计算得出

## 管理公司信用限额

当你创建了一个公司，信用限额会被设为0，使用`PUT /V1/companyCredits/:id`调用来改变这个值并执行公司信用设置的其它更新。

**REST接口**

{% highlight json %}
PUT /V1/companyCredits/:id
GET /V1/companyCredits/:creditId
GET /V1/companyCredits/company/:companyId
GET /V1/companyCredits/
{% endhighlight %}

**公司信用帐户参数**

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
`id` | 系统生成的信用ID| integer | Required
`company_id` | 公司ID| integer | Required
`credit_limit` | 授予公司的信用总额| Number | Required
`balance` | 公司当前欠销售者的总金额| Number | 可选
`currency_code` | 公司信用的货币代码，比如USD| String | Required
`exceed_limit` | 指示公司是否能超过信用限额 | Boolean  | 可选
`available_limit` | 公司当前可用的信用总额 | Number | 可选
`credit_comment` | 描述产生的改变 | String | 可选

### 更新公司信用限额

此调用修改了公司信用额度到$1000. `available_limit`参数是计算出来的，所以你不通指定它的值。

**服务名称**

`companyCreditCreditLimitRepositoryV1`

**样例用法**

`PUT /V1/companyCredits/company/2`

**载荷**

{% highlight json %}
{
  "creditLimit": {
  "id": 2,
  "company_id": 2,
  "credit_limit": 1000,
  "currency_code": "USD"
  }
}
{% endhighlight %}

**响应**

{% highlight json %}
{
    "id": 2,
    "company_id": 2,
    "credit_limit": 1000,
    "balance": 0,
    "currency_code": "USD",
    "exceed_limit": false,
    "available_limit": 1000
}
{% endhighlight %}

### 使用信用ID获取公司信用限额的详情

此调用为指定的信用ID返回信用限额上的数据

**服务名称**

`companyCreditCreditLimitRepositoryV1`

**样例用法**

`GET /V1/companyCredits/2`

**载荷**

不适用

**响应**

{% highlight json %}
{
  "id": 2,
  "company_id": 2,
  "credit_limit": 500,
  "balance": 0,
  "currency_code": "USD",
  "exceed_limit": false,
  "available_limit": 500
}
{% endhighlight %}

### 使用公司ID获取公司信用限额的详情

此调用为指定的公司返回信用限额数据。

**服务名称**

`companyCreditCreditLimitManagementV1`

**样例用法**

`GET /V1/companyCredits/company/2`

**载荷**

不适用

**响应**

{% highlight json %}
{
  "id": 2,
  "company_id": 2,
  "credit_limit": 500,
  "balance": 0,
  "currency_code": "USD",
  "exceed_limit": false,
  "available_limit": 500
}
{% endhighlight %}

### 查找信用ID

以下调用返回所有公司信用余额为0的公司信息

参考[使用REST API搜索]({{ page.baseurl }}/rest/performing-searches.html)了解更多关于构造查询的信息

**样例用法**

`GET  /V1/companyCredits?searchCriteria[filter_groups][0][filters][0][field]=balance&searchCriteria[filter_groups][0][filters][0][value]=0&searchCriteria[filter_groups][0][filters][0][condition_type]=eq`

**载荷**

不适用

**响应**

{% collapsible Show code sample %}
{% highlight json %}
{
    "items": [
        {
            "id": 2,
            "company_id": 2,
            "credit_limit": 1000,
            "balance": 0,
            "currency_code": "USD",
            "exceed_limit": false,
            "available_limit": 1000
        },
        {
            "id": 3,
            "company_id": 3,
            "balance": 0,
            "currency_code": "USD",
            "exceed_limit": false,
            "available_limit": 0
        },
        {
            "id": 4,
            "company_id": 4,
            "credit_limit": 2000,
            "balance": 0,
            "currency_code": "USD",
            "exceed_limit": false,
            "available_limit": 2000
        }
    ],
    "search_criteria": {
        "filter_groups": [
            {
                "filters": [
                    {
                        "field": "balance",
                        "value": "0",
                        "condition_type": "eq"
                    }
                ]
            }
        ]
    },
    "total_count": 3
}
{% endhighlight %}
{% endcollapsible %}

## 余额操作

公司的未结余额可被购买者支付、购买及基它交易动作更新。

**服务名称**

`companyCreditCreditBalanceManagementV1`

**REST接口**

{% highlight json %}
POST /V1/companyCredits/:creditId/decreaseBalance
POST /V1/companyCredits/:creditId/increaseBalance
{% endhighlight %}

**余额参数**

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
`value` | 指示公司信用余额操作涉及的金额数量 | Nuumber | Required
`currency` |交易的货币代码，如USD | String | Required
`operationType` | 必须是以下值之一 1 - 已分配; 2 - 已更新; 3 - 已购买; 4 - 已报销; 5 - 已退款; 6 - 已归还 | Integer | Required
`comment` | 操作描述 | String | 可选
`options` | 一个为增加和减少信用余额提供附加信息的对象 | Object | 可选

**`options`参数**

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
`purchase_order` | 公司购买的订单号  | String | 可选
`order_increment` | Order increment | String | 可选
`currency_display` | 展示操作的货币代码| String | 可选
`currency_base` | 其础货币 | String | 可选

### 增加公司的信用余额

此调用公司的信用随分配、更新、退款、归还或报销事务增长。（你不能指定购买(3)的操作类型）此调用也可以减少公司的未结余额

**样例用法**

`V1/companyCredits/2/increaseBalance`

**载荷**

{% highlight json %}
{
  "value": 250,
  "currency": "USD",
  "operationType": 2,
  "comment": "update limit"
}
{% endhighlight %}

**响应**

`true`，指示增加信用余额成功

### 减少余额

此调用公司的信用随更新(操作类型为2)、购买(3)或报销(4)事务减少。（你不能指定其它的操作类型）此调用也会增加公司的未结余额。

**样例用法**

`V1/companyCredits/2/decreaseBalance`

**载荷**

{% highlight json %}
{
  "value": 250,
  "currency": "USD",
  "operationType": 4,
  "comment": "issue refund"
}
{% endhighlight %}

**响应**

`true`，指示公司信用额减少成功

## 信用额历史

一个报销事务可以被更新来包含一个购买的订单和备注。

**服务名称**
`companyCreditCreditHistoryManagementV1`

**REST接口**
{% highlight json %}
GET /V1/companyCredits/history
PUT /V1/companyCredits/history/:historyId
{% endhighlight %}

### 保存信用额历史

此调用更新食用额历史指定一个购买的订单号

**样例用法**

`PUT /V1/companyCredits/history/6`

**载荷**

{% highlight json %}
{
  "purchaseOrder": "A12345",
  "comment": "Adding PO info"
}
{% endhighlight %}

**响应**

`true`,指示调用成功

### 搜索食用额历史ID

下面的调用返回一个实例列表，它们的限额都被设置为$500以上

参考[使用REST API搜索]({{ page.baseurl }}/rest/performing-searches.html)了解更多关于构造查询的信息


**样例用法**

`GET /V1/companyCredits/history?searchCriteria[filter_groups][0][filters][0][field]=credit_limit&searchCriteria[filter_groups][0][filters][0][value]=500&searchCriteria[filter_groups][0][filters][0][condition_type]=gt`

**载荷**

不适用

**响应**
{% highlight json %}
{
    "items": [
        {
            "id": 6,
            "company_credit_id": 2,
            "user_id": 1,
            "user_type": 2,
            "currency_credit": "USD",
            "currency_operation": "USD",
            "rate": 1,
            "rate_credit": 0,
            "amount": -250,
            "balance": 0,
            "credit_limit": 1000,
            "available_limit": 1000,
            "type": 4,
            "datetime": "2017-06-12 02:26:28",
            "purchase_order": "A12345",
            "comment": "{\"custom\":\"Adding PO info\"}"
        },
        {
            "id": 7,
            "company_credit_id": 4,
            "user_id": 1,
            "user_type": 2,
            "currency_credit": "USD",
            "currency_operation": "USD",
            "rate": 1,
            "rate_credit": 0,
            "amount": 0,
            "balance": 0,
            "credit_limit": 2000,
            "available_limit": 2000,
            "type": 1,
            "datetime": "2017-07-20 21:28:35",
            "comment": ""
        }
    ],
    "search_criteria": {
        "filter_groups": [
            {
                "filters": [
                    {
                        "field": "credit_limit",
                        "value": "500",
                        "condition_type": "gt"
                    }
                ]
            }
        ]
    },
    "total_count": 2
}
{% endhighlight %}

## 相关信息

[与CompanyCredit模块集成]({{ page.baseurl }}/b2b/company-credit.html)
