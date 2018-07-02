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

## Manage custom shared catalogs

{{site.data.var.b2b}} provides two types of shared catalog: public and custom. A public catalog is the default shared catalog. It is automatically displayed to all guest customers and to logged-in customers that are not company users. The seller assigns a custom shared catalog to specific companies as configured by admin. There can only be one public catalog, and it cannot be deleted.

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

**Shared catalog parameters**

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
`id` | The system-generated shared catalog ID number | integer | Required to update a shared catalog. Not applicable for create operations.
`name` | The display name of the shared catalog. Must be unique | string | Required to create or update a shared catalog.
`description` | Describes the shared catalog | string | 可选
`customer_group_id` | A system-generated ID. It cannot be changed. | integer |  0 - Not logged in; 1 - General; 2 - Wholesale; 3 - Retailer
`type` | Indicates whether this is a custom or public shared catalog. | integer | Required to create or update a shared catalog. 0 - Custom; 1 - Public
`created_by` | The user ID of the admin who created the shared catalog | integer | 可选
`store_id`  | The store ID the shared catalog is assigned to | integer | Required to create or update a shared catalog.
`tax_class_id`  | | integer |  Required to create a shared catalog. 2 - Taxable goods; 3 - Retail Customer


### Create a custom shared catalog

When B2B is enabled, the system creates a public shared catalog named `Default (General)`. Magento allows only one public shared catalog at a time. You can create an unlimited number of custom shared catalogs.

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

The shared catalog `id`, such as `2`.

### Update a characteristics of a shared catalog

You cannot change the `type` from public (`1`) to custom (`0`). If you need to replace the public shared catalog, create a custom catalog and change its type to public.

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

The shared catalog `id`, such as `2`.

### Retrieve general information about a shared catalog

This call returns information about the specified shared catalog.

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

### Delete a shared catalog

Only custom shared catalogs can be deleted. When a custom catalog is deleted, the assigned companies are re-assigned to the default public catalog.

**样例用法**

`DELETE  /V1/sharedCatalog/2`

**载荷**

不适用

**响应**

`true`,指示请求成功

### Search for a shared catalog

The following search returns all the custom shared catalogs (`type = 0`) in the system.

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
* [Assign categories and products]({{ page.baseurl }}/b2b/shared-cat-product-assign.html)
* [Assign companies]({{ page.baseurl }}/b2b/shared-cat-company.html)
