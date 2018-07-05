---
group: b2b
subgroup: 10_REST
title: 管理共享类目录
menu_title: 管理共享类目录
menu_order: 22
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: shared
github_link: b2b/shared-cat-manage.md
functional_areas:
  - B2B
  - Catalog
  - Integration
---

## Magento自定义共享产品目录

{{site.data.var.b2b}}提供了两种类型的共享产品目录：公共的和自定义的。公共的共享产品目录就是默认的共享产品目录。它自动展示给所有不是公司用户的游客及登录客户。销售者通过管理面板配置来分配一个自定义的共享产品目录到指定的公司。只能有一个公共产品目录且不能被删除。

**服务名称**

`sharedCatalogSharedCatalogRepositoryV1`

**REST接口**

{% highlight json %}
POST /V1/sharedCatalog
PUT  /V1/sharedCatalog/:id
GET  /V1/sharedCatalog/:sharedCatalogId
DELETE  /V1/sharedCatalog/:sharedCatalogId
GET  /V1/sharedCatalog/
{% endhighlight %}

**共享产品目录参数**

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
`id` | 系统生成的共享产品目录的ID号| integer | 更新共享产品目录时必须 ，创建操作是不可用的
`name` | 此共享产品目录的显示名称，必须唯一 | string | 创建和更新共享产品目录时必需
`description` | 共享产品目录的描述 | string | 可选
`customer_group_id` | 系统生成的ID,不通修改| integer |  0-未登录；1-正常；2-整体销售；3-零售
`type` | 指示是否是自定义共享产品目录，或是公共共享产品目录 | integer | 创建和更新共享产品目录时必需 0 - 自定义; 1 - 公共
`created_by` | The user ID of the admin who created the shared catalog | integer | 可选
`store_id`  | 共享目录分配到的网站ID | integer | 创建和更新共享产品目录时必需
`tax_class_id`  | | integer |  创建共享产品目录时必需。1-应纳税商品。2-零售顾客


### 创建一个自定义的共享产品目录

当启用B2B，系统会创建一个公共的共享产品目录，名字叫`Defalut(General)`。Magento只允许同一时间只有一个公共共享产品目录。你可以创建无限多个自定义共享产品目录。

**样例用法**

`POST /V1/sharedCatalog`

**载荷**

{% highlight json %}
{
  "sharedCatalog": {
    "name": "Test",
    "type": 0,
    "store_id": 0,
    "tax_class_id": 3
  }
}
{% endhighlight %}

**响应**

共享产品目录的`id`,如`2`

### 更新共享产品目录的特点

你不能修改`type`的值，从公共(`1`)改为自定义(`0`),如果你需要替换公共产品目录，可以创建一个自定义共享产品目录并将其类型改为公共的。

**样例用法**

`PUT  /V1/sharedCatalog/2`

{% highlight json %}

{
  "sharedCatalog": {
    "id": 2,
    "name": "Custom shared catalog",
    "description": "Just a sample custom shared catalog.",
    "type": 0,
    "store_id": 0,
    "tax_class_id": 3
  }
}
{% endhighlight %}

**响应**

共享产品目录的`id`,如`2`

### 接收共享产品目录的一般信息

此调用返回指定共享产品目录的信息

**样例用法**

`GET  /V1/sharedCatalog/2`

**载荷**

不适用

**响应**

{% highlight json %}
{
    "id": 2,
    "name": "Custom shared catalog",
    "description": "Just a sample custom shared catalog.",
    "customer_group_id": 4,
    "type": 0,
    "created_at": "2017-07-21 15:39:40",
    "created_by": 1,
    "store_id": 0,
    "tax_class_id": 3
}
{% endhighlight %}

### 删除共享产品目录

仅有自定义的共享产品目录可以被删除，当一个自定义的产品目录被删除时，被分配在此上的公司将被重新分配到公共产品目录中。

**样例用法**

`DELETE  /V1/sharedCatalog/2`

**载荷**

不适用

**响应**

`true`,指示请求成功

### 查找共享产品目录

下面的查询返回了系统中所有的自定义(`type = 0`)目录

参考[使用REST API搜索]({{ page.baseurl }}/rest/performing-searches.html)了解更多关于构造查询的信息

**样例用法**

`GET V1/sharedCatalog?searchCriteria[filter_groups][0][filters][0][field]=type&searchCriteria[filter_groups][0][filters][0][value]=0&searchCriteria[filter_groups][0][filters][0][condition_type]=eq`

**载荷**

不适用

**响应**

{% highlight json %}

{
    "items": [
        {
            "id": 2,
            "name": "Custom shared catalog",
            "description": "Just a sample custom shared catalog.",
            "customer_group_id": 4,
            "type": 0,
            "created_at": "2017-07-21 15:39:40",
            "created_by": 1,
            "store_id": 0,
            "tax_class_id": 3
        }
    ],
    "search_criteria": {
        "filter_groups": [
            {
                "filters": [
                    {
                        "field": "type",
                        "value": "0",
                        "condition_type": "eq"
                    }
                ]
            }
        ]
    },
    "total_count": 1
}

{% endhighlight %}

## 相关信息

* [与ShareCatalog模块集成]({{ page.baseurl }}/b2b/shared-catalog.html)
* [分配分类和产品]({{ page.baseurl }}/b2b/shared-cat-product-assign.html)
* [分配公司]({{ page.baseurl }}/b2b/shared-cat-company.html)
