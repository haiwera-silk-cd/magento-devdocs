---
group: arch-guide
subgroup: 架构基础
title: 容易的前端定制
menu_title: 容易的前端定制
menu_node:
menu_order:
version: 2.1
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

包含在{% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento管理面板{% endglossarytooltip %}表单元素模板包括：

* 地址表单
* 按钮栏
* 容器
* 标签页
* 注册表单

Magento默认网店前台的用户会看到这些表单元素样本，这些模板为{% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}扩展{% endglossarytooltip %}开发者及管理员提供了一个非常有用的软件组件语言（间接地，用户体验）

Magento{% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}管理面板{% endglossarytooltip %}模板库使用LESS预处理器构建并以模块的形式实现，你可以从[Magento Marketplace](https://marketplace.magento.com/){:target="_blank"}.免费下载当前这个版本的模块

参考<a href="{{ page.baseurl }}/pattern-library/bk-pattern.html">Magento管理面板用到的设计模式和库</a> 了解更多使用这个库的信息

## 相关主题 {#m2arch-related}

<a href="{{ page.baseurl }}/architecture/extensibility.html">可扩展和模块化</a>

<a href="{{ page.baseurl }}/architecture/global_extensibility_features.html">全局扩性特征</a>

<a href="{{ page.baseurl }}/pattern-library/bk-pattern.html">Magento管理面板用到的设计模式和库</a>

<a href="{{ page.baseurl }}/ui-components/ui-component.html">Magento UI库组件</a>
