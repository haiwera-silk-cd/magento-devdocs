---
group: b2b
subgroup: 10_REST
title: 分配公司到共享类目录
menu_title: 分配公司
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

一个共享产品目录在它能被公司用户访问之前必须被分配到一个或多个公司

**服务名称**

`sharedCatalogCompanyManagementV1`


**REST接口**

{% highlight json %}
POST /V1/sharedCatalog/:sharedCatalogId/assignCompanies
POST /V1/sharedCatalog/:sharedCatalogId/unassignCompanies
GET  /V1/sharedCatalog/:sharedCatalogId/companies
{% endhighlight %}

**Company parameters**

<div class="bs-callout bs-callout-info" id="info" markdown="1">
虽然你可以指定其它在`categories`对象中定义的参数，但`id`是唯一用于绑定或解绑分类到共享产品目录的参数。
</div>

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
`id` | 公司ID号 | integer | 绑定或解绑一个公司到到一个共享目录时必须

## 分配(绑定)分类和共享产品目录

此动作类似于更新方式的工作。它不会替换已经分配的公司

如果指定的公司已经关联了一个不同的共享产品目录，此调求会解绑先前的产品目录并分配新的。

**示例用法**

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

`true`, 指示操作成功

## 从共享产品目录中解绑分类

当你从一个自定义的产品目录解绑公司时，系统自动分配公司到公共共享产品目录，你不能从公共产品目录解绑公司。

**示例用法**

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

`true`, 指示操作成功

## 列出共享产品目录的公司

`GET`调用返回一个公司ID的数组。

**样例用法**

`GET  /V1/sharedCatalog/2/companies`

**载荷**

不适用

**响应**

`"[\"1\",\"2\"]"`

## 相关信息

* [与ShareCatalog模块集成]({{ page.baseurl }}/b2b/shared-catalog.html)
* [管理共享类目录]({{ page.baseurl }}/b2b/shared-cat-manage.html)
* [分配分类和产品]({{ page.baseurl }}/b2b/shared-cat-product-assign.html)
