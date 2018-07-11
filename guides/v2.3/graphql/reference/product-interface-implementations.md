---
group: graphql
title: Product interface implementations
version: 2.3
github_link: graphql/reference/product-interface-implementations.md
---

Magento provides multiple product types, and most of these product types have specialized attributes that are not defined in the `ProductInterface`.

Product type | Implements | Has product-specific attributes?
--- | --- | ---
* [BundleProduct]({{ page.baseurl }}/graphql/reference/bundle-product.html) | [ProductInterface]({{ page.baseurl }}/graphql/reference/products.html#ProductInterface), [PhysicalProductInterface]({{ page.baseurl }}/graphql/reference/products.html#PhysicalProductInterface), [CustomizableProductInterface]({{ page.baseurl }}/graphql/reference/customizable-option-interface.html) | 是
* [ConfigurableProduct]({{ page.baseurl }}/graphql/reference/configurable-product.html) | [ProductInterface]({{ page.baseurl }}/graphql/reference/products.html#ProductInterface), [PhysicalProductInterface]({{ page.baseurl }}/graphql/reference/products.html#PhysicalProductInterface), [CustomizableProductInterface]({{ page.baseurl }}/graphql/reference/customizable-option-interface.html) | 是
* [DownloadableProduct]({{ page.baseurl }}/graphql/reference/downloadable-product.html) | [ProductInterface]({{ page.baseurl }}/graphql/reference/products.html#ProductInterface),  [CustomizableProductInterface]({{ page.baseurl }}/graphql/reference/customizable-option-interface.html)  | 是
* [GroupedProduct]({{ page.baseurl }}/graphql/reference/grouped-product.html) | [ProductInterface]({{ page.baseurl }}/graphql/reference/products.html#ProductInterface), [PhysicalProductInterface]({{ page.baseurl }}/graphql/reference/products.html#PhysicalProductInterface), [CustomizableProductInterface]({{ page.baseurl }}/graphql/reference/customizable-option-interface.html) | 是
* SimpleProduct | [ProductInterface]({{ page.baseurl }}/graphql/reference/products.html#ProductInterface), [PhysicalProductInterface]({{ page.baseurl }}/graphql/reference/products.html#PhysicalProductInterface), [CustomizableProductInterface]({{ page.baseurl }}/graphql/reference/customizable-option-interface.html)  | 否
* VirtualProduct | [ProductInterface]({{ page.baseurl }}/graphql/reference/products.html#ProductInterface),  [CustomizableProductInterface]({{ page.baseurl }}/graphql/reference/customizable-option-interface.html)  | 否

## Query for product-specific attributes

To return attributes that are specific to a product type, append a structure similar to the following to the end of the `Products` output object:

{% highlight json %}
... on <ProductType> {
  items{
    <ProductType-attribute1>
    <ProductType-attribute2>
    ...
    }
  }
  {% endhighlight %}

例如， to return `GroupedProduct` attributes, construct your query like this:

{% highlight json %}
{
  products(filter:
    {sku: {eq: "24-WG085_Group"}}
  	)
  	{
    items {
      id
      name
      sku
      type_id
      ... on GroupedProduct {
        items{
          qty
          position
          product{
            sku
            name
            type_id
            url_key
          }
        }
      }
    }
  }
}
{% endhighlight %}
