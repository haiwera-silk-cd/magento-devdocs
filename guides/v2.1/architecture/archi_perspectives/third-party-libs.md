---
group: arch-guide
subgroup: Logical View
title: 第三方库
menu_title: 第三方库
menu_order: 5
version: 2.1
github_link: architecture/archi_perspectives/third-party-libs.md
redirect_from: /guides/v1.0/architecture/archi_perspectives/third-party-libs.html
---

Magento依赖一系统的外部库，你可以使用{% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %}来管理这些依赖。Composer下载所有的被它自己主配置文件包含的外部库并安装它们到它的默认安装目录(`vendor/`)中.第三方库包括Zend框架及Symfony的库

有一些请求的Composer没有加载的库，它们被放在`lib/`下且包含{% glossarytooltip 312b4baf-15f7-4968-944e-c814d53de218 %}JavaScript{% endglossarytooltip %}库 (它们不被Composer加载)，而且有一些{% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %}库。(你也可以使用Composer来管理Magento不同组件之间依赖)

如果你正在扩展你的Magento{% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网站前台{% endglossarytooltip %}来和第三方应用交互，你可能须要去引入额外的库。这些外部的库可以像包裹一样简单。包裹了你正在集成到你的Magento网店的第三方产品的API或一个完整的框架
