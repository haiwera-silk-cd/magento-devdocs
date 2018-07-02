---
group: b2b
subgroup: 10_REST
title: 管理公司结构
menu_title: 管理公司结构
menu_order: 15
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: company
github_link: b2b/company-structures.md
functional_areas:
  - B2B
  - Integration
---

{{site.data.var.b2b}}允许公司用户被分配到公司团队或等级结构中。

## 管理公司团队

公司团队允许使用位置、工作职责或作何你选择的标准分组公司的用户。你可以使用公司等级结构接口分配自身的公司用户到团队中

**服务名称**

`companyTeamRepositoryV1`

**REST接口**

{% highlight json %}
POST /V1/team/:companyId
PUT /V1/team/:teamId
GET /V1/team/:teamId
DELETE /V1/team/:teamId
GET /V1/team/
{% endhighlight %}


**公司团队参数**

名称 | 描述 | 格式 | 要求
--- | --- | --- | ---
id | 系统生成的团队ID | integer | 创建操作不可用
name | 团队的显示名称 | string | Required to create or update a team.
description | 团除的可选的描述 | string | 可选

### 创建一个团队

一个新创建的团队位于公司等级结构中的公司管理员下

**样例用法**

`POST /V1/team/2`

**载荷**

{% highlight json %}
{
  "team": {
    "name": "Western District",
    "description": "Buyers from the California office"
  }
}
{% endhighlight %}

**响应**

团队的ID,  比如`4`

### 更新团队

你仅能修改团队的名字或描述

**样例用法**

`PUT /V1/team/4`

**载荷**

{% highlight json %}
{
  "team": {
  	"id": 4,
    "name": "Western Region"
  }
}
{% endhighlight %}

**响应**

`true`,指示请求成功

### 返回所有的团队信息

此`GET`调用返回团队`id`,`name`及`description`

**样例用法**

`GET /V1/team/4`

**载荷**

不适用

**响应**

{% highlight json %}
{
  "id": 4,
  "name": "Western Region",
  "description": "Buyers from the California office"
}
{% endhighlight %}

### 删除团队

如果有成员分配，你不能删除此团队

**样例用法**

`DELETE /V1/team/4`

**载荷**

不适用

**响应**

An empty array

### 搜索团队

下面的请求返回所有团队(`team_id` &ge; `0`)

参考[使用REST API搜索]({{ page.baseurl }}/rest/performing-searches.html)了解更多关于构造查询的信息

**样例用法**

`GET V1/team?searchCriteria[filter_groups][0][filters][0][field]=team_id&searchCriteria[filter_groups][0][filters][0][value]=0&searchCriteria[filter_groups][0][filters][0][condition_type]=gteq`

**载荷**

不适用

**响应**
{% collapsible Show code sample %}
{% highlight json %}
{
    "items": [
        {
            "id": 1,
            "name": "West",
            "description": "California office"
        },
        {
            "id": 2,
            "name": "East",
            "description": "New York office"
        }
    ],
    "search_criteria": {
        "filter_groups": [
            {
                "filters": [
                    {
                        "field": "team_id",
                        "value": "0",
                        "condition_type": "gteq"
                    }
                ]
            }
        ]
    },
    "total_count": 2
}
{% endhighlight %}
{% endcollapsible %}

## 公司的等级结构

在B2B网店前台，购买者可以看见表示成一棵等级结构树的公司结构。这棵树显示公司细分的多个层级及公司用户。公司的等级结构可以有任意数量的团队和层级。

你可以使用REST接口来在当前等级结构中接收当前结构和移动团队及购买者

**服务名称**

`companyHierarchyV1`

**REST接口**

{% highlight json %}
GET /V1/hierarchy/:id
PUT /V1/hierarchy/move/:id
{% endhighlight %}

### 返回所有的公司等级的信息

下面的例子，以下的公司等级已经建立

```
Admin (structure_id = 2)
|-- East (team, structure_id = 8)
|   |-- Bryce Martin (customer, structure_id = 4)
|   |-- Melanie Shaw (customer, structure_id = 3)
|
|-- West (team, structure_id = 7)
|   |-- Marcus Thomas (customer, structure_id = 6)
|   |-- Teresa Gomez (customer, structure_id = 5)
```

**样例用法**

`GET /V1/heirarchy/2`

**载荷**

不适用

**响应**

{% collapsible Show code sample %}
{% highlight json %}

[
  {
    "structure_id": 6,
    "entity_id": 7,
    "entity_type": "customer",
    "structure_parent_id": 7
  },
  {
    "structure_id": 5,
    "entity_id": 6,
    "entity_type": "customer",
    "structure_parent_id": 7
  },
  {
    "structure_id": 7,
    "entity_id": 1,
    "entity_type": "team",
    "structure_parent_id": 2
  },
  {
    "structure_id": 3,
    "entity_id": 4,
    "entity_type": "customer",
    "structure_parent_id": 8
  },
  {
    "structure_id": 4,
    "entity_id": 5,
    "entity_type": "customer",
    "structure_parent_id": 8
  },
  {
    "structure_id": 8,
    "entity_id": 2,
    "entity_type": "team",
    "structure_parent_id": 2
  },
  {
    "structure_id": 2,
    "entity_id": 3,
    "entity_type": "customer",
    "structure_parent_id": 0
  }

{% endhighlight %}
{% endcollapsible %}

### 分配一个新的父节点到团队和公司用户上

下面的例子移动Bryce Martin (`structure_id = 4`)到West团队

**样例用法**

`PUT /V1/hierarchy/move/5`

**载荷**

{% highlight json %}
{
  "newParentId": 7
}
{% endhighlight %}

**响应**

`[]` (一个空数组)


## 相关信息

* [集成公司模块]({{ page.baseurl }}/b2b/company.html)
* [管理公司对像]({{ page.baseurl }}/b2b/company-object.html)
* [管理公司用户]({{ page.baseurl }}/b2b/company-users.html)
* [管理公司角色]({{ page.baseurl }}/b2b/roles.html)
