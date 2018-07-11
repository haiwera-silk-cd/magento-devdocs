---
group: b2b
subgroup: 10_REST
title: 管理公司角色
menu_title: 管理公司角色
menu_order: 14
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: company
github_link: b2b/roles.md
functional_areas:
  - B2B
---


在一个公司中，客户可能有多个不同的工作角色，职责层级，以及访问他们公司信息权限。{{site.data.var.b2b}}定义了几个类型的系统资源，并且公司管理员(或一个代表公司管理员的操作集成)使用公司角色授权或阻止这些资源的访问，公司管理员拥有所有资源的访问权限。

{{site.data.var.b2b}} 定义了以下类型的资源：

* 销售
* 可商议的报价
* 公司信息
* 公司用户管理
* 公司信用账户

其中的每一个资源都包含了其它资源的一个等级结构，当公司管理员从网店UI上授权或阻止一个资源的访问时，此动作会应用到所有的子资源，除非明确地覆盖。然面，如果你使用web API授权或阻止访问，你必须逐一地指定每一个资源

以下的表格列出了所有对客户可用的，与公司一起定义的资源。要可视化这些资源的等级结构，可以以公司管理员的身份登录到网店，选择**角色和权限**然后点击编辑，下一步到默认用户角色。

资源名称 | 显示名称 | 层等级
--- | --- | ---
Magento_Company::index | 全部 | 1
Magento_Sales::all | 销售 | 2
Magento_Sales::place_order | 结算(确认订单) | 3
Magento_Sales::payment_account | 使用记帐方式 | 4
Magento_Sales::view_orders | 查看订单 | 3
Magento_Sales::view_orders_sub | 查看下级用户的订单 | 4
Magento_NegotiableQuote::all | 报价 | 2
Magento_NegotiableQuote::view_quotes | 查看 | 3
Magento_NegotiableQuote::manage | 请求，编辑，删除 | 4
Magento_NegotiableQuote::checkout | 结算报价 | 4
Magento_NegotiableQuote::view_quotes_sub | 查看下级用户的报价 | 4
Magento_Company::view | 公司信息 | 2
Magento_Company::view_account | 帐号信息(查看) | 3
Magento_Company::edit_account | 编辑 | 4
Magento_Company::view_address | 法人地址(查看) |3
Magento_Company::edit_address | 编辑 | 4
Magento_Company::contacts | 联系人(查看) | 3
Magento_Company::payment_information| 支付信息(查看) | 3
Magento_Company::user_management | 公司用户管理 | 2
Magento_Company::roles_view | 查看角色和权限 | 3
Magento_Company::roles_edit | 管理角色和权限 | 4
Magento_Company::users_view | 查看用户和团队 | 3
Magento_Company::users_edit | 管理用户和团队 |  4
Magento_Company::credit | 公司信用账户 | 2
Magento_Company::credit_history | 查看 | 3

## 管理公司角色

公司管理员创建公共的角色及为角色绑定权限，然后将它们分配给用户，用以控制公司内每个客户可能的动作，在大多数情况下，少量的角色就足以覆盖公司所需的不同可能的权限组合

**服务名称**

`companyRoleRepositoryV1`

**REST接口**

{% highlight json %}
POST /V1/company/role/
PUT /V1/company/role/:id
GET /V1/company/role/:roleId
DELETE /V1/company/role/:roleId
GET /V1/company/role/
{% endhighlight %}

 **RoleInterface参数**

下面的表格列出了`RoleInterface`接口定义的参数

<table>
<tr>
<th>名称</th><th>描述</th><th>格式</th><th>要求</th></tr>
<tr>
<td><code>id</code></td><td>角色 ID</td><td>integer </td><td>更新和删除时必需</td></tr>
<tr>
<td><code>role_name</code></td><td>分配给角色的名字</td><td>string</td><td>创建角色时必需</td></tr>
<tr>
<td><code>permissions</code></td><td>一个授予给角色的资源及权限的列表，请情参考下面的权限数组表</td><td>Array[string]</td><td> 创建角色时必需</td></tr>
<tr>
<td><code>company_id</code></td><td>角色关联的公司 </td><td>integer</td><td>创建角色时必需</td></tr>
</table>

**Permissions array**

<table>
<tr>
<th>名称</th><th>描述</th><th>格式</th><th>要求</th></tr>
<tr>
<td><code>id</code></td><td>Magento生成的权限的ID</td><td>integer</td><td>更新和删除时必需</td></tr>
<tr>
<td><code>role_id</code></td><td>权限要应用在的角色ID </td><td>integer</td><td>创建角色时必需</td></tr>
<tr>
<td><code>resource_id</code></td><td>Magento资源的内部名称，比如 <code>Magento_Sales::place_order</code>.</td><td>string</td><td>必需</td></tr>
<tr>
<td><code>permission</code></td><td>Either <code>allow</code>或<code>deny</code>.</td><td>string</td><td>必需</td></tr>
</table>


### 创建一个角色

本例创建一个名为"Junior Buyer"我角色，它允许分配人访问所有销售的资源，除了"查看下级用户的订单"

所有不明确分配的资源都是被阻止的，你必须在所有调用中指定`Magento_Company::index`资源

**样例用法**

`POST /V1/company/role`

**载荷**

{% highlight json %}
{
  "role": {
    "role_name":"Junior Buyer",
    "permissions":[
      {"resource_id": "Magento_Company::index", "permission":"allow"},
      {"resource_id": "Magento_Sales::all", "permission":"allow"},
      {"resource_id": "Magento_Sales::place_order", "permission":"allow"},
      {"resource_id": "Magento_Sales::payment_account", "permission":"allow"},
      {"resource_id": "Magento_Sales::view_orders", "permission":"allow"},
      {"resource_id": "Magento_Sales::view_orders_sub", "permission":"deny"}
      ],
    "company_id": 2
  }
}
{% endhighlight %}

**响应**

{% collapsible 查看代码示例 %}
{% highlight json %}
{
  "id": 6,
  "role_name": "Junior Buyer",
  "permissions": [
    {
      "id": 176,
      "role_id": 6,
      "resource_id": "Magento_Company::index",
      "permission": "allow"
    },
    {
      "id": 177,
      "role_id": 6,
      "resource_id": "Magento_Sales::all",
      "permission": "allow"
    },
    {
      "id": 178,
      "role_id": 6,
      "resource_id": "Magento_Sales::place_order",
      "permission": "allow"
    },
    {
      "id": 179,
      "role_id": 6,
      "resource_id": "Magento_Sales::payment_account",
      "permission": "allow"
    },
    {
      "id": 180,
      "role_id": 6,
      "resource_id": "Magento_Sales::view_orders",
      "permission": "allow"
    },
    {
      "id": 181,
      "role_id": 6,
      "resource_id": "Magento_Sales::view_orders_sub",
      "permission": "deny"
    },
    {
      "id": 182,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::all",
      "permission": "deny"
    },
    {
      "id": 183,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::view_quotes",
      "permission": "deny"
    },
    {
      "id": 184,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::manage",
      "permission": "deny"
    },
    {
      "id": 185,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::checkout",
      "permission": "deny"
    },
    {
      "id": 186,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::view_quotes_sub",
      "permission": "deny"
    },
    {
      "id": 187,
      "role_id": 6,
      "resource_id": "Magento_Company::view",
      "permission": "deny"
    },
    {
      "id": 188,
      "role_id": 6,
      "resource_id": "Magento_Company::view_account",
      "permission": "deny"
    },
    {
      "id": 189,
      "role_id": 6,
      "resource_id": "Magento_Company::edit_account",
      "permission": "deny"
    },
    {
      "id": 190,
      "role_id": 6,
      "resource_id": "Magento_Company::view_address",
      "permission": "deny"
    },
    {
      "id": 191,
      "role_id": 6,
      "resource_id": "Magento_Company::edit_address",
      "permission": "deny"
    },
    {
      "id": 192,
      "role_id": 6,
      "resource_id": "Magento_Company::contacts",
      "permission": "deny"
    },
    {
      "id": 193,
      "role_id": 6,
      "resource_id": "Magento_Company::payment_information",
      "permission": "deny"
    },
    {
      "id": 194,
      "role_id": 6,
      "resource_id": "Magento_Company::user_management",
      "permission": "deny"
    },
    {
      "id": 195,
      "role_id": 6,
      "resource_id": "Magento_Company::roles_view",
      "permission": "deny"
    },
    {
      "id": 196,
      "role_id": 6,
      "resource_id": "Magento_Company::roles_edit",
      "permission": "deny"
    },
    {
      "id": 197,
      "role_id": 6,
      "resource_id": "Magento_Company::users_view",
      "permission": "deny"
    },
    {
      "id": 198,
      "role_id": 6,
      "resource_id": "Magento_Company::users_edit",
      "permission": "deny"
    },
    {
      "id": 199,
      "role_id": 6,
      "resource_id": "Magento_Company::credit",
      "permission": "deny"
    },
    {
      "id": 200,
      "role_id": 6,
      "resource_id": "Magento_Company::credit_history",
      "permission": "deny"
    }
  ],
  "company_id": 2,
  "extension_attributes": []
}
{% endhighlight %}
{% endcollapsible %}

### 更新角色

每个更新调用必须包含分配人将会访问的所有资源

本调用例子添加所有除了"查看下级用户报价"的议价资源到Junior Buyer角色

**样例用法**

`PUT /V1/company/role/6`

**载荷**

{% highlight json %}
{
  "role": {
    "id": 6,
    "permissions":[
      {"resource_id": "Magento_Company::index", "permission":"allow"},
      {"resource_id": "Magento_Sales::all", "permission":"allow"},
      {"resource_id": "Magento_Sales::place_order", "permission":"allow"},
      {"resource_id": "Magento_Sales::payment_account", "permission":"allow"},
      {"resource_id": "Magento_Sales::view_orders", "permission":"allow"},
      {"resource_id": "Magento_Sales::view_orders_sub", "permission":"deny"},
      {"resource_id": "Magento_NegotiableQuote::all", "permission":"allow"},
      {"resource_id": "Magento_NegotiableQuote::view_quotes", "permission":"allow"},
      {"resource_id": "Magento_NegotiableQuote::manage", "permission":"allow"},
      {"resource_id": "Magento_NegotiableQuote::checkout", "permission":"allow"},
      {"resource_id": "Magento_NegotiableQuote::view_quotes_sub", "permission":"deny"}
      ],
    "company_id": 2
  }
}
{% endhighlight %}

**响应**

{% collapsible 查看代码示例 %}
{% highlight json %}
{
  "id": 6,
  "role_name": "Junior Buyer",
  "permissions": [
    {
      "id": 226,
      "role_id": 6,
      "resource_id": "Magento_Company::index",
      "permission": "allow"
    },
    {
      "id": 227,
      "role_id": 6,
      "resource_id": "Magento_Sales::all",
      "permission": "allow"
    },
    {
      "id": 228,
      "role_id": 6,
      "resource_id": "Magento_Sales::place_order",
      "permission": "allow"
    },
    {
      "id": 229,
      "role_id": 6,
      "resource_id": "Magento_Sales::payment_account",
      "permission": "allow"
    },
    {
      "id": 230,
      "role_id": 6,
      "resource_id": "Magento_Sales::view_orders",
      "permission": "allow"
    },
    {
      "id": 231,
      "role_id": 6,
      "resource_id": "Magento_Sales::view_orders_sub",
      "permission": "deny"
    },
    {
      "id": 232,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::all",
      "permission": "allow"
    },
    {
      "id": 233,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::view_quotes",
      "permission": "allow"
    },
    {
      "id": 234,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::manage",
      "permission": "allow"
    },
    {
      "id": 235,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::checkout",
      "permission": "allow"
    },
    {
      "id": 236,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::view_quotes_sub",
      "permission": "deny"
    },
    {
      "id": 237,
      "role_id": 6,
      "resource_id": "Magento_Company::view",
      "permission": "deny"
    },
    {
      "id": 238,
      "role_id": 6,
      "resource_id": "Magento_Company::view_account",
      "permission": "deny"
    },
    {
      "id": 239,
      "role_id": 6,
      "resource_id": "Magento_Company::edit_account",
      "permission": "deny"
    },
    {
      "id": 240,
      "role_id": 6,
      "resource_id": "Magento_Company::view_address",
      "permission": "deny"
    },
    {
      "id": 241,
      "role_id": 6,
      "resource_id": "Magento_Company::edit_address",
      "permission": "deny"
    },
    {
      "id": 242,
      "role_id": 6,
      "resource_id": "Magento_Company::contacts",
      "permission": "deny"
    },
    {
      "id": 243,
      "role_id": 6,
      "resource_id": "Magento_Company::payment_information",
      "permission": "deny"
    },
    {
      "id": 244,
      "role_id": 6,
      "resource_id": "Magento_Company::user_management",
      "permission": "deny"
    },
    {
      "id": 245,
      "role_id": 6,
      "resource_id": "Magento_Company::roles_view",
      "permission": "deny"
    },
    {
      "id": 246,
      "role_id": 6,
      "resource_id": "Magento_Company::roles_edit",
      "permission": "deny"
    },
    {
      "id": 247,
      "role_id": 6,
      "resource_id": "Magento_Company::users_view",
      "permission": "deny"
    },
    {
      "id": 248,
      "role_id": 6,
      "resource_id": "Magento_Company::users_edit",
      "permission": "deny"
    },
    {
      "id": 249,
      "role_id": 6,
      "resource_id": "Magento_Company::credit",
      "permission": "deny"
    },
    {
      "id": 250,
      "role_id": 6,
      "resource_id": "Magento_Company::credit_history",
      "permission": "deny"
    }
  ],
  "company_id": 2,
  "extension_attributes": []
}
{% endhighlight %}
{% endcollapsible %}

### 返回角色的所有信息

此调用返回`id`，角色名，和指定`role_id`定义的权限集

**样例用法**

`GET /V1/company/role/6`

**载荷**

无

**响应**

{% collapsible 查看代码示例 %}
{% highlight json %}
{
  "id": 6,
  "role_name": "Junior Buyer",
  "permissions": [
    {
      "id": 226,
      "role_id": 6,
      "resource_id": "Magento_Company::index",
      "permission": "allow"
    },
    {
      "id": 227,
      "role_id": 6,
      "resource_id": "Magento_Sales::all",
      "permission": "allow"
    },
    {
      "id": 228,
      "role_id": 6,
      "resource_id": "Magento_Sales::place_order",
      "permission": "allow"
    },
    {
      "id": 229,
      "role_id": 6,
      "resource_id": "Magento_Sales::payment_account",
      "permission": "allow"
    },
    {
      "id": 230,
      "role_id": 6,
      "resource_id": "Magento_Sales::view_orders",
      "permission": "allow"
    },
    {
      "id": 231,
      "role_id": 6,
      "resource_id": "Magento_Sales::view_orders_sub",
      "permission": "deny"
    },
    {
      "id": 232,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::all",
      "permission": "allow"
    },
    {
      "id": 233,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::view_quotes",
      "permission": "allow"
    },
    {
      "id": 234,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::manage",
      "permission": "allow"
    },
    {
      "id": 235,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::checkout",
      "permission": "allow"
    },
    {
      "id": 236,
      "role_id": 6,
      "resource_id": "Magento_NegotiableQuote::view_quotes_sub",
      "permission": "deny"
    },
    {
      "id": 237,
      "role_id": 6,
      "resource_id": "Magento_Company::view",
      "permission": "deny"
    },
    {
      "id": 238,
      "role_id": 6,
      "resource_id": "Magento_Company::view_account",
      "permission": "deny"
    },
    {
      "id": 239,
      "role_id": 6,
      "resource_id": "Magento_Company::edit_account",
      "permission": "deny"
    },
    {
      "id": 240,
      "role_id": 6,
      "resource_id": "Magento_Company::view_address",
      "permission": "deny"
    },
    {
      "id": 241,
      "role_id": 6,
      "resource_id": "Magento_Company::edit_address",
      "permission": "deny"
    },
    {
      "id": 242,
      "role_id": 6,
      "resource_id": "Magento_Company::contacts",
      "permission": "deny"
    },
    {
      "id": 243,
      "role_id": 6,
      "resource_id": "Magento_Company::payment_information",
      "permission": "deny"
    },
    {
      "id": 244,
      "role_id": 6,
      "resource_id": "Magento_Company::user_management",
      "permission": "deny"
    },
    {
      "id": 245,
      "role_id": 6,
      "resource_id": "Magento_Company::roles_view",
      "permission": "deny"
    },
    {
      "id": 246,
      "role_id": 6,
      "resource_id": "Magento_Company::roles_edit",
      "permission": "deny"
    },
    {
      "id": 247,
      "role_id": 6,
      "resource_id": "Magento_Company::users_view",
      "permission": "deny"
    },
    {
      "id": 248,
      "role_id": 6,
      "resource_id": "Magento_Company::users_edit",
      "permission": "deny"
    },
    {
      "id": 249,
      "role_id": 6,
      "resource_id": "Magento_Company::credit",
      "permission": "deny"
    },
    {
      "id": 250,
      "role_id": 6,
      "resource_id": "Magento_Company::credit_history",
      "permission": "deny"
    }
  ],
  "company_id": 2,
  "extension_attributes": []
}
{% endhighlight %}
{% endcollapsible %}

### 删除角色

如果此角色是公司唯一的角色，则你不能删除它

**样例用法**

`DELETE /V1/company/role/5`

**载荷**

无

**响应**

`true`,指示请求成功

### 查找一个角色

下面的调用返回所有的被一个公司创建的(`company_id` = `2`)角色

参考[使用REST API搜索]({{ page.baseurl }}/rest/performing-searches.html)了解更多关于构造查询的信息

**样例用法**

`GET /V1/company/role?searchCriteria[filter_groups][0][filters][0][field]=company_id&searchCriteria[filter_groups][0][filters][0][value]=2&searchCriteria[filter_groups][0][filters][0][condition_type]=eq`

**载荷**

无

**响应**

{% collapsible 查看代码示例 %}
{% highlight json %}

{
    "items": [
        {
            "id": 2,
            "role_name": "Default User",
            "permissions": [
                {
                    "id": 26,
                    "role_id": 2,
                    "resource_id": "Magento_Company::index",
                    "permission": "allow"
                },
                {
                    "id": 27,
                    "role_id": 2,
                    "resource_id": "Magento_Sales::all",
                    "permission": "allow"
                },
                {
                    "id": 28,
                    "role_id": 2,
                    "resource_id": "Magento_Sales::place_order",
                    "permission": "allow"
                },
                {
                    "id": 29,
                    "role_id": 2,
                    "resource_id": "Magento_Sales::payment_account",
                    "permission": "deny"
                },
                {
                    "id": 30,
                    "role_id": 2,
                    "resource_id": "Magento_Sales::view_orders",
                    "permission": "allow"
                },
                {
                    "id": 31,
                    "role_id": 2,
                    "resource_id": "Magento_Sales::view_orders_sub",
                    "permission": "deny"
                },
                {
                    "id": 32,
                    "role_id": 2,
                    "resource_id": "Magento_NegotiableQuote::all",
                    "permission": "allow"
                },
                {
                    "id": 33,
                    "role_id": 2,
                    "resource_id": "Magento_NegotiableQuote::view_quotes",
                    "permission": "allow"
                },
                {
                    "id": 34,
                    "role_id": 2,
                    "resource_id": "Magento_NegotiableQuote::manage",
                    "permission": "allow"
                },
                {
                    "id": 35,
                    "role_id": 2,
                    "resource_id": "Magento_NegotiableQuote::checkout",
                    "permission": "allow"
                },
                {
                    "id": 36,
                    "role_id": 2,
                    "resource_id": "Magento_NegotiableQuote::view_quotes_sub",
                    "permission": "deny"
                },
                {
                    "id": 37,
                    "role_id": 2,
                    "resource_id": "Magento_Company::view",
                    "permission": "allow"
                },
                {
                    "id": 38,
                    "role_id": 2,
                    "resource_id": "Magento_Company::view_account",
                    "permission": "allow"
                },
                {
                    "id": 39,
                    "role_id": 2,
                    "resource_id": "Magento_Company::edit_account",
                    "permission": "deny"
                },
                {
                    "id": 40,
                    "role_id": 2,
                    "resource_id": "Magento_Company::view_address",
                    "permission": "allow"
                },
                {
                    "id": 41,
                    "role_id": 2,
                    "resource_id": "Magento_Company::edit_address",
                    "permission": "deny"
                },
                {
                    "id": 42,
                    "role_id": 2,
                    "resource_id": "Magento_Company::contacts",
                    "permission": "allow"
                },
                {
                    "id": 43,
                    "role_id": 2,
                    "resource_id": "Magento_Company::payment_information",
                    "permission": "allow"
                },
                {
                    "id": 44,
                    "role_id": 2,
                    "resource_id": "Magento_Company::user_management",
                    "permission": "allow"
                },
                {
                    "id": 45,
                    "role_id": 2,
                    "resource_id": "Magento_Company::roles_view",
                    "permission": "deny"
                },
                {
                    "id": 46,
                    "role_id": 2,
                    "resource_id": "Magento_Company::roles_edit",
                    "permission": "deny"
                },
                {
                    "id": 47,
                    "role_id": 2,
                    "resource_id": "Magento_Company::users_view",
                    "permission": "allow"
                },
                {
                    "id": 48,
                    "role_id": 2,
                    "resource_id": "Magento_Company::users_edit",
                    "permission": "deny"
                },
                {
                    "id": 49,
                    "role_id": 2,
                    "resource_id": "Magento_Company::credit",
                    "permission": "deny"
                },
                {
                    "id": 50,
                    "role_id": 2,
                    "resource_id": "Magento_Company::credit_history",
                    "permission": "deny"
                }
            ],
            "company_id": 2
        },
        {
            "id": 3,
            "role_name": "Senior Buyer",
            "permissions": [
                {
                    "id": 51,
                    "role_id": 3,
                    "resource_id": "Magento_Company::index",
                    "permission": "allow"
                },
                {
                    "id": 52,
                    "role_id": 3,
                    "resource_id": "Magento_Sales::all",
                    "permission": "allow"
                },
                {
                    "id": 53,
                    "role_id": 3,
                    "resource_id": "Magento_Sales::place_order",
                    "permission": "allow"
                },
                {
                    "id": 54,
                    "role_id": 3,
                    "resource_id": "Magento_Sales::payment_account",
                    "permission": "allow"
                },
                {
                    "id": 55,
                    "role_id": 3,
                    "resource_id": "Magento_Sales::view_orders",
                    "permission": "allow"
                },
                {
                    "id": 56,
                    "role_id": 3,
                    "resource_id": "Magento_Sales::view_orders_sub",
                    "permission": "allow"
                },
                {
                    "id": 57,
                    "role_id": 3,
                    "resource_id": "Magento_NegotiableQuote::all",
                    "permission": "allow"
                },
                {
                    "id": 58,
                    "role_id": 3,
                    "resource_id": "Magento_NegotiableQuote::view_quotes",
                    "permission": "allow"
                },
                {
                    "id": 59,
                    "role_id": 3,
                    "resource_id": "Magento_NegotiableQuote::manage",
                    "permission": "allow"
                },
                {
                    "id": 60,
                    "role_id": 3,
                    "resource_id": "Magento_NegotiableQuote::checkout",
                    "permission": "allow"
                },
                {
                    "id": 61,
                    "role_id": 3,
                    "resource_id": "Magento_NegotiableQuote::view_quotes_sub",
                    "permission": "allow"
                },
                {
                    "id": 62,
                    "role_id": 3,
                    "resource_id": "Magento_Company::view",
                    "permission": "allow"
                },
                {
                    "id": 63,
                    "role_id": 3,
                    "resource_id": "Magento_Company::view_account",
                    "permission": "allow"
                },
                {
                    "id": 64,
                    "role_id": 3,
                    "resource_id": "Magento_Company::edit_account",
                    "permission": "deny"
                },
                {
                    "id": 65,
                    "role_id": 3,
                    "resource_id": "Magento_Company::view_address",
                    "permission": "allow"
                },
                {
                    "id": 66,
                    "role_id": 3,
                    "resource_id": "Magento_Company::edit_address",
                    "permission": "deny"
                },
                {
                    "id": 67,
                    "role_id": 3,
                    "resource_id": "Magento_Company::contacts",
                    "permission": "allow"
                },
                {
                    "id": 68,
                    "role_id": 3,
                    "resource_id": "Magento_Company::payment_information",
                    "permission": "allow"
                },
                {
                    "id": 69,
                    "role_id": 3,
                    "resource_id": "Magento_Company::user_management",
                    "permission": "allow"
                },
                {
                    "id": 70,
                    "role_id": 3,
                    "resource_id": "Magento_Company::roles_view",
                    "permission": "allow"
                },
                {
                    "id": 71,
                    "role_id": 3,
                    "resource_id": "Magento_Company::roles_edit",
                    "permission": "allow"
                },
                {
                    "id": 72,
                    "role_id": 3,
                    "resource_id": "Magento_Company::users_view",
                    "permission": "allow"
                },
                {
                    "id": 73,
                    "role_id": 3,
                    "resource_id": "Magento_Company::users_edit",
                    "permission": "allow"
                },
                {
                    "id": 74,
                    "role_id": 3,
                    "resource_id": "Magento_Company::credit",
                    "permission": "allow"
                },
                {
                    "id": 75,
                    "role_id": 3,
                    "resource_id": "Magento_Company::credit_history",
                    "permission": "allow"
                }
            ],
            "company_id": 2
        },
        {
            "id": 4,
            "role_name": "Junior Buyer",
            "permissions": [
                {
                    "id": 76,
                    "role_id": 4,
                    "resource_id": "Magento_Company::index",
                    "permission": "allow"
                },
                {
                    "id": 77,
                    "role_id": 4,
                    "resource_id": "Magento_Sales::all",
                    "permission": "allow"
                },
                {
                    "id": 78,
                    "role_id": 4,
                    "resource_id": "Magento_Sales::place_order",
                    "permission": "allow"
                },
                {
                    "id": 79,
                    "role_id": 4,
                    "resource_id": "Magento_Sales::payment_account",
                    "permission": "allow"
                },
                {
                    "id": 80,
                    "role_id": 4,
                    "resource_id": "Magento_Sales::view_orders",
                    "permission": "allow"
                },
                {
                    "id": 81,
                    "role_id": 4,
                    "resource_id": "Magento_Sales::view_orders_sub",
                    "permission": "deny"
                },
                {
                    "id": 82,
                    "role_id": 4,
                    "resource_id": "Magento_NegotiableQuote::all",
                    "permission": "allow"
                },
                {
                    "id": 83,
                    "role_id": 4,
                    "resource_id": "Magento_NegotiableQuote::view_quotes",
                    "permission": "allow"
                },
                {
                    "id": 84,
                    "role_id": 4,
                    "resource_id": "Magento_NegotiableQuote::manage",
                    "permission": "allow"
                },
                {
                    "id": 85,
                    "role_id": 4,
                    "resource_id": "Magento_NegotiableQuote::checkout",
                    "permission": "allow"
                },
                {
                    "id": 86,
                    "role_id": 4,
                    "resource_id": "Magento_NegotiableQuote::view_quotes_sub",
                    "permission": "allow"
                },
                {
                    "id": 87,
                    "role_id": 4,
                    "resource_id": "Magento_Company::view",
                    "permission": "allow"
                },
                {
                    "id": 88,
                    "role_id": 4,
                    "resource_id": "Magento_Company::view_account",
                    "permission": "allow"
                },
                {
                    "id": 89,
                    "role_id": 4,
                    "resource_id": "Magento_Company::edit_account",
                    "permission": "deny"
                },
                {
                    "id": 90,
                    "role_id": 4,
                    "resource_id": "Magento_Company::view_address",
                    "permission": "allow"
                },
                {
                    "id": 91,
                    "role_id": 4,
                    "resource_id": "Magento_Company::edit_address",
                    "permission": "deny"
                },
                {
                    "id": 92,
                    "role_id": 4,
                    "resource_id": "Magento_Company::contacts",
                    "permission": "allow"
                },
                {
                    "id": 93,
                    "role_id": 4,
                    "resource_id": "Magento_Company::payment_information",
                    "permission": "allow"
                },
                {
                    "id": 94,
                    "role_id": 4,
                    "resource_id": "Magento_Company::user_management",
                    "permission": "allow"
                },
                {
                    "id": 95,
                    "role_id": 4,
                    "resource_id": "Magento_Company::roles_view",
                    "permission": "allow"
                },
                {
                    "id": 96,
                    "role_id": 4,
                    "resource_id": "Magento_Company::roles_edit",
                    "permission": "deny"
                },
                {
                    "id": 97,
                    "role_id": 4,
                    "resource_id": "Magento_Company::users_view",
                    "permission": "allow"
                },
                {
                    "id": 98,
                    "role_id": 4,
                    "resource_id": "Magento_Company::users_edit",
                    "permission": "deny"
                },
                {
                    "id": 99,
                    "role_id": 4,
                    "resource_id": "Magento_Company::credit",
                    "permission": "allow"
                },
                {
                    "id": 100,
                    "role_id": 4,
                    "resource_id": "Magento_Company::credit_history",
                    "permission": "allow"
                }
            ],
            "company_id": 2
        }
    ],
    "search_criteria": {
        "filter_groups": [
            {
                "filters": [
                    {
                        "field": "company_id",
                        "value": "2",
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

## 相关信息

* [集成公司模块]({{ page.baseurl }}/b2b/company.html)
* [管理公司对像]({{ page.baseurl }}/b2b/company-object.html)
* [管理公司用户]({{ page.baseurl }}/b2b/company-users.html)
* [管理公司结构]({{ page.baseurl }}/b2b/company-structures.html)
