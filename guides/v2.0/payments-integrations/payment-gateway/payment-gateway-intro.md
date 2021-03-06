---
group: payments-integrations
subgroup: A_gateway
title: Magento支付提供商网关
menu_title: Magento支付提供商网关 
menu_node: parent
menu_order: 1
version: 2.0
github_link: payments-integrations/payment-gateway/payment-gateway-intro.md

---

### What is Magento支付提供商网关
The Magento支付提供商网关 is a mechanism that allows you to integrate your stores with payment service providers. As a result, you can create and handle transactions based on order details.

The following diagram shows a simplified interaction flow between Magento sales management and external payment service provider using Magento支付提供商网关: 

![Payment Gateway Interaction]({{ site.magentourl }}/common/images/payments-integrations/pg_interaction_flow.png)

Magento payment provider supports the following payment operations:

 * authorize: process {% glossarytooltip 34ecb0ab-b8a3-42d9-a728-0b893e8c0417 %}authorization{% endglossarytooltip %} transaction; funds are blocked on customer account, but not withdrawn
 * sale: process authorization transaction and capture automatically, funds are withdrawn
 * capture: withdraw previously authorized amount
 * refund: return previously withdrawn customer funds
 * void: cancel transfer of funds from customer account

### What's in this chapter

The topics of this chapter are conceptual and describe the 组件 of the Magento支付提供商网关:
 
* [支付提供商网关结构]({{ page.baseurl }}/payments-integrations/payment-gateway/payment-gateway-structure.html)
* [网关命令]({{ page.baseurl }}/payments-integrations/payment-gateway/gateway-command.html)
* [网关命令池]({{ page.baseurl }}/payments-integrations/payment-gateway/command-pool.html)
* [请求构造器]({{ page.baseurl }}/payments-integrations/payment-gateway/request-builder.html)
* [网关客户端]({{ page.baseurl }}/payments-integrations/payment-gateway/gateway-client.html)
* [响应校验器]({{ page.baseurl }}/payments-integrations/payment-gateway/response-validator.html)
* [响应处理器]({{ page.baseurl }}/payments-integrations/payment-gateway/response-handler.html)

#### Terms used {#terms}

<table>
<tr>
<th>
Term
</th>
<th>
Description
</th>
</tr>
<tr>
<td>
<i>Magento sales management</i>
</td>
<td>
Magento interfaces that provide the ability to create orders, invoices, and shipments.
</td>
</tr>
<tr>
<td>
<i>Payment service provider, payment provider, payment processor</i>
</td>
<td>
 Online service for accepting electronic payments, like PayPal, Authorize.Net and so on.
</td>
</tr>
<tr>
<td>
<i>Payload</i>
</td>
<td>
Data used for a transaction. Might include the following:

<ul>
<li> payment details </li>
<li> order items </li>
<li> shipping, billing addresses </li>
<li> customer details </li>
<li> taxes </li>
<li> merchant's payment provider {% glossarytooltip 786086f2-622b-4007-97fe-2c19e5283035 %}API{% endglossarytooltip %} credentials </li>
</ul>
</td>
</tr>
</table>


