---
group: arch-guide
subgroup: Architectural Layers
title: 表示层
menu_title: Presentation layer
menu_order: 1
version: 2.0
github_link: architecture/archi_perspectives/present_layer.md
redirect_from: /guides/v1.0/architecture/archi_perspectives/present_layer.html
---

## 什么是Magento的表示层？

当你和Magento web接口交互时，那么你正在和 *表示层* 代码进行交互。

表示层包含处理来自或到用户界面的命令的视图元素 **(布局，显示区块，模板) ** 和 **控制器**。
表示层代码控制web用户和产品及其表现的交互。

你可以使用表示层的元素HTML,CSS和{% glossarytooltip ae0f1f68-c466-4189-88fd-6cd8b23c804f %}PHTML{% endglossarytooltip %}文件的修改来扩展地定制用户界面。
表示层表现HTML,CSS,Javascript,Magento UI,PHTML文件和显示区块文件的定制

表示层是四个层(表示层，服务层，领域层和持久层)中的最顶层

## 谁使用表示层？

三种类型的Magent用户与表示层代码交互。
Magento使用 *地区* 来有效地进行web服务调用，仅加载特定类型用户必要的依赖代码。
用户类型和它们关联的地区包括:

* **web用户** 和网店前台交互，他们可以看到Magento数据展示的视图模型；以及和产品UI元素交互为展现和操作来请求数据。
这些用户工作在(`frontend`)地区

* **系统管理员** 定制{% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网站前台{% endglossarytooltip %}可以间接地操作表示层，例如添加主题或小工具到前层。

* **Web {% glossarytooltip 786086f2-622b-4007-97fe-2c19e5283035 %}API{% endglossarytooltip %}调用** 能够通过像浏览器请求来产生，也能通过用户界面的AJAX调用来产生。

## 表示层组件

理解Magento表示层组件的一个有用方式是审查Magento的<i>主题</i>
Magento主题组织视觉的方面和某些产品行为的方面。

每一个{% glossarytooltip d2093e4a-2b71-48a3-99b7-b32af7158019 %}主题{% endglossarytooltip %}放置在一个唯一的目录并且包含自定义的布局、模板、样式及语言文件,这些文件一起工作来创造一个不同的用户体验。

对于主题元素的扩展介绍及如何扩展与覆盖Magento的默认主题，请参考<a href="{{ page.baseurl }}/frontend-dev-guide/bk-frontend-dev-guide.html">前端工程师手册</a>.

## 视图模型

Magento从树形的视图元素生成{% glossarytooltip a2aff425-07dd-4bd6-9671-29b7edefa871 %}HTML{% endglossarytooltip %}来给用户展示页面。

视图元素组织在两大类中：显示区块和容器。

* **显示区块** 能生成{% glossarytooltip f7550977-2132-4155-a5e0-d000fcfea866 %}动态内容{% endglossarytooltip %}及包含有名字的子视图元素，这类似于参数传递。
(`as`属性维护子视图元素的名字便于父显示区块引用它们)

* **容器** 收集一个有序的子视图元素的分组。

浏览器看到的产品页面是通过视图元素树渲染自身到HTML形成的
容器和显示区块放出被它们子元素适当包围的HTML。
显示区使用静态的HTML，Knockout JS脚本及PHTML块生成它们的内容.

## 表示层代码如何调用其它层。

典型地，表示层代码调用服务契约，尤其是网店前台。
然而，表示层代码偶尔依赖特定的实现，这些实现要求表示层代码直接调用<i>业务逻辑</i>层。
例如，{% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}管理面板{% endglossarytooltip %}UI展示通常被紧连接到一个特定的实现，并且在实现过程中是不通用的。

视图层调用模型中的代码来获取关于应用程序的状态信息(例如:产品的价格)
典型地，通过服务契约来访问模型层的方式

## 表示层流程

网页用户与表示层的组件交互来选择启动潜在的产品层的调用的动作。
表示层组件发起到服务层的调用，服务层依次发送请求到{% glossarytooltip 41aee03b-a5d5-49c2-8839-894090ef4e86 %}领域{% endglossarytooltip %}（或业务逻辑)层

## 相关主题 {#related}

<a href="{{ page.baseurl }}/architecture/archi_perspectives/arch_diagrams.html">架构图</a>

<a href="{{ page.baseurl }}/architecture/archi_perspectives/ALayers_intro.html">分层架构概述</a>
