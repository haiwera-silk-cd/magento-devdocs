---
group: howdoi
subgroup:
title: 自定义结算页
menu_title: 自定义结算页
menu_node: parent
menu_order: 1
version: 2.0
github_link: howdoi/checkout/checkout_overview.md
functional_areas:
  - Checkout
---

### Default checkout overview

Magento {% glossarytooltip 278c3ce0-cd4c-4ffc-a098-695d94d73bde %}checkout{% endglossarytooltip %} is implemented using the [UI components](http://devdocs.magento.com/guides/v2.1/ui_comp_guide/bk-ui_comps.html).
Out of the box, the checkout consists of two steps:

 - Shipping Information
 - Review and Payment Information

The checkout totals and the corresponding side-bar are only displayed after the first step is completed.

The only {% glossarytooltip 53da11f1-d0b8-4a7e-b078-1e099462b409 %}exception{% endglossarytooltip %} is checkout of virtual and/or downloadable products: if there are only these  types of products in the shopping cart, checkout is automatically transformed to one-step procedure, because shipping information is not required.

### List of described customizations
You can customize the default checkout in many ways. Here the following customizations are described:

 - [添加一个结算步骤]({{ page.baseurl }}/howdoi/checkout/checkout_new_step.html)
 - [自定义已存在步骤的视图]({{ page.baseurl }}/howdoi/checkout/checkout_customize.html)
 - [为结算添加自定义的支付方式]({{ page.baseurl }}/howdoi/checkout/checkout_payment.html)
 - [添加提交前自定义数据校验]({{ page.baseurl }}/howdoi/checkout/checkout_order.html)
 - [添加自定义物流校验]({{ page.baseurl }}/howdoi/checkout/checkout_carrier.html)
 - [为邮编添加自定义掩码]({{ page.baseurl }}/howdoi/checkout/checkout_zip.html)
 - [在结算页为表单输入添加自定义模板]({{ page.baseurl }}/howdoi/checkout/checkout_edit_form.html)
 - [添加一个新的输入表单到结算页]({{ page.baseurl }}/howdoi/checkout/checkout_form.html)
 - [添加一个新的输入项到地址表单]({{ page.baseurl }}/howdoi/checkout/checkout_new_field.html)
 - [添加自定义运送地址渲染器]({{ page.baseurl }}/howdoi/checkout/checkout_address.html)

For the sake of compatibility, upgradability, and easy maintenance, do not edit the default Magento code, add your customizations in a custom {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}.
