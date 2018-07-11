---
group: payments-integrations
subgroup: A_gateway
title: 网关命令
menu_title: 网关命令 
menu_node: 
menu_order: 2 
version: 2.1
github_link: payments-integrations/payment-gateway/gateway-command.md
---

网关命令 is a component of the Magento {% glossarytooltip 5b963536-8f03-45c4-963b-688021f4eea7 %}payment gateway{% endglossarytooltip %} that takes the [payload]({{ page.baseurl }}/payments-integrations/payment-gateway/payment-gateway-intro.html#terms) required for a particular payment provider and sends, receives, and processes the provider's response. 
For each operation (authorization, capture and so on) of a certain payment provider - a separate gateway command is added.

## Interface
Basic interface for a gateway command is [`\Magento\Payment\Gateway\CommandInterface`]({{ site.mage2000url }}app/code/Magento/Payment/Gateway/CommandInterface.php). It implements the [Command design pattern](http://designpatternsphp.readthedocs.io/en/latest/Behavioral/Command/README.html).

## Basic implementation

The `\Magento\Payment\Gateway\Command\GatewayCommand` class is the default `CommandInterface` implementation. It allows performing most of the operations implemented in the [Magento sales management]({{ page.baseurl }}/payments-integrations/payment-gateway/payment-gateway-intro.html#terms).

## Adding gateway commands
For each particular integration with a payment provider, gateway commands are added using virtual types in [dependency injection (DI)]({{ page.baseurl }}/extension-dev-guide/depend-inj.html) configuration.

In the following example the `BraintreeAuthorizeCommand` gateway command is added. The command implements the "authorize" operation for the Braintree payment provider ([`app/code/Magento/Braintree/etc/di.xml#131`]({{ site.mage2100url }}app/code/Magento/Braintree/etc/di.xml#L131)):

{% highlight xml %}
<virtualType name="BraintreeAuthorizeCommand" type="Magento\Payment\Gateway\Command\GatewayCommand">
    <arguments>
        <argument name="requestBuilder" xsi:type="object">BraintreeAuthorizeRequest</argument>
        <argument name="transferFactory" xsi:type="object">Magento\Braintree\Gateway\Http\TransferFactory</argument>
        <argument name="client" xsi:type="object">Magento\Braintree\Gateway\Http\Client\TransactionSale</argument>
        <argument name="handler" xsi:type="object">BraintreeAuthorizationHandler</argument>
        <argument name="validator" xsi:type="object">Magento\Braintree\Gateway\Validator\ResponseValidator</argument>
    </arguments>
</virtualType>
{% endhighlight %}

(The code sample is from {{site.data.var.ce}} v2.1. Although the payment provider gateway was added in v2.0, the particular default implementation using the gateway were added in v2.1)

A gateway command must be configured with the following arguments:

* `requestBuilder`: [request builder]({{ page.baseurl }}/payments-integrations/payment-gateway/request-builder.html), builds an array of provider-specific arguments using the order information. 

* `transferFactory`: [transfer factory]({{ page.baseurl }}/payments-integrations/payment-gateway/gateway-client.html#transfer_factory), creates transfer object from request data, which will be used by 网关客户端 to process requests. For details see [网关客户端 #Transfer Factory]({{ page.baseurl }}/payments-integrations/payment-gateway/gateway-client.html#transfer_factory)

* `client`: [gateway client]({{ page.baseurl }}/payments-integrations/payment-gateway/gateway-client.html), takes the provider-specific arguments and performs a low-level call to the provider.

Optional arguments :

* `handler`: [response handler]({{ page.baseurl }}/payments-integrations/payment-gateway/response-handler.html), changes the order and payment status depending on the payment provider response. 
* `validator`: [response validator]({{ page.baseurl }}/payments-integrations/payment-gateway/response-validator.html), validates the provider response. 
