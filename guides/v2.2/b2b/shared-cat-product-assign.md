---
group: b2b
subgroup: 10_REST
title: 分配分类和产品到类目录
menu_title: 分配分类和产品
menu_order: 23
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: shared
github_link: b2b/shared-cat-product-assign.md
functional_areas:
  - B2B
  - Catalog
  - Integration
---

共享产品目录配置过程包含分配分类和产品到共享产品目录。要分配这些项到共享产品目录，首先要满足以下条件：

* 分类结构必须已经被定义。你不能创建一个新的分类来放到共享产品目录。使用像`POST /V1/categories`接口来创建一个新的分类。

* 每个分类下必须已经有产品，你不能分配一个新的产品到已经被包含在共享产品目录中的分类下。使用像`POST /V1/products`的接口来创建一个新的产品。

## 分配分类

`sharedCatalogCategoryManagementV1`服务基于`catalogCategoryManagementV1`。要查看一个商店下的分类结构，可以调用`GET /V1/categories`接口

<div class="bs-callout bs-callout-info" id="info" markdown="1">
当你分配一个分类到共享产品目录时，在分类下定义的产品都不会被包含，你必须单独地分配产品。
</div>

**服务名称**

`sharedCatalogCategoryManagementV1`

**REST接口**

{% highlight json %}
POST /V1/sharedCatalog/:id/assignCategories
POST /V1/sharedCatalog/:id/unassignCategories
GET  /V1/sharedCatalog/:id/categories
{% endhighlight %}

**分类参数**

<div class="bs-callout bs-callout-info" id="info" markdown="1">
虽然你可以指定其它在`categories`对象中定义的参数，但`id`是唯一用于绑定或解绑分类到共享产品目录的参数。
</div>

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
`id` | 分类的ID号 | integer | Required to assign or unassign a category

### 分配(绑定)分类和共享产品目录

下面的例子添加Luma Gear分类(`id=3`)及它的子类(`id=4,5,6`) 到一个自定义的共享产品目录。

**示例用法**

`POST /V1/sharedCatalog/2/assignCategories`

**载荷**

{% highlight json %}
{
  "categories": [
    {
      "id": 3
    },
    {
      "id": 4
    },
    {
      "id": 5
    },
    {
      "id": 6
    }
  ]
}
{% endhighlight %}

**响应**

`true`, 指示操作成功

### 从共享产品目录中解绑分类

当你从共享产品目录解绑分类时，Magento也会同时移除它在共享产品目录下的产品。如果产品被分配到了多个分类，Magento只移除当前解绑分类下的这个。

下面的例子从共享产品目录中移除了两个分类

**示例用法**

`POST /V1/sharedCatalog/2/unassignCategories`

**载荷**

{% highlight json %}
{
  "categories": [
    {
      "id": 7
    },

    {
      "id": 8
    }
  ]
}
{% endhighlight %}

**响应**

`true`, 指示操作成功

### 列出所有共享产品目录的分类

`GET`调用返回产品目录的ID数组

**样例用法**

`GET  /V1/sharedCatalog/2/categories`

**载荷**

不适用

**响应**

{% highlight json %}
[
  3,
  4,
  5,
  6
]
{% endhighlight %}

## 分配产品

`sharedCatalogProductManagementV1`服务基于`catalogProductManagementV1`. 要返回一个分类下定义的产品列表，可以调用`GET /V1/categories/:categoryId/products`.

**服务名称**

`sharedCatalogProductManagementV1 `

**REST接口**

{% highlight json %}
POST  /V1/sharedCatalog/:id/assignProducts
POST  /V1/sharedCatalog/:id/unassignProducts
GET  /V1/sharedCatalog/:id/products
{% endhighlight %}

**分类参数**

<div class="bs-callout bs-callout-info" id="info" markdown="1">
虽然你可以指定其它`products`对象定义的其它参数，但`sku`是唯一用于分配和解绑产品到共享产品目录的参数。
</div>

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
`sku` |产品的sku标识| string | 分配和解绑产品到共享产品目录时必需

### 分配产品到共享产品目录

下面的例子添加了Bags, Fitness Equipment及Watches分类下各两个产品到一个自定义的共享产品目录。指定的目录不须要在同一个分类下。

**示例用法**

`POST /V1/sharedCatalog/2/assignProducts`

**载荷**

{% highlight json %}
{
	"products": [
    	{
        	"sku": "24-MB01"
    	},
    	{
        	"sku": "24-MB04"
    	},
    	{
        	"sku": "24-UG06"
    	},
    	{
        	"sku": "24-UG07"
    	},
    	{
        	"sku": "24-MG04"
    	},
    	{
        	"sku": "24-MG01"
    	}
	]
}
{% endhighlight %}

**响应**

`true`, 指示操作成功

### 从共享产品目录解绑产品

解绑产品不会移除它所对应的分类

**示例用法**

`POST /V1/sharedCatalog/2/unassignProducts`

**载荷**
{% highlight json %}
{
  "products": [
  	{
  		"sku": "24-MG01"
  	}
  ]
}
{% endhighlight %}

**响应**

`true`, 指示操作成功

### 列出所有共享产品目录的产品

`GET`调用返回一个sku的数组

**样例用法**

`GET  /V1/sharedCatalog/2/products`

**载荷**

不适用

**响应**

{% highlight json %}
[
    "24-MB01",
    "24-MB04",
    "24-UG06",
    "24-UG07",
    "24-MG04"
]
{% endhighlight %}

## 相关信息

* [与ShareCatalog模块集成]({{ page.baseurl }}/b2b/shared-catalog.html)
* [管理共享类目录]({{ page.baseurl }}/b2b/shared-cat-manage.html)
* [分配公司]({{ page.baseurl }}/b2b/shared-cat-company.html)
