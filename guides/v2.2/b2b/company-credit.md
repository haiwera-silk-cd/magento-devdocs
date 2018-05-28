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

公司信用帐户 allows company members to purchase items on credit. This is a feature specific to {{site.data.var.b2b}} that is used only for transactions between companies. The seller allocates an amount (or the credit limit) to a company and then company members can purchase items using this amount with the Payment on Account method. The credit amount used by a company is sent to the seller offline. Then the seller creates a Reimburse transaction in the system to adjust the company balance.

The following diagram illustrates the process flow of orders using the Payment on Account method.

![Payment on credit]({{ page.baseurl }}/b2b/images/payment-on-credit.png)

## Related information

[管理公司信用帐户]({{ page.baseurl }}/b2b/credit-manage.html)
