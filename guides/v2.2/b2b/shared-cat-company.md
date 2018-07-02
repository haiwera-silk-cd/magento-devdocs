---
group: b2b
subgroup: 10_REST
title: 分配公司到共享类目录
menu_title: Assign companies
menu_order: 24
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: shared
github_link: b2b/shared-cat-company.md
functional_areas:
  - B2B
  - Catalog
  - Integration
---

A shared catalog must be assigned to one or more companies before it can be accessed by the company users.

**服务名称**

`sharedCatalogCompanyManagementV1`


**REST endpoints**

{% highlight json %}
POST /V1/sharedCatalog/:sharedCatalogId/assignCompanies
POST /V1/sharedCatalog/:sharedCatalogId/unassignCompanies
GET  /V1/sharedCatalog/:sharedCatalogId/companies
{% endhighlight %}

**Company parameters**

<div class="bs-callout bs-callout-info" id="info" markdown="1">
Although you can specify other parameters defined within a `categories` object, the `id` is the only one used to assign or unassign a category to a shared catalog.
</div>

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
`id` | The company ID number | integer | Required to assign or unassign a company to a shared catalog

## Assign categories to shared catalog

This action works as an update. It does not replace companies that have already been assigned.

If a specified company is already assigned to a different shared catalog, this request unassigns the company from the previous catalog and assigns to the new one.

**Sample usage**

`POST /V1/sharedCatalog/2/assignCompanies`

**载荷**

{% highlight json %}

{
  "companies": [
    {
      "id": 1
    },
    {
      "id": 2
    }
  ]
}
{% endhighlight %}

**响应**

`true`, indicating the operation was successful

## Unassign categories from a shared catalog

When you unassign a company from a custom catalog, the system automatically assigns this company to the public shared catalog. You cannot unassign a company from the public catalog.

**Sample usage**

`POST /V1/sharedCatalog/2/unassignCompanies`

**载荷**

{% highlight json %}
{
  "companies": [
    {
      "id": 2
    }
  ]
}
{% endhighlight %}

**响应**

`true`, indicating the operation was successful

## List the shared catalog companies

The `GET` call returns an array of company IDs.

**样例用法**

`GET  /V1/sharedCatalog/2/companies`

**载荷**

不适用

**响应**

`"[\"1\",\"2\"]"`

## 相关信息

* [与ShareCatalog模块集成]({{ page.baseurl }}/b2b/shared-catalog.html)
* [管理共享类目录]({{ page.baseurl }}/b2b/shared-cat-manage.html)
* [Assign categories and products]({{ page.baseurl }}/b2b/shared-cat-product-assign.html)
