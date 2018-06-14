---
group: arch-guide
subgroup: Architectural Layers
title: 持久层
menu_title: 持久层
menu_order: 4
version: 2.1
github_link: architecture/archi_perspectives/persist_layer.md
redirect_from: /guides/v1.0/architecture/archi_perspectives/persist_layer.html
---

Magento使用活动记录模式生策略处理持久层。在系统中，模型对象包含一个映身对象到一个或多个数据库行记录的 *资源模型* 。一个资源模型可响应像下面这样执行的功能：

* 执行所有的CRUD(增、删、改、查)请求。资源模型为完成这些请求包含SQL代码。

* 执行附加业务逻辑。例如，一个资源模型可以执行数据校验，在数据被保存之前或之后开启进程，或执行另外的数据库操作。

如果你期望从一个数据库请求返回多个数据项，你可以实现一个特殊类型的模型，这个模型叫作 *集合* ，一个集合是一个基于一系列规则加载多个模型到一个数组结构中的类。这类似于SQL中的`WHERE`子句。

一个简单的资源模型定义且与一个简单表交互。

然而，一些对象有大量的属性，或它们可能有许多关联对象，而这些关联对象有大量的属性。在这种情况下，这些对象是使用了 **实体属性值 (EAV)** 的模型构造的对象。 

任何使用了EAV资源的模型有它自己的从某些MySQL表展开来的属性。

`Customer`,`Catalog`和`Order`的资源模型都使用了EAV属性。

## 相关主题 {#related}

<a href="{{ page.baseurl }}/architecture/archi_perspectives/arch_diagrams.html">架构图</a>

<a href="{{ page.baseurl }}/architecture/archi_perspectives/ALayers_intro.html">分层架构概述</a>
