---
group: arch-guide
subgroup: Components
title: 模块依赖类型
menu_title: 模块依赖类型
menu_order: 7
level3_menu_node: level3child
level3_subgroup: modules
version: 2.1
github_link: architecture/archi_perspectives/components/modules/mod_depend_types.md
redirect_from: /guides/v1.0/architecture/modules/mod_depend_types.html
---

## 两类依赖 {#m2devgde-moddep-declare-dep}

Magento{% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}有两种依赖类型: 硬依赖和软依赖.

## 硬依赖

模块和另一个模块有 *硬依赖* ，在缺少另一个模块时这个模块是无法起做用的。特别地：

* 这个模块直接包含另一个模块的逻辑代码，(例如,后者的模块实例，类常量，静态方法，公共类属性，接口及特点)

* 模块包含另一个模块的类名，方法名，类常量，类属性，接口及特点的字符串。

* 模块反序列化另一个模块声明的类对像。

* 模块使用或修改用于另一个模块的数据库表。

## 软依赖

模块和另一个模块有 *软依赖* ，在缺少另一个模块时即使存在依赖可能也可以正常工作。

* 模块直接检查别一个模块的有效性。

* 模块扩展另一个模块的配置。

* 模块扩展另一个模块的 {% glossarytooltip 73ab5daa-5857-4039-97df-11269b626134 %}布局{% endglossarytooltip %}。

<div class="bs-callout bs-callout-warning" id="warning">
  <p>
    注意：一个模块使用另一个模块的代码，应该明确的声明依赖。
  </p>
</div>

Magento以下面的顺序安装模块：

1) 作为另一个模块的依赖为其提供服务的模块

2) 依赖它的模块

## 不恰当的依赖 {#m2devgde-moddep-inapp-dep}

避免创建以下类的依赖：

* 循环(包括直接的和间接的)

* 未声明的

* 错误的

## 在不同产品层的模块间的依赖 {#m2devgde-moddep-diff-layer}

你可以在模块间的不同层构建依赖。

## 框架层的依赖 {#m2devgde-moddep-frmwk-layer}

Magento框架的模块可以通过显示依赖用于应用层。

<div class="bs-callout bs-callout-info" id="info">
  <p>注意：这种情况下，使用接口比直接用类更好。 </p>
  <p>你可以在Magento的类之间构建依赖，即使他们属于不同模块。</p>
</div>

## 应用层依赖 {#m2devgde-moddep-app-layer}
属于应用层的模块不能被用在Magento框架上。

你可以应用层的类之间构建依赖，但是这些类必须属于相同的模块。模块间的应用层依赖只能被{% glossarytooltip cdf644c4-bc99-4550-a954-dd5ae165785a %}服务契约{% endglossarytooltip %}或服务提供器接口(SPI)构建。

## 相关主题 {#m2arch-module-related}

<a href="{{ page.baseurl }}/architecture/archi_perspectives/components/modules/mod_depend.html">模块依赖</a>
