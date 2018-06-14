---
group: arch-guide
subgroup: Architectural Layers
title: 分层架构概述
menu_title: 架构的分层
menu_node: parent
menu_order:
version: 2.0
github_link: architecture/archi_perspectives/ALayers_intro.md
redirect_from: /guides/v1.0/architecture/archi_perspectives/ALayers_intro.html
---

## Magento作为分层软件

在它的最就层，Magento的产品架构由核心软件加可选<i>模块<i>组成.这些可选的模块增强或替换了基础产品代码。

如果你相当多地定制Magento基础产品，{% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}开发将成为你关注的中心，模块组织支持特定任务或特征的代码。一个模块可以包含改变你的{% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网站前台{% endglossarytooltip %}的视觉和体验以及其基础行为的代码。

你的模块随着Magento产品核心代码起作用，它们被组织成层结构。为了理解Magento产品的组织结构，理解分层软件设计模式是非常必要的。

分成的软件在软件开发中是流行的，被广泛探讨的原则。关于这个主题有很多现有的资源，但考虑一般的探讨，查阅面象模式的软件架构

## 分层应用设计的优势

分层应用设计表现出很多优势，但Magento用户应领会：

* 严格地区分业务逻辑和表现逻辑以简化定制过程，例如，你可以修改你的网店前台的表现而不影响任何{% glossarytooltip 74d6d228-34bd-4475-a6f8-0c0f4d6d0d61 %}后端{% endglossarytooltip %}业务逻辑

* 清晰的代码组织可预见地指示{% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}扩展{% endglossarytooltip %}开发者定位代码。

## 相关主题

<a href="{{ page.baseurl }}/architecture/archi_perspectives/arch_diagrams.html">架构图</a>

<a href="{{ page.baseurl }}/architecture/archi_perspectives/present_layer.html">表示层</a>

<a href="{{ page.baseurl }}/architecture/archi_perspectives/service_layer.html">服务层</a>

<a href="{{ page.baseurl }}/architecture/archi_perspectives/domain_layer.html">领域层</a>

<a href="{{ page.baseurl }}/architecture/archi_perspectives/persist_layer.html">持久层</a>
