---
group: arch-guide
subgroup: Components
title: 模块依赖
menu_title: 模块依赖
menu_order: 6
level3_menu_node: level3child
level3_subgroup: modules
version: 2.1
github_link: architecture/archi_perspectives/components/modules/mod_depend.md
redirect_from:
  - /guides/v1.0/architecture/modules/mod_depend.html
  - /guides/v2.0/architecture/modules/mod_depend.html
---

## 概述 {#m2devgde-moddep-intro}

*软件依赖* 表示一个软件组件为实现适当的功能依赖其它组件。Magento架构的一个核心原则是 **最小化软件依赖**. 并不是成为紧密地相互关联，而是被最佳地设计成<i>松藕合</i>。松藕合的模块执行它自身的任务时，需要更少或根本不需要知道其它模块的信息。

每一个Magento的{% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}响应一个唯一的特性。实践中，这意味着：

* 多个模块不能响应同一个特性

* 一个模块不能响应多个特性

* 模块依赖其它模块必须明确声明. 也要声明任何依赖的其它组件(例如, 主题，语言包，或库).

* 移除或禁用模块不会导致禁用其它模块。

## 什么组件能被模块依赖？

虽然Magento架构偏好松藕合的软件组件。但模块能包含这些的软件组件的依赖：

* 其它模块

* {% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %}扩展

* 库(可以是Magento框架的{% glossarytooltip 08968dbb-2eeb-45c7-ae95-ffca228a7575 %}库{% endglossarytooltip %}或第三方库)

<div class="bs-callout bs-callout-warning" id="warning">
<p>注意：如果模块被移除或禁用你可能会丢失模块包含的历史信息。我们建议您在禁用或移除模块前备份模块信息。</p></div>

## 管理模块依赖

在高层，Magento模块依赖主要有三个步骤：

1. 在`module.xml`文件中命名和声明模块。

2. 在模块的`composer.json`文件中声明所有模块有的依赖(无论是其它模块还是不同的组件)

3. (*可选*) 在`module.xml`中定义期望的配置文件以及`css`文件加载顺序。

例如:模块A声明要依赖模块B. 例如:模块A声明要依赖模块B.此时，在模块A的`module.xml`文件中，模块B要写到&lt;sequence>列表中，这样模块B的所有文件将在A加载完成后加载。 此外，你必须在模块A的`composer.json`文件中声明依赖B。同时，在<a href="{{ page.baseurl }}/config-guide/config/config-php.html">部署配置</a>中, 模块A和B必须同时被启用。

## 相关主题 {#m2arch-module-related}

<a href="{{ page.baseurl }}/architecture/archi_perspectives/components/modules/mod_intro.html">模块概述</a>

<a href="{{ page.baseurl }}/architecture/archi_perspectives/components/modules/mod_depend_types.html">模块依赖的类型</a>
>
