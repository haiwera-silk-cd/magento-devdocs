---
group: arch-guide
subgroup: Components
title: 模块概述
menu_title: 模块概述
menu_order: 3
level3_menu_node: level3child
level3_subgroup: modules
version: 2.1
github_link: architecture/archi_perspectives/components/modules/mod_intro.md
redirect_from:
  - /guides/v1.0/architecture/modules/mod_intro.html
  - /guides/v2.0/architecture/modules/mod_intro.html
---

## Magento模块是什么？ {#arch-modules-overview}

<i>模块</i>是一个逻辑组--是一个包含了显示区块类、控制器、助手类、模型的目录 -- 同一个特定业务特征相关的。为遵守Magento的规范达到最优模块化，{% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}应囊括了一个特性且和其它模块有尽可能少的依赖

模块和主题都是Magento可定制化的单元。模块使用支撑逻辑提供了业务特性，而主题全方位的影响用户体验及{% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网店前台{% endglossarytooltip %}的显示。这两个组件都有一个生命周期，允许它们被安装、删除、及禁用。从商人和{% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}扩展{% endglossarytooltip %}开发者的视角来看，模块是Magento组织的核心单元。

Magento框架提供了一套核心逻辑: {% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %}代码，库，以及可以被模块和其它逻辑继承的基本方法。

## 模块的目的

每个模块的目的是实现新的功能或扩展其它模块的功能以提供特定产品特性。每个模块被设计成独立的，如此，引入或排出一个特定模块不至于影响到其它模块的功能。

## 模块组件

模块是一个目录，有某个业务特性相关的PHP和{% glossarytooltip 8c0645c5-aa6b-4a52-8266-5659a8b9d079 %}XML{% endglossarytooltip %}文件(区块类，控制器，助手类，模型)，如Magento的Shipping模块，它由以下软件组件组成：<a href="{{ page.baseurl }}/frontend-dev-guide/themes/theme-overview.html">themes</a>, <a href="{{ page.baseurl }}/architecture/archi_perspectives/third-party-libs.html">libraries</a>,以及<a href="{{ page.baseurl }}/frontend-dev-guide/translations/xlate.html#m2devgde-xlate-languagepack">language packages</a>.

## 模块存放在哪？

典型地，存放在magento安装目录的`vendor`目录下，以以下的PSR-0规范的格式：`vendor/<vendor>/<type>-<module-name>`, `<type>`可以是以下值:
 - **`module`** - 表示模块 (`module-customer-import-export`)
 - **`theme`** - 表示前台或管理面板的主题 (`theme-frontend-luma`或`theme-adminhtml-backend`)
 - **`language`** - 表示语言包 (`language-de_de`)

例如，Magento客户导入/导出模块定义在 `vendor/magento/module-customer-import-export`.

但如果你要创建一个新的模块，你仅能创建`app/code/<vendor>/<type>-<module-name>`目录和它里面的所需的目录。

在目录中，你可以找到所有这个模块的代码，包括定义此模块名称、版本以及所有依赖项的`etc/module.xml`文件。

## 使用模块开发

Magento开发者，管理员及任何构建了Magento站点的人，想要了解自已特定目的和用例所有相关的主题。

参考<a href="{{ page.baseurl }}/extension-dev-guide/bk-extension-dev-guide.html">PHP开发文档</a>了解扩展模块的特定用法说明。


参考<a href="{{ page.baseurl }}/frontend-dev-guide/bk-frontend-dev-guide.html">前端工程师手册</a>了解实现主题和其它组件的相关

## 相关主题 {#arch-modules-related}

<a href="{{ page.baseurl }}/architecture/archi_perspectives/components/modules/mod_depend.html">模块依赖</a>

<a href="{{ page.baseurl }}/architecture/archi_perspectives/components/modules/mod_and_areas.html">模块和地区</a>

<a href="{{ page.baseurl }}/architecture/archi_perspectives/components/modules/mod_conventions.html">模块位置和命名习惯</a>
