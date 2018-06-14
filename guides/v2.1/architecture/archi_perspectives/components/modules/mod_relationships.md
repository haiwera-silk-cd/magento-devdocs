---
group: arch-guide
subgroup: Components
title: 模块关系
menu_title: 模块关系
menu_order: 5
level3_menu_node: level3child
level3_subgroup: modules
version: 2.1
github_link: architecture/archi_perspectives/components/modules/mod_relationships.md
redirect_from:
  - /guides/v1.0/architecture/modules/mod_relationships.html
  - /guides/v2.0/architecture/modules/mod_relationships.html
---

## 概述 {#m2arch-module-relationships-overview}

理解一个{% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}如何与另一个模块连系，有助于确定模块中它是如何对改变起作用的

简单的模块和其它模块可以有以下类型的关系:

* **使用**: 如果模块A调用了模块B的行为，则它使用了模块B

* **起反应**: 模块A对模块B作出反应，当其行为它B的{% glossarytooltip c57aef7c-97b4-4b2b-a999-8001accef1fe %}event{% endglossarytooltip %}触发，但模块B并不知道有模块A。

* **定制**: 如果模块A修饰了模块B的行为，称A定制了B

* **实现**: 模块A实现了模块B中定义的一些行为，不必是所有行为。

* **替换**: 模块A替换模块B，是说它为模块B暴露和实现的{% glossarytooltip 786086f2-622b-4007-97fe-2c19e5283035 %}API{% endglossarytooltip %}提供了它自己的版本

## 关系类型和场景

### A使用B,C定制B

在模块A使用模块B并且模块C定制模块B的场景下，模块C的定制不能打断模块B的API，如此模块A在定制后仍能正常起作用

![模块关系场景:A使用B,C定制B]({{ site.magentourl }}/common/images/archi_first_relate.png)

### A对起作出反应，C定制B

类似地，在模块A对模块B起反应并且模块C定制模块B的情况下，模块C的定制不能干涉模块A依赖的模块B的事件。

![模块关系场景:A对起作出反应，C定制B]({{ site.magentourl }}/common/images/archi_second_relate.png)

### A和C都定制B

<p>如果模块A和C同时定制模块B,要当心它们的定制都被实现以避免冲突（参考如下）</p>

![模块关系场景:A和C都定制B]({{ site.magentourl }}/common/images/archi_third_relate.png)

### A替换B

如果模块A替换模块B，那么它须要能够以一种方式使其它模块不受影响，这意味着在模块B上没有直接的硬依赖，而是依赖于第三个模块，模块A和B都实现的模块C。

![模块关系场景:A替换B]({{ site.magentourl }}/common/images/archi_fourth_relate.png)

## 相关主题 {#m2arch-module-related}

<a href="{{ page.baseurl }}/architecture/archi_perspectives/components/modules/mod_intro.html">模块概述</a>
