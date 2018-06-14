---
group: arch-guide
subgroup: Architectural Layers
title: 服务层
menu_title: 服务层
menu_order: 2
version: 2.0
github_link: architecture/archi_perspectives/service_layer.md
redirect_from: /guides/v1.0/architecture/archi_perspectives/service_layer.html
---

## 什么是服务层?

服务层提供在表示层和{% glossarytooltip 41aee03b-a5d5-49c2-8839-894090ef4e86 %}领域{% endglossarytooltip %}模型层逻辑和资源相关的数据之间一个桥梁。
使用*服务契约*实现，服务契约以{% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %}接口的形式定义的。

通常，服务层:

* 处在表示层下面而在领域层上面。

* 包含服务契约，契约定义了实现如何表现。

* 提供一种简单的方式访问REST/SOAP{% glossarytooltip 786086f2-622b-4007-97fe-2c19e5283035 %}API{% endglossarytooltip %}框架代码(它也处在服务契约上面)
你可以通过配置绑定服务API到服务契约上 --- 不需要写代码。

* 提供为其它的模块调用进来的稳定的API。

## 谁调用服务层？

所有服务接口的调用或和你{% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网站前台{% endglossarytooltip %}一起工作的用户(他们是启动控制器的请求),通常都是通过服务层路由的.
我们非常鼓励使用服务契约的来调用业务逻辑。

外部的应用程序为完成业务逻辑可以以简单的SOAP和REST调用发起请求。
用一些简单的{% glossarytooltip 8c0645c5-aa6b-4a52-8266-5659a8b9d079 %}XML{% endglossarytooltip %}或JSON，你可以暴露服务层的PHP API并使它可被REST或SOAP的web服务访问
一旦被实现，网页服务能发起一个简单的 API调用并返回信息丰富的数据结构。

{% glossarytooltip cdf644c4-bc99-4550-a954-dd5ae165785a %}服务契约{% endglossarytooltip %}的客户端包含:

* 控制器 (被网店前台用户的动作启动的)

* Web 服务(SOAP和REST调用)

* 其它经由服务契约的Magento模块。

## 服务契约剖析

一个{% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}的服务契约由一系列的接口定义，它们放在模块的`/Api`目录下。

目录包含:

* 模块(比如[Catalog API][catalog-api])的`/Api` {% glossarytooltip 621ef86b-7314-4fbc-a80d-ab7fa45a27cb %}命名空间{% endglossarytooltip %}下的服务接口

* `Api/Data`目录下的数据(或 *实体*)接口(例如：[Catalog API/Data][catalog-api-data]).
  *数据实体* 是服务接口传递和返回的数据结构
  
  数据目录下的文件为实体表和扩展属性的项设有`get()`和`set()`方法

通常，服务契约提供三种不同类型的接口：

* 仓库接口

* 管理接口

* {% glossarytooltip 3f0f2ef1-ad38-41c6-bd1e-390daaa71d76 %}元数据{% endglossarytooltip %}接口

然而，服务契约不必都要符合这三种模式

## 服务契约的优势

服务契约允许你去添加一个定制的添加或修改了业务逻辑层资源模型的{% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}扩展{% endglossarytooltip %}而不破坏系统。

在定制的模块的{% glossarytooltip 2be50595-c5c7-4b9d-911c-3bf2cd3f7beb %}依赖注入{% endglossarytooltip %}配置文件(`di.xml`)中使用*&lt;preference&gt;*元素

`di.xml`文件指定了哪一个PHP类用于`Magento\Customer\Api\CustomerRepositoryInterface`接口.

其它模块可以以指定不同类名的方式改变接口文件。
然而，如果客户端代码仅使用了接口的定义，那么类修改就是不必要的。

## 相关主题 {#related}

<a href="{{ page.baseurl }}/architecture/archi_perspectives/arch_diagrams.html">架构图</a>

<a href="{{ page.baseurl }}/architecture/archi_perspectives/ALayers_intro.html">分层架构概述</a>

[catalog-api]: {{ site.mage2000url }}app/code/Magento/Customer/Api
[catalog-api-data]: {{ site.mage2000url }}app/code/Magento/Customer/Api/Data
