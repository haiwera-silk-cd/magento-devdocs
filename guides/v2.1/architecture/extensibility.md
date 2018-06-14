---
group: arch-guide
subgroup: 架构基础
title: 可扩展和模块化
menu_title: 可扩展和模块化
menu_node:
menu_order:
version: 2.1
github_link: architecture/extensibility.md
---

## 概述

产品<i>可扩展性</i>描述扩展产品特征是否简单，一个可扩展的产品是以最简单定制和增强的策略设计的。可扩展的产品设计成扩展特征简单、丰富当前特征简单及集成三方软件简单。

通过所有Magento开发的方面最大化可扩展性是我们的目标。核心任务，像物流，被打包成一个分离的模块，并且你可以通过安装买来的或自己开发的三方模块或库来扩展你的特性。甚至每个逻辑相关的{% glossarytooltip b51bd4e9-7174-4ca0-83a0-1a895c9fc9e8 %}shipping carrier{% endglossarytooltip %}也被打包成分离的模块，你可以以简单的添加或删除模块的形式非常方便地添加或删除物流提供商。Magento框架提供公用的逻辑来控制路由和其它核心应用程序的功能

## 什么使得产品可扩展？

<i>Magento可扩展性</i>描述了产品的内在的能力，这种能力表现为随着业务的增长，开发者和店主能常规地扩展他们网店的兼容性

以下是影响可扩展性的主要因素。

### 指导产品结构的架构原则

Magento软件开发的模式的核心是替换和扩展核心代码而不直接修改它们。这种策略支持你在维持我们提供的已测代码完整性的同时，仍能广泛地定制你的{% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网店{% endglossarytooltip %}

### 开源软件来创建和管理扩展

Magento在有开发社区的开源技术上构建，例如，它使用了% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %}来管理依赖，参考<a href="{{ page.baseurl }}/architecture/tech-stack.html">技术栈</a>了解完整的用到的技术。

### 编码规范

遵守{% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %}和{% glossarytooltip 312b4baf-15f7-4968-944e-c814d53de218 %}JavaScript{% endglossarytooltip %}代码的标准最佳实现确何代码基础是合理的。Magento的PHP代码采用了大量的Zend框架的编码规范，更多信息请参考<a href="{{ page.baseurl }}/coding-standards/bk-coding-standards.html">编码规范</a>

### 升级和版本控制策略

Magento定义了良好的升级和版本控制策略能帮你避免软件组件依赖的任何问题。添加模块是在确认{% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}版本与Magento框架版本之后

## 相关主题 {#m2arch-related}

<a href="{{ page.baseurl }}/architecture/archi_perspectives/ABasics_intro.html">架构基础</a>

<a href="{{ page.baseurl }}/architecture/global_extensibility_features.html">全局可扩展的特性</a>

<a href="{{ page.baseurl }}/architecture/frontend_custom_strategies.html">容易的前端定制</a>
