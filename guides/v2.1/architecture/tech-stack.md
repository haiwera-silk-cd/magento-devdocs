---
group: arch-guide
subgroup: 架构基础
title: 技术栈
menu_title: 技术栈
menu_order: 2
version: 2.1
github_link: architecture/tech-stack.md
redirect_from: /guides/v1.0/extension-dev-guide/tech-stack.html
---

## 概述

 本章总结了我们使用的技术，更多详细信息，请参考[系统要求]({{ page.baseurl }}/install-gde/system-requirements-tech.html).

Magento的高度模块化结构包含以下开源技术。

### Web服务

*	Apache
*	{% glossarytooltip b14ef3d8-51fd-48fe-94df-ed069afb2cdc %}nginx{% endglossarytooltip %}

### PHP

*	{% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %} (dependency management package for PHP)

### Database

*	MySQL
*	MySQL Percona

### HTTP加速器

*	Varnish

### 缓存存储

*	Redis
*	Memcache

### Search

* Solr (仅Magento企业版)
* Elasticsearch (仅Magento企业版2.1.x)

### 其它技术

*	HTML5
*	CSS3 (LESS {% glossarytooltip 6c5cb4e9-9197-46f2-ba79-6147d9bfe66d %}CSS{% endglossarytooltip %} pre-processor)
*	{% glossarytooltip 5bfa8a8e-6f3e-4fed-a43e-62339916f02e %}jQuery{% endglossarytooltip %} (primary {% glossarytooltip 312b4baf-15f7-4968-944e-c814d53de218 %}JavaScript{% endglossarytooltip %} library)
*	RequireJS (帮助按需加载Javascript资源的库)
*	Knockout.js (简单的Javascript MVVM UI渲染库)
*	第三方库 (Zend Framework 1, Zend Framework 2, Symfony)
*	编码规范 PSR-0 (标准自动加载), PSR-1 (基础编码标准), and PSR-2 (编码风格指引), PSR-3, PSR-4

### 可选栈组件

*	Varnish (缓存)
*	Redis (用于页面缓存)
*	Solr (搜索引擎)
*	Elasticsearch (搜索引擎)

Magento is *compatible with but not supported* for:

*	HHVM 3.9 {% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %} interpreter

### 自动测试

Magento也提供了自动测试的工具箱，包含单元测试、集成测试、功能测试和性能测试脚本，以及Javascript测试和静态代码分析工具。组件包括单元测试的PHPUnit和功能测试框架的Selenium.

这些框架位于`dev/tests`目录。功能测试框架`mtf`可以在[单独的仓库](https://github.com/magento/mtf){:target="_blank"}中找到.
更多信息，请参考[功能测试框架]({{ page.baseurl }}/mtf/mtf_introduction.html)手册.

## 相关主题
<a href="{{ page.baseurl }}/architecture/archi_perspectives/ABasics_intro.html">架构基础</a>
