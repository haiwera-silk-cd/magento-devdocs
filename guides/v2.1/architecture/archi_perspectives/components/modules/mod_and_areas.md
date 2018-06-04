---
group: arch-guide
subgroup: Components
title: 模块和地区
menu_title: 模块和地区
menu_order: 4
level3_menu_node: level3child
level3_subgroup: modules
version: 2.1
github_link: architecture/archi_perspectives/components/modules/mod_and_areas.md
redirect_from:
  - /guides/v1.0/architecture/modules/mod_and_areas.html
  - /guides/v2.0/architecture/modules/mod_and_areas.html
---

## 概述 {#m2arch-module-areas-overview}

*地区* 是一个为了优化请求处理而组织代码的逻辑组件，Magento使用地区把web服务调用做流线型，仅载入指定地区相关的代码。Magento定义的每个默认地区可以包含完全不同的代码，来处理URL和用户请求

例如,如果你正在调用一个REST的服务，而不加载所有关联到生成用户{% glossarytooltip a2aff425-07dd-4bd6-9671-29b7edefa871 %}HTML{% endglossarytooltip %}页面的代码，你可以指定一个独立的地区来加载代码，这会使响应这个REST调用的范围被限制。

### Magento地区类型

Magento被组织成以下几个主地区:

* **Magento 管理面板** (`adminhtml`): 地区的入口点是`index.php`或`public/index.php`。 {% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}管理{% endglossarytooltip %}面板地区包含了网店管理所需的代码。 /app/design/adminhtml目录包含了所有你可以在管理面板看到的所有组件的代码

* **网店前台** (`frontend`): 地区的入口点是`index.php`或`public/index.php`。 网店前台(或`frontend`)包含模板及定义了你{% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网店前台{% endglossarytooltip %}展示的{% glossarytooltip 73ab5daa-5857-4039-97df-11269b626134 %}布局{% endglossarytooltip %}文件.

* **基础** (`base`): 用于归并机制，当在`adminhtml`和`frontend`地区中没有找到文件时。归并机制会使用这个地区下的文件。

你也可以使用SOAP和REST API发送请求到Magento，如下两个地区：

* **Web API REST** (`webapi_rest`): 地区的入口点是`index.php`或`public/index.php`。 REST地区有一个知道如何处理{% glossarytooltip a05c59d3-77b9-47d0-92a1-2cbffe3f8622 %}URL{% endglossarytooltip %}的前端控制器,对REST基础URL进行查找.

* **Web API SOAP** (`webapi_soap`): 地区的入口点是`index.php`或`public/index.php`。

## 地区如何与模块一起工作 {#m2arch-module-using}

模块定义了一个地区的哪些资源是可见及可访问的，以及地区的行为，相同的{% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}可以影响多个地区。比如，RMA模块的一部份表现在`adminhtml`地区，一部分表现在`frontend`地区。

如果你的{% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}扩展{% endglossarytooltip %}工作在几个不同的地区，请确保每个地区分别拥有行为和视图组件。

每个地区在模块中声明了自身，所有地区特定的资源位于相同的模块中。

你可以启用或禁用模块的地区。如果这个模块是启用的，它注入一个地区路由到生成的应用程路由处理中。如果模块是禁用的，Magento将不会加载地区的路由，结果是你的地区的资源和特定的功能将不能访问。

### 快速了解模块/地区的交互

* 模块不应该依赖其它模块的地区。

* 禁用地区不会导致禁用它相关的模块。

* 地区在{% glossarytooltip 2be50595-c5c7-4b9d-911c-3bf2cd3f7beb %}依赖注入{% endglossarytooltip %}框架的`di.xml`中注册

### 注意Magento的请求处理

Magento处理URL请求首先剥离基础URL,剩下的路径的第一段标识请求的地区。

在地区名之后，URI指定了*full front name*. 当一个HTTP请求到达时，这部分会从URL中拿出来. Magento使用这部分标识哪个控制器(一个{% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %}类)的哪个方法(一个PHP类的方法)将被执行。展示一个HTML页面的通常方法是`index`. 它将返回一个html页面。

## 相关主题 {#m2arch-module-related}

* <a href="{{ page.baseurl }}/architecture/archi_perspectives/components/modules/mod_intro.html">模块概述</a>

