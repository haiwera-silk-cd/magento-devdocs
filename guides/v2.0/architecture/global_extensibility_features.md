---
group: arch-guide
subgroup: 架构基础
title: 全局可扩展的特性
menu_title: 全局可扩展的特性
menu_node:
menu_order:
version: 2.0
github_link: architecture/global_extensibility_features.md
---

## 概述

Essential qualities foster extensibility throughout the entire set of Magento组件. This discussion focuses on:

* 模块化
* Reliance on popular design patterns
* Coding standards
* Flexible attribute types
* Web APIs
* 服务契约 and {% glossarytooltip 2be50595-c5c7-4b9d-911c-3bf2cd3f7beb %}依赖注入{% endglossarytooltip %}
* Plug-ins

### Modularity

The concept of the <i>module</i> is the heart of Magento {% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}扩展{% endglossarytooltip %} development, and modular design of software 组件 (in particular, modules, themes, and language packages) is a core architectural principle of the product. Self-contained modules of discrete code are organized by feature, thereby reducing each module's external dependencies.

If a {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %} is self-contained, then you can modify or replace it without affecting other areas of the code. This <i>loose coupling</i> of software 组件 reduces the ripple effects throughout your code base of changing code.

 See the <a href="{{ page.baseurl }}/extension-dev-guide/bk-extension-dev-guide.html">PHP开发文档</a> for detailed instructions on how to create modules.

### Reliance on popular design patterns

Reliance on known architectural and programming structures helps {% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %} developers orient themselves to the specific development issues that affect coding in a particular product ecosystem. This can reduce the learning curve for new Magento developers.

Design patterns are time-tested, widely recognized software architecture constructs. Magento product architecture incorporates many well known patterns, but Model-View-Controller (MVC) holds particular interest for extension developers.

### 编码规范

Magento developers should familiarize themselves with our coding standards, best practices, and conventions, especially standards for PHP file formatting, coding style, and file naming conventions. Magento standards are based on Zend Framework 编码规范.

See <a href="{{ page.baseurl }}/coding-standards/bk-coding-standards.html">编码规范</a> for guidelines and requirements.

### Rich product ecosystem

The wider Magento ecosystem provides an extensive community and rich third-party marketplace for extensions. Visit [Magento Marketplace](https://marketplace.magento.com/) for an overview of the many modules and themes available for download and to buy modules and {% glossarytooltip d2093e4a-2b71-48a3-99b7-b32af7158019 %}主题{% endglossarytooltip %} packages, which offer more possibilities for extending your {% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网站前台{% endglossarytooltip %}.

### Flexible attribute types

You can enhance your storefront by adding unique attributes to the default product attributes. For example, you might need to add a new attribute to describe a product, such as texture or an industry-specific rating. You can add these attributes from the Magento Admin, and the storefront  displays them.

<table>
   <tbody>
      <tr style="background-color: lightgray">
         <th>Attribute type</th>
         <th>Displayed by storefront?</th>

      </tr>
<tr>
         <td>EAV
         </td>
         <td>否</td>
         </tr>

         <tr>
         <td>Custom
         </td>
         <td>yes</td>
         </tr>
         <tr>
         <td>Extension
         </td>
         <td>否</td>
         </tr>


</tbody>
</table>

Attribute types fall into three general categories:

* <b>EAV (Entity-Attribute-Value) attributes</b> are site-specific attributes that you can define for a local site using the {% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento管理面板{% endglossarytooltip %}.

* <b>Custom attributes</b> are a subset of EAV attributes. Objects that use EAV attributes typically store values in several MySQL tables. The Customer and {% glossarytooltip 8d40d668-4996-4856-9f81-b1386cf4b14f %}Catalog{% endglossarytooltip %} modules use EAV attributes.

* <b>Extension attributes</b> often use more {% glossarytooltip fd9ae55f-ccf5-480b-a7f3-bd2c80f0b2a4 %}complex data{% endglossarytooltip %} types than custom attributes. These attributes do not appear in the storefront. Extension attributes are introduced by modules.

See <a href="{{ page.baseurl }}/extension-dev-guide/bk-extension-dev-guide.html">PHP开发文档</a> for information about using attributes.

### Web APIs

Magento or third-party services can be configured as a web {% glossarytooltip 786086f2-622b-4007-97fe-2c19e5283035 %}API{% endglossarytooltip %} (REST or SOAP) with some simple {% glossarytooltip 8c0645c5-aa6b-4a52-8266-5659a8b9d079 %}XML{% endglossarytooltip %}. You can use these services to integrate your Magento installation into third-party applications, such as CRM (Customer Relationship Management), ERP (Enterprise Resource Planning) back office systems, and {% glossarytooltip f3944faf-127e-4097-9918-a2e9c647d44f %}CMS{% endglossarytooltip %} (Content Management Systems).

See <a href="{{ page.baseurl }}/get-started/bk-get-started-api.html">Magento web API起步</a> for more information.

### 服务契约, dependency injection, and dependency inversion

<i>服务契约</i> provide a new way to access public API endpoints. These PHP interfaces offer robust, stable extension points to which clients can connect.  服务契约 define the endpoints that function as a module's public API. Defining these endpoints is an essential part of adding a module.

服务契约 are discussed throughout the Magento documentation set. See <a href="{{ page.baseurl }}/architecture/archi_perspectives/service_layer.html">服务层</a> for a high-level introduction. See <a href="{{ page.baseurl }}/extension-dev-guide/bk-extension-dev-guide.html">PHP开发文档</a> for a more detailed discussion of service contracts and dependency injection.

Magento implements <i>dependency injection</i> along with service contracts. 依赖注入 provides a mechanism for changing a module's behavior without altering the client or understanding nitty-gritty details of implementation. Both dependency injection and its related concept *dependency inversion* support Magento's fundamental architectural principles of modularity and ease-of-extensibility. They strongly encourage basic coding practices that support the loose coupling of software modules.

See <a href="{{ page.baseurl }}/extension-dev-guide/bk-extension-dev-guide.html">PHP开发文档</a> for information on both dependency injection and service contracts.

### Plug-ins

Plug-ins, like modules, are a mechanism for adding features to the core Magento product. Plug-ins enable you to make changes to the behavior of any public method in a Magento class. You can consider it a form of extension that uses the `Plugin` class.

Plug-ins are also called <i>interceptors</i>. Applications use the {% glossarytooltip 9fceecbe-31be-4e49-aac7-11d155a85382 %}plug-in{% endglossarytooltip %} pattern to change method behavior without modifying the actual class. Plug-ins can typically intercept method processing before or after the method runs, or only when the method throws an {% glossarytooltip 53da11f1-d0b8-4a7e-b078-1e099462b409 %}exception{% endglossarytooltip %}.

See <a href="{{ page.baseurl }}/extension-dev-guide/plugins.html">Plug-ins</a> in <a href="{{ page.baseurl }}/extension-dev-guide/bk-extension-dev-guide.html">PHP开发文档</a> for information on declaring and prioritizing plug-ins.

### 相关主题 {#m2arch-related}

<a href="{{ page.baseurl }}/architecture/extensibility.html">可扩展和模块化</a>
