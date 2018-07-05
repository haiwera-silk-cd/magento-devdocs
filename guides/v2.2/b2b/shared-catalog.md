---
group: b2b
subgroup: 10_REST
title: 与ShareCatalog模块集成
menu_title: 与ShareCatalog模块集成
menu_order: 21
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: shared
github_link: b2b/shared-catalog.md
functional_areas:
  - B2B
  - Catalog
  - Integration
---

共享产品目录是一个允许销售者为公司用户(购买者)购买产品设置特定规则的实体。使用共享产品目录，销售者可以给不同的公司应用不同的价格级别。也允许销售者为不同公司配置特定分类和产品的可见性。

产品和分类不是创建或储存在共享产品目录，产品仍在主产品目录上。（主产品目录是指Magento标准的产品目录，只有销售者可以看到),分类在分类页面创建，销售者决定一个分类是否被显示在每一个共享产品目录中。

自定义的产品目录只可以被分配给公司。它们不能被分配给用户本身。公司只能被分配在一个共享产品目录下。

{{site.data.var.b2b}} 提供两种类型的共享产品目录：公共的和自定义的。公共的产品目录是默认的共享产品目录，它自动展示给所有不是公司用户的游客和未登录的顾客，虽然公司可以被分配到公共共享产品目录，销售者也分配一个自定义的共享产品目录到指定的公司。只能有一个公共共享产品目录，并且它不能被删除。

## 相关信息

* [管理共享类目录]({{ page.baseurl }}/b2b/shared-cat-manage.html)
* [分配分类和产品]({{ page.baseurl }}/b2b/shared-cat-product-assign.html)
* [分配公司]({{ page.baseurl }}/b2b/shared-cat-company.html)
* [管理多产品价格]({{ page.baseurl }}/rest/catalog-pricing.html)
