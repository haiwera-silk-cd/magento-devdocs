---
group: b2b
subgroup: 10_REST
title: 与CompanyCredit模块集成
menu_title: 与CompanyCredit模块集成
menu_order: 17
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: credit
github_link: b2b/company-credit.md
functional_areas:
  - B2B
  - Integration
---

公司信用帐户允许公司成员使用信用购买产品。这是{{site.data.var.b2b}}特有的特性，仅用于公司间的业务。销售者分配金额(或信用度)到一个公司，然后公司成员可以使用这个金额作为支付来购买产品。信用额用于公司线下寄送给销售者。然后销售者在系统中创建一个报销事务来调整该公司的余额。

下面的图示说明了在帐号方式上使用这种支付方式的订单的流程

![信用支付]({{ page.baseurl }}/b2b/images/payment-on-credit.png)

## 相关信息

[管理公司信用帐户]({{ page.baseurl }}/b2b/credit-manage.html)
