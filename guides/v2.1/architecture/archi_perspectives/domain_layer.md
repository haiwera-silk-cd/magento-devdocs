---
group: arch-guide
subgroup: Architectural Layers
title: 领域层
menu_title: 领域层
menu_order: 3
version: 2.1
github_link: architecture/archi_perspectives/domain_layer.md
redirect_from: /guides/v1.0/architecture/archi_perspectives/domain_layer.html
---

## 什么是领域层？

{% glossarytooltip 41aee03b-a5d5-49c2-8839-894090ef4e86 %}领域{% endglossarytooltip %}层维护Magento{% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}的业务逻辑。典型地，它不包含资源相关的或数据库相关的信息。它的主要功能包括：

* 定义一般的Magento数据对象，或模型，它们包含业务逻辑。这些逻辑定义了在特定类型的数据上（诸如一个客户对象）哪些操作可以被执行。模型则仅包含普通信息。应用程序也可以使用SOAP或REST风格的接口来请求模型的数据。

* (可选)包含服务契约的实现，虽然没有它们的定义。

<div class="bs-callout bs-callout-tip">
  <p><b>最佳实践:</b> 使用服务契约通过强类型对象传递数据类型来和领域层通信。这会帮助你避免当替换业务层逻辑时替换表示层的代码的需要。</p>
</div>

## 模型

每个领域层的模型包含一个资源模型的引用，这个引用用于通过MySQL调用来接收数据库的数据。资源模型包含连接到潜在数据库的逻辑，典型地像MySQL.一个模型只有在模型数据必须持久化的情况下才需要资源模型.

## 谁访问领域层？

有三种主要的访问一个模块领域层代码方式：

* 服务契约是一个模块访问另一个模块领域层代码最推荐的方式。这样的松藕合情况也是多数模块访问其它模块最优的方式。

* 一个模块直接调用到另一个模块。这种紧藕合的情况在大多数情况下是不被推荐的，但有时可能又无法避免。

* 一个模块的领域层代码也能能过以下方式将自己插入到另一个模块：

    * 事件钩子

    * 插件

    * `di.xml`文件(使用SPI契约)

你的调用另一个模块领域层代码的策略是相当依赖唯一配置和你系统需要的

## 相关主题 {#related}

<a href="{{ page.baseurl }}/architecture/archi_perspectives/arch_diagrams.html">架构图</a>

<a href="{{ page.baseurl }}/architecture/archi_perspectives/ALayers_intro.html">分层架构概述</a>
