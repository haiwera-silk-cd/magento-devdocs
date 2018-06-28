---
group: arch-guide
subgroup: 架构基础
title: 全局可扩展的特性
menu_title: 全局可扩展的特性
menu_node:
menu_order:
version: 2.1
github_link: architecture/global_extensibility_features.md
---

## 概述

必要的质量在完整的Magento组件中促进可扩展性，本节讨论关注：

* 模块化
* 依赖流行的设计模式
* 编码规范
* 灵活的属性类型
* Web APIs
* 服务契约和{% glossarytooltip 2be50595-c5c7-4b9d-911c-3bf2cd3f7beb %}依赖注入{% endglossarytooltip %}
* 插件

### 模块化

<i>模块</i>的概念是Magento{% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}扩展{% endglossarytooltip %}开发的核心，并且模块化的软件组件(特别地, 模块, 主题, 及语言包)设计是产品的核心架构原则，离散代码的独主的模块是以特征组织在一起的。由此减少每个模块外部的依赖。

如果一个{% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}是独立的，你可以在不引响其它地方代码码的情况下修改和替换它。这种软件组件间的<i>松藕合</i>减少了你在基础代码上修改其间的影响

 参考<a href="{{ page.baseurl }}/extension-dev-guide/bk-extension-dev-guide.html">PHP开发文档</a>了解更多关于如何创建模块的细节。

### 依赖流行的设计模式

依赖于已知的架构和编程结构有助于{% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %}开发者在特定的产品生态中定位影响编码的特殊的产品问题。对于新的Magento开发都来说这可以减小学习曲线。

设计模式是经的住时间考验的，广泛地识别了软件架构的结构。Magento产品架构由许多好的已知的模式组成，但扩展开发者应对模型-视图-控制器(MVC)模式有特别的兴趣。

### 编码规范

Magento开发者应该使他们自己熟知我们的编码规范、最佳实践和习惯，特别是PHP文件的格式、编码风格和文件命名习惯的规范。Magento规范是基于Zend框架编码规范的。

参考<a href="{{ page.baseurl }}/coding-standards/bk-coding-standards.html">编码规范</a>了解指南和要求

### 丰富的产品生态

更广的Magento生态提供了一个扩展社区及丰富的第三方扩展市场，访问[Magento市场](https://marketplace.magento.com/)了解可以下载的模块和主题的概述及购买为你扩展{% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网站前台{% endglossarytooltip %}提供更多可能性的模块和{% glossarytooltip d2093e4a-2b71-48a3-99b7-b32af7158019 %}主题{% endglossarytooltip %}

### 灵活的属性类型

你可以增强你的网店前台通过添加惟一属性到默认产品属性中，你可能须要添加新的属性来描述一个产品，如材质或行业特定的评级。你可以Magento管理员添加这些属性，让前通台展示。

<table>
   <tbody>
      <tr style="background-color: lightgray">
         <th>属性类型</th>
         <th>是否前台显示</th>

      </tr>
<tr>
         <td>EAV
         </td>
         <td>否</td>
         </tr>

         <tr>
         <td>自定义
         </td>
         <td>是</td>
         </tr>
         <tr>
         </td>扩展
         </td>
         <td>否</td>
         </tr>


</tbody>
</table>

属性类型归于三大类:

* <b>EAV(实体属性值)属性</b>是站点特定的属性，你可以使用{% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento管理面板{% endglossarytooltip %}为你的本地站点定义它

* <b>自定义属性</b>是一个EAV的子集，使用EAV属性的对象存储这些属性值在几个MySQL表中，顾客和{% glossarytooltip 8d40d668-4996-4856-9f81-b1386cf4b14f %}产品目录{% endglossarytooltip %}模块使用EAV属性

* <b>扩展属性</b>通常用比自定义属性更复杂的数据类型，这些属性不会出现在网店前台，扩展属性由模块引入。

参考<a href="{{ page.baseurl }}/extension-dev-guide/bk-extension-dev-guide.html">PHP开发文档</a>了解更多关于使用属性的信息。

### Web APIs

Magento或第三方服务可被配置成一个象web{% glossarytooltip 786086f2-622b-4007-97fe-2c19e5283035 %}API{% endglossarytooltip %} (REST的SOAP)的一些简单的{% glossarytooltip 8c0645c5-aa6b-4a52-8266-5659a8b9d079 %}XML{% endglossarytooltip %}。你可以使用这些服务来集成你的Magento到第三方应用中去，像CRM(客户关系管理系统)或ERP(企业资源规划系统)的后系统，以及{% glossarytooltip f3944faf-127e-4097-9918-a2e9c647d44f %}CMS{% endglossarytooltip %}（内容管理系统）.

参考<a href="{{ page.baseurl }}/get-started/bk-get-started-api.html">Magento web API起步</a>了解更多

### 服务契约, 依赖注入和依赖倒置

<i>服务契约</i>提供了一个新的方式访问公共API接口。这些php接口提供健壮的、稳定的扩展点给到客户端来连接。服务契约定义了和模块公共API起相同作用的接口。定义这些接口是添加模块非常必要的一部分。

服务契约在整个Magento文档中被反复讨论。参考<a href="{{ page.baseurl }}/architecture/archi_perspectives/service_layer.html">服务层</a>了解高层介绍。参考<a href="{{ page.baseurl }}/extension-dev-guide/bk-extension-dev-guide.html">PHP开发文档</a>了解服务契约和依赖注入更多细节的讨论。

Magento随关服务契约实现<i>依赖注入</i>，依赖注入提供一种机制，改变模块的行为而不须要修改客户端，也不须要理解实现的细节。依赖注入及相关的概念*依赖倒置*支撑Magento的基本架构原则，模块化和易于扩展。它们非常鼓励支持软件模块松藕合的基础代码实践。

参考<a href="{{ page.baseurl }}/extension-dev-guide/bk-extension-dev-guide.html">PHP开发文档</a>了解更多关于依赖注入和服务契约的信息。

### 插件

插件，类似模块，是一个为添加特性到Magento核心行为中的机制。插件允许你改变Magento类中任何公有方法的行为。你可以考虑它是一种使用`插件`类形式的扩展。

插件也被称为<i>拦截器</i>。应用程序使用{% glossarytooltip 9fceecbe-31be-4e49-aac7-11d155a85382 %}插件{% endglossarytooltip %}模式来改变方法的形为，而不修改实际的类。插件或以在原方法执行过程的之前和之后插入要执行的方法，或仅在原方法抛异常时执行

参考<a href="{{ page.baseurl }}/extension-dev-guide/bk-extension-dev-guide.html">PHP开发文档</a>中的<a href="{{ page.baseurl }}/extension-dev-guide/plugins.html">插件</a>了解更多优先考虑插件和声明插件的信息

### 相关主题 {#m2arch-related}

<a href="{{ page.baseurl }}/architecture/extensibility.html">可扩展和模块化</a>
