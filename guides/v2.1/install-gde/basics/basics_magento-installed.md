---
group: install2
subgroup: 起步
title: 我的Magento有装好吗？
menu_title: 我的Magento有装好吗？
menu_node:
menu_order: 101
level3_menu_node: level3child
level3_subgroup: basics
version: 2.1
github_link: install-gde/basics/basics_magento-installed.md
redirect_from: /guides/v1.0/install-gde/basics/basics_magento-installed.html
functional_areas:
  - Install
  - System
  - Setup
---

要判定你的Magento是否已经安装好，你可以用浏览器访问{% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento管理面板{% endglossarytooltip %}(管理控制台)或者直接打开{% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}你的网站前台{% endglossarytooltip %}.

**先决条件**: 你必须知道你的服务器的IP地址或主机名，以及访问Magento安装页面的{% glossarytooltip a05c59d3-77b9-47d0-92a1-2cbffe3f8622 %}URL{% endglossarytooltip %}，如果你不知道，请询问你的系统管理员或主机提供商.

然后用浏览器打开这个URL，例如

	http://www.example.com/magento2/admin
	https://www.example.com/admin
	http://www.example.com

如果显示是404 (未找到), 那么Magento可能没有正确安装. 你可以找你的系统管理员或主机提商确认.

如果Magento正确安装了，你登录之后看到的应方是这样的:

Magento管理面板:

<p><img src="{{ site.magentourl }}/common/images/install_success_admin.png" alt="正确安装了的Magento管理面板"></p>


Magento storefront:

<p><img src="{{ site.magentourl }}/common/images/install-success_store.png" alt="正确安装了的Magento商城"></p>

## 安装好了之后呢?

如果Magento已经装好了，并且你想要管理和升级它的组件，你可以查阅下面的文档：

*	<a href="{{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html">组件管理手册</a>

	一个Magento组件是一个扩展、语言包或是一个主题，组件管理器负责安装、卸载、更新、启用和禁用组件。
	
*	<a href="{{ page.baseurl }}/comp-mgr/upgrader/upgrade-start.html">升级向导</a>

	升级Magento软件或组件。
