---
group: b2b
subgroup: 10_REST
title: 管理公司对像
menu_title: 管理公司对像
menu_order: 12
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: company
github_link: b2b/company-object.md
functional_areas:
  - B2B
  - Integration
---


## 管理公司对像

本节描述用于管理`Company`对象的REST接口

**服务名称**

`companyCompanyRepositoryV1`

**REST接口**

{% highlight json %}
POST /V1/company/
PUT /V1/company/:companyId
GET /V1/company/:companyId
DELETE /V1/company/:companyId
GET /V1/company/
{% endhighlight %}

**CompanyInterface 参数**

下面的表格列出了`CompanyInterface`的参数定义

<table>
<tr>
<th>名称</th><th>描述</th><th>格式</th><th>要求</th></tr>
<tr>
<td><code>id</code></td><td>系统生成的公司ID </td><td>integer </td><td>更新和删除时需要</td></tr>
<tr>
<td><code>status</code></td><td>0 - 待审核<br>1 - 已审核<br>2 - 已拒绝<br>3 - Blocked </td><td>integer </td><td>可选</td></tr>
<tr>
<td><code>company_name </code></td><td>公司名称</td><td>string </td><td>创建和更新公司时需要</td></tr>
<tr>
<td><code>legal_name </code></td><td>法人名字 </td><td>string </td><td>可选</td></tr>
<tr>
<td><code>company_email </code></td><td>公司官方邮箱地址，不一定要唯一</td><td>string</td><td>更新和创建公司时需要</td></tr>
<tr>
<td><code>vat_tax_id </code></td><td>公司的增值税号</td><td>string </td><td>可选</td></tr>
<tr>
<td><code>reseller_id </code></td><td>公司分销商的唯一ID</td><td>string </td><td>可选</td></tr>
<tr>
<td><code>comment </code></td><td>公司的更多细节信息</td><td>string</td><td>可选</td></tr>
<tr>
<td><code>street</code></td><td>公司注册的街道地址，可以包含一行或两行。/td><td>Array[string]</td><td>更新和创建公司时需要</td></tr>
<tr>
<td><code>city</code></td><td>公司所在城市</td><td>string </td><td>更新和创建公司时需要</td></tr>
<tr>
<td><code>country_id</code></td><td>公司注册的国家</td><td>string </td><td>创建和更新公司时需要</td></tr>
<tr>
<td><code>region</code></td><td>州或省</td><td>string</td><td>更新和创建公司时需要</td></tr>
<tr>
<td><code>region_id</code></td><td>分配给州或省的ID</td><td>string </td><td>可选</td></tr>
<tr>
<td><code>postcode</code></td><td>公司的邮政编码</td><td>string </td><td>更新和创建公司时需要</td></tr>
<tr>
<td><code>telephone</code></td><td>公司的联系电话</td><td>string</td><td>更新和创建公司时需要</td></tr>
<tr>
<td><code>customer_group_id </code></td><td>定义公司的共享产品目录。值`1`分配给默认共享产品目录</td><td>integer</td><td>更新和创建公司时需要</td></tr>
<tr>
<td><code>sales_representative_id</code></td><td>公司销售代表的用户ID</td><td>integer</td><td>可选</td></tr>
<tr>
<td><code>reject_reason</code></td><td>指定为什么公司请求成为B2B客户被拒</td><td>string</td><td>可选</td></tr>
<tr>
<td><code>rejected_at</code></td><td>指示公司被拒的时间截</td><td>string</td><td>可选</td></tr>
<tr>
<td><code>super_user_id</code></td><td>公司管理员的`customer_id`，当创建一个公司时，`customer_id`必须已经存在</td><td>integer</td><td>更新和创建公司时需要</td></tr>
</table>


### 创建一个公司

以下是创建公司并分配默认共享产品目录(`customer_group_id`)的一个例子。此公司管理员(`super_user_id`)必须是先前定义的一个`customer_id`

**样例用法**

`POST /V1/company/`

**载荷**

{% highlight json %}
{
  "company": {
    "company_name": "Test company",
    "company_email": "newemail@example.com",
    "street":[
    "100 Big Tree Avenue"
    ],
    "city": "San Francisco",
    "country_id": "US",
    "region": "CA",
    "region_id": "12",
    "postcode": "99999",
    "telephone": "4155551212",
    "super_user_id": 5,
    "customer_group_id": 1
  }
}

{% endhighlight %}

**响应**

{% highlight json %}
{
  "id": 2,
  "company_name": "Test company",
  "company_email": "newemail@example.com",
  "street": [
    "100 Big Tree Avenue"
  ],
  "city": "San Francisco",
  "country_id": "US",
  "region": "California",
  "region_id": "12",
  "postcode": "99999",
  "telephone": "4155551212",
  "customer_group_id": 1,
  "sales_representative_id": 1,
  "reject_reason": null,
  "rejected_at": null,
  "super_user_id": 5,
  "extension_attributes": {
    "quote_config": {
      "company_id": "2",
      "is_quote_enabled": false
    }
  }
}
{% endhighlight %}

### 更新公司

下面的调用改变了公司的状态到拒绝状态(`2`),并解释了原因

**样例用法**

`PUT /V1/company/2`

**载荷**

{% highlight json %}
{
  "company": {
  	"id": 2,
  	"company_name": "Test company",
    "company_email": "newemail@example.com",
    "customer_group_id": 1,
        "street":[
    "100 Big Tree Avenue"
    ],
    "city": "San Francisco",
    "country_id": "US",
    "region": "CA",
    "region_id": "12",
    "postcode": "99999",
    "telephone": "4155551212",
    "super_user_id": 5,
    "status": 2,
    "reject_reason": "Failed background check."

  }
}
{% endhighlight %}

**响应**

{% highlight json %}
{
  "id": 2,
  "company_name": "Test company",
  "company_email": "newemail@example.com",
  "street": [
    "100 Big Tree Avenue"
  ],
  "city": "San Francisco",
  "country_id": "US",
  "region": "California",
  "region_id": "12",
  "postcode": "99999",
  "telephone": "4155551212",
  "customer_group_id": 1,
  "sales_representative_id": 1,
  "reject_reason": null,
  "rejected_at": null,
  "super_user_id": 5,
  "extension_attributes": {
    "quote_config": {
      "company_id": "2",
      "is_quote_enabled": true
    }
  }
}
{% endhighlight %}

### 返回公司的所有信息

此调用返回了指定公司的详细信息
**样例用法**

`GET /V1/company/2`

**载荷**

无

**响应**

{% highlight json %}
{
  "id": 2,
  "status": 0,
  "company_name": "Test company",
  "company_email": "newemail@example.com",
  "street": [
    "100 Big Tree Avenue"
  ],
  "city": "San Francisco",
  "country_id": "US",
  "region": "California",
  "region_id": "12",
  "postcode": "99999",
  "telephone": "4155551212",
  "customer_group_id": 1,
  "sales_representative_id": 1,
  "reject_reason": null,
  "rejected_at": null,
  "super_user_id": 5,
  "extension_attributes": {
    "quote_config": {
      "company_id": "2",
      "is_quote_enabled": true
    }
  }
}
{% endhighlight %}


### 删除公司

当你删除一个公司，Magento分配"不活动"状态给所有的公司成员。系统也将从所有公司成员的客户信息中移除公司ID

**样例用法**

`DELETE /V1/company/2`

**载荷**

无

**响应**

`true`,指示请求成功

### 搜索公司

下面的调用返回所有位于加利福尼亚的公司(`region_id` = `12`)

参考[使用REST API搜索]({{ page.baseurl }}/rest/performing-searches.html)了解更多关于构造查询的信息

**样例用法**

`GET /V1/company?searchCriteria[filter_groups][0][filters][0][field]=region_id&searchCriteria[filter_groups][0][filters][0][value]=12&searchCriteria[filter_groups][0][filters][0][condition_type]=eq`

**载荷**

无

**响应**

{% collapsible 查看代码示例 %}
{% highlight json %}
{
    "items": [
        {
            "id": 2,
            "status": 1,
            "company_name": "Test Company",
            "legal_name": "Test Company",
            "company_email": "newemail@example.com",
            "street": [
                "100 Big Tree Avenue"
            ],
            "city": "San Francisco",
            "country_id": "US",
            "region": "California",
            "region_id": "12",
            "postcode": "99999",
            "telephone": "4155551212",
            "customer_group_id": 1,
            "sales_representative_id": 1,
            "reject_reason": null,
            "rejected_at": null,
            "super_user_id": 3,
            "extension_attributes": {
                "applicable_payment_method": 0,
                "available_payment_methods": "banktransfer,cashondelivery,checkmo,payflowpro,payflow_advanced,payflow_link,braintree,cybersource,eway,authorizenet_directpost,free,braintree_paypal,paypal_billing_agreement,payflow_express_bml,paypal_express_bml,paypal_express,payflow_express,hosted_pro,worldpay,companycredit,purchaseorder,braintree_paypal_vault,braintree_cc_vault,payflowpro_cc_vault",
                "use_config_settings": 1,
                "quote_config": {
                    "is_quote_enabled": true
                }
            }
        },
        {
            "id": 3,
            "status": 1,
            "company_name": "Widgets, Inc",
            "legal_name": "Widgets, Inc",
            "company_email": "widgetsinc@example.com",
            "street": [
                "8383 Wilshire Blvd",
                "Ste 1500"
            ],
            "city": "Beverly Hills",
            "country_id": "US",
            "region": "California",
            "region_id": "12",
            "postcode": "90211",
            "telephone": "(310) 555-0000",
            "customer_group_id": 1,
            "sales_representative_id": 1,
            "reject_reason": null,
            "rejected_at": null,
            "super_user_id": 10,
            "extension_attributes": {
                "applicable_payment_method": 0,
                "available_payment_methods": "banktransfer,cashondelivery,checkmo,payflowpro,payflow_advanced,payflow_link,braintree,cybersource,eway,authorizenet_directpost,free,braintree_paypal,paypal_billing_agreement,payflow_express_bml,paypal_express_bml,paypal_express,payflow_express,hosted_pro,worldpay,companycredit,purchaseorder,braintree_paypal_vault,braintree_cc_vault,payflowpro_cc_vault",
                "use_config_settings": 1,
                "quote_config": {
                    "is_quote_enabled": true
                }
            }
        }
    ],
    "search_criteria": {
        "filter_groups": [
            {
                "filters": [
                    {
                        "field": "region_id",
                        "value": "12",
                        "condition_type": "eq"
                    }
                ]
            }
        ]
    },
    "total_count": 2
}
{% endhighlight %}
{% endcollapsible %}

## 相关信息

* [集成公司模块]({{ page.baseurl }}/b2b/company.html)
* [管理公司用户]({{ page.baseurl }}/b2b/company-users.html)
* [管理公司角色]({{ page.baseurl }}/b2b/roles.html)
* [管理公司结构]({{ page.baseurl }}/b2b/company-structures.html)
