---
group: b2b
subgroup: 10_REST
title: 管理公司用户
menu_title: 管理公司用户
menu_order: 13
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: company
github_link: b2b/company-users.md
functional_areas:
  - B2B
  - Integration
---

公司用户是一个被分配额外的指示用户所属公司属性的客户(购买者)。使用`POST /V1/customers`调用，此调用在{{site.data.var.ce}}和{{site.data.var.ee}}中都有，并指定`company_attributes`扩展属性来创建公司用户。

<div class="bs-callout bs-callout-info" id="info" markdown="1">
本节仅论讨B2B指定的`customerCustomerRepositoryV1`服务的特性。参考[创建一个客户]({{ page.baseurl }}/get-started/order-tutorial/order-create-customer.html)了解创建一个标准客户的例子。
</div>

## 管理公司用户

本节描述用于管理公司用户的REST接口

**服务名称**

`customerCustomerRepositoryV1`

**REST接口**

{% highlight json %}
POST /V1/customers/
PUT /V1/customers/:customerId
{% endhighlight %}

** 公司用户的参数 **

下面的表格列出了能被用于创建公司客户的参数

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
`customer_id` | 系统生成的客户ID | integer | 创建操作不可用
`company_id` | 系统生成的公司的ID | integer | 创建和更新公司用户时必须
`job_title` | 描述公司用户职责的一个字符串 | 更新和创建公司时必须
`status` | 指示是否公司用户是活动的 | integer | `0` - 不活动的; `1` - 活动的
`telephone`  |  电话号码 | string | 创建公司用户时必须

### 创建一个公司用户

`POST /V1/customers`调用创建一个Magento的客户。B2B扩展`customerAccountManagementV1`服务以使你可以创建公司用户

**样例用法**

`POST /V1/customers`

**载荷**

添加`company_attributes`代码块到创建一个标准用户所需参数的载荷中

{% highlight json %}

"extension_attributes": {
   "company_attributes": {
   "company_id": 2,
   "status": 1,
   "job_title": "Sales Rep",
   "telephone": "512-555-3322"
   }
}
{% endhighlight %}

完整版:

{% highlight json %}
{
	"customer": {
		"email": "mshaw@example.com",
		"firstname": "Melanie",
		"lastname": "Shaw",
		"extension_attributes": {
    		"company_attributes": {
    		"company_id": 2,
    		"status": 1,
    		"job_title": "Sales Rep",
    		"telephone": "512-555-3322"
    		}
		}
	}
}
{% endhighlight %}

**响应**

{% highlight json %}
{
  "id": 13,
  "group_id": 1,
  "created_at": "2017-05-18 16:47:44",
  "updated_at": "2017-05-18 16:47:44",
  "created_in": "Default Store View",
  "email": "mshaw@example.com",
  "firstname": "Melanie",
  "lastname": "Shaw",
  "store_id": 1,
  "website_id": 1,
  "addresses": [],
  "disable_auto_group_change": 0,
  "extension_attributes": {
    "company_attributes": {
      "customer_id": 13,
      "company_id": 2,
      "job_title": "Sales Rep",
      "status": 1,
      "telephone": "512-555-3322"
    }
  }
}
{% endhighlight %}

### 修改公司用户

下面的例子修改公司用户的状态到不活动。

如果你修改状态到不活动，此帐户是锁定的，如果此公司用户有子用户，系统重新分配其子用户到被操作用户的父用户上。


**样例用法**

`PUT /V1/customers/13`

**载荷**

{% highlight json %}
{
  "customer": {
    "id": 13,
    "email": "mshaw@example.com",
    "firstname": "Melanie",
    "lastname": "Shaw",
    "website_id": 1,
    "extension_attributes": {
      "company_attributes": {
        "company_id": 2,
        "status": 0
        }
      }
  }
}
{% endhighlight %}

**响应**

{% highlight json %}
{
  "id": 13,
  "group_id": 1,
  "created_at": "2017-05-18 16:47:44",
  "updated_at": "2017-05-18 18:50:58",
  "created_in": "Default Store View",
  "email": "mshaw@example.com",
  "firstname": "Melanie",
  "lastname": "Shaw",
  "store_id": 1,
  "website_id": 1,
  "addresses": [],
  "disable_auto_group_change": 0,
  "extension_attributes": {
    "company_attributes": {
      "customer_id": 13,
      "company_id": 2,
      "status": 0
    }
  }
}
{% endhighlight %}

### 删除公司用户

如果指定公司用户有子用户，系统重新分配其子用户到被删用户的父用户。此用帐的帐号及其所有内容将从Magento上删除，除了报价和订单。此用户的订单和报价信息对销售者仍可见。

Magento锁定删除用户的报价并修改它们为关闭。系统不允许修改这类的报价。

**样例用法**

`DELETE /V1/customers/13`

**载荷**

不适用

**响应**

`true`,指示请求成功

## 相关信息

* [集成公司模块]({{ page.baseurl }}/b2b/company.html)
* [管理公司对像]({{ page.baseurl }}/b2b/company-object.html)
* [管理公司角色]({{ page.baseurl }}/b2b/roles.html)
* [管理公司结构]({{ page.baseurl }}/b2b/company-structures.html)
