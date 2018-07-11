---
group: payments-integrations
subgroup: C_vault
title: 添加vault到模块依赖
menu_title: 添加vault到模块依赖
menu_order: 1
version: 2.1
github_link: payments-integrations/vault/module-configuration.md
functional_areas:
  - Integration
---

You need to add dependencies on the Magento_Vault模块 in the payment method's `composer.json` and `module.xml` files.

## 例如: adding Vault module dependencies for the Braintree payment method

`app/code/Magento/Braintree/composer.json`:

{% highlight json %}
{
    "name": "magento/module-braintree",
    ...
    "require": {
        ...
        "magento/module-vault": "100.1.*"
        ...
    }
    ...
}
{% endhighlight %}

`app/code/Magento/Braintree/etc/module.xml`:
{% highlight xml %}
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Magento_Braintree" setup_version="2.0.0">
        <sequence>
            ...
            <module name="Magento_Vault"/>
            ...
        </sequence>
    </module>
</config>
{% endhighlight %}

## What's next

[Configure vault general parameters]({{ page.baseurl }}/payments-integrations/vault/vault-payment-configuration.html).