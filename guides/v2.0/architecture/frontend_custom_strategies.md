---
group: arch-guide
subgroup: 架构基础
title: 容易的前端定制
menu_title: 容易的前端定制
menu_node:
menu_order:
version: 2.0
github_link: architecture/frontend_custom_strategies.md
---

## 概述 {#m2arch-whatis-overview}

Magento{% glossarytooltip b00459e5-a793-44dd-98d5-852ab33fc344 %}前端{% endglossarytooltip %}被设计成用高度可扩展的主题做为核心定制机制来优化{% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网站前台{% endglossarytooltip %}的定制。

推荐店主使用Magento组件和主题来扩展及改变网店的外观。

## 网店前台定制工具

Magento 提供了几个工具来明显地帮助你快速开始前端定制过程：

* Magento空白{% glossarytooltip d2093e4a-2b71-48a3-99b7-b32af7158019 %}主题{% endglossarytooltip %}

* <a href="{{ page.baseurl }}/ui-components/ui-component.html">Magento UI库组件</a>

* <a href="{{ page.baseurl }}/pattern-library/bk-pattern.html">Magento管理面板用到的设计模式和库</a>

参考<a href="{{ page.baseurl }}/frontend-dev-guide/bk-frontend-dev-guide.html">前端工程师手册</a>了解更多关于创建主题的信息。

### Magento空白主题

Magento空白主题模板为定制提供了一个跳板，你可以使用这个样板为一个稳健的起点开发你自己的主题

### Magento UI 组件
使用Magento标准代码和样式工具可以帮助我们：

* 增强你网店前台的设计风格的一致性
* 简化(及加快)设置过程

组件{% glossarytooltip 08968dbb-2eeb-45c7-ae95-ffca228a7575 %}库{% endglossarytooltip %}包含标准的可重用的表单特性的组件，如输入框和按钮以及导航元素。Magento UI库是一个通用Web组件集合并且是Magento特定的样板，这些样板简化主题创建和定制过程

参考<a href="{{ page.baseurl }}/ui-components/ui-component.html">Magento UI库组件</a>了解更多相关信息

### Magento管理面板样板库

<i>样版库</i>是一个用户界面设计样版的集合，它们始终能在你安装的产品中被重复使用。<a href="{{ page.baseurl }}/pattern-library/bk-pattern.html">Magento管理面板用到的设计模式和库</a>定义了一些管理员工作在网店前台能使用的组件的例子。

Form elements included in the {% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento管理面板{% endglossarytooltip %} pattern library include:

* address form
* button bar
* container
* tabs
* sign-in form

Users of the default Magento storefront encounter examples of these form elements throughout the product. These patterns provide a valuable language of software 组件 (and indirectly, user experiences) for {% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}扩展{% endglossarytooltip %} developers and administrators.

The Magento {% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}Admin{% endglossarytooltip %} Pattern library is built on the LESS preprocessor and implemented as a {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}. You can download a free, current version of this module from [Magento Marketplace](https://marketplace.magento.com/){:target="_blank"}.

See <a href="{{ page.baseurl }}/pattern-library/bk-pattern.html">Magento管理面板用到的设计模式和库</a> for more information on using this library.

## 相关主题 {#m2arch-related}

<a href="{{ page.baseurl }}/architecture/extensibility.html">可扩展和模块化</a>

<a href="{{ page.baseurl }}/architecture/global_extensibility_features.html">Global extensibility features</a>

<a href="{{ page.baseurl }}/pattern-library/bk-pattern.html">Magento管理面板用到的设计模式和库</a>

<a href="{{ page.baseurl }}/ui-components/ui-component.html">Magento UI库组件</a>
