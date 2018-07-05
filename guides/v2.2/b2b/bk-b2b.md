---
group: b2b
subgroup: 01_Introduction
title: B2B开发者文档
landing-page: B2B
menu_title: B2B开发者文档
menu_order: 1
menu_node: parent
version: 2.2
ee_only: True
github_link: b2b/bk-b2b.md
functional_areas:
  - B2B
  - Integration
---

不像标准的B2C模型，{{site.data.var.b2b}} (B2B)被设计成商议销售者所需的模式，他们的客户主要是公司，他们有着复杂的组织结构及多用户、多角色，不同权限级别

B2B模型中有两种基本的角色

* **销售者** 是一个管理员用户，他可以访问Magento的管理面板。
* **购买者** 是任意一个关联到一个公司账户的客户，它可以访问网店前台。

公司组件是B2B中关键的实体，所有其他的特征都在一些方面依赖了它。这允许加入多个同一公司的购买者到一个公司的账户(或合作账户)下。公司的管理员能够构建公司结构(分级部门，细分部门及用户)为一个适当的等级结构，并提拱不同的用户角色和权限到公司的成员。这样一个等级结构允许允许公司管理员控制账户下的成员的活动：下单、报价、购买及访问信息卡账户和其它账号信息等。除此之外，一个销售可以配置如何与购买公司在站点上合作：包括支付方式、定价级别，议价能力和创建需求列表的能力。

公司有可选的支付账户，换句话说，能使用信用购买。销售者分配信用额度到公司账户并且管理它们的信用设置及信用报销。

共享的产品目录是分级定价的，允许在一个或多个站点为每个产品不同公司设置自定义的价格。使用共享产品目录，销售者可以为不同的客户群应用不同的价格级别来进行销售。

销售者和代表一个公司的购买者能在定单确认前商议订单的价格。此功能在议价模块完成。这意味着在生成一个定单前，购买者可以对销售者的定价和折扣发起议价。商议暗示着创建的报价可能在转化成定单前被提交、审查和修改。

## B2B模块

{{site.data.var.b2b}}是一个被安装在{{site.data.var.ee}}之上的模块集。以面的表格列出了B2B担供的模块。

名称 | 描述 | 能否使用WebAPI?
--- | --- | ---
B2b | B2B基础模块，也提供品牌元素。 | 否
BundleNegotiableQuote | 允许在B2B环境中归拢产品展示在议价中 | 否
BundleRequisitionList | 允许归拢产品展示在需求列表中 | 否
BundleSharedCatalog | 允许在B2B环境中归拢产品添加到共享产品目录中 | 否
Company | 允许销售者创建一个公司账户和分配多个公司成员到这个账户 | 是
CompanyCredit | 为B2B的公司添加支付到账户支付方式| 是
CompanyPayment | 允许销售者配置哪一种支付方式对B2B公司是有效的 | 否
ConfigurableNegotiableQuote | 允许在B2B环境中将可配置的产品显示到议价中 | 否
ConfigurableRequisitionList | 允许可配置的产品显示到需求列表中 | 否
ConfigurableSharedCatalog |允许在B2B环境中将可配置的产品添加到共享目录中 | 否
GiftCardNegotiableQuote | 允许在B2B环境中将礼品卡显示到议价中 | 否
GiftCardRequisitionList | 允许将礼品卡显示到需求列表中 | 否
GiftCardSharedCatalog | 允许在B2B环境将礼品卡添加到共享产品目录中 | 否
GroupedSharedCatalog | 允许在B2B环境将分组的产品添加到共享目录中 | 否
NegotiableQuote | 允许购买者和销售者(管理员用户)在定单确认前商议产品或物流价格| 是
NegotiableQuoteSharedCatalog | 允许B2B环境中`NegotiableQuote`和`SharedCatalog`模块交互 | 否
QuickOrder | 允许购买者用多个Sku的列表创建一个新的订单 | 否
RequisitionList | 允许购买者创建经常购买项的多列表及使用这些列表来下单。 | 否
SharedCatalog | 为不同公司的账号定义产品及价格在产品目录和B2B报价中的可见性 | 是

## 相关信息
* [安装B2B扩展]({{ page.baseurl }}/comp-mgr/install-extensions/b2b-installation.html)
* [起步 with {{site.data.var.b2b}}](http://docs.magento.com/m2/b2b/user_guide/getting-started.html)
