---
group: payments-integrations
subgroup: A_gateway
title: 支付提供商网关结构
menu_title: 支付提供商网关结构
menu_order: 1
version: 2.0
github_link: payments-integrations/payment-gateway/payment-gateway-structure.md
redirect_from: guides/v2.0/payment-gateway/payment-gateway-stucture.html
---

The following diagram shows the basic 组件 of the Magento支付提供商网关:

![Payment Gateway Structure]({{ site.magentourl }}/common/images/payments-integrations/pg_structure.png)

The interaction between the {% glossarytooltip 5b963536-8f03-45c4-963b-688021f4eea7 %}payment gateway{% endglossarytooltip %} 组件 looks like following:

![Payment Gateway Structure]({{ site.magentourl }}/common/images/pg_internal_flow.png)

Each component from this scheme is described in the corresponding topic:

* [网关命令]({{ page.baseurl }}/payments-integrations/payment-gateway/gateway-command.html)
* [网关命令池]({{ page.baseurl }}/payments-integrations/payment-gateway/command-pool.html)
* [请求构造器]({{ page.baseurl }}/payments-integrations/payment-gateway/request-builder.html)
* [网关客户端]({{ page.baseurl }}/payments-integrations/payment-gateway/gateway-client.html)
* [响应校验器]({{ page.baseurl }}/payments-integrations/payment-gateway/response-validator.html)
* [响应处理器]({{ page.baseurl }}/payments-integrations/payment-gateway/response-handler.html)




