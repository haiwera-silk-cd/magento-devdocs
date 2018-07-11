---
group: cloud
subgroup: 020_tech
title: Fastly
menu_title: Fastly
menu_node:
menu_order: 15
version: 2.1
github_link: cloud/basic-information/cloud-fastly.md
functional_areas:
  - Cloud
  - Setup
---

Fastly is a CDN based on Varnish caching, basically a cloud varnish service. When working with Fastly, you are also working directly with a heavily customized version of Varnish (2.1). [Fastly](https://docs.fastly.com/){:target="_blank"} with [Varnish](https://varnish-cache.org/docs/){:target="_blank"} caches your site pages, assets, CSS, and more in backend datacenters you set up. As customers access your site and stores, the requests hit Fastly to load cached pages faster.

For {{site.data.var.ece}}, you receive Fastly CDN and DDoS services. When you update products, catalogs, content, and more, Fastly purges that specific cached content to refresh and provide the latest changes.

We provide Fastly service credentials including a Fastly Service ID and API key pair for your Staging and Production environments. To [set up Fastly](#install-configure), you enter credentials, upload VCL snippets, and configure backends (with Origin shields) in Staging and Production environments, not in Integration.

Fastly provides the following powerful tools for Magento:

* Create edge and ACL dictionaries with VCL snippets (Varnish 2.1 compliant) to modify how caching responds to requests
* Three types of purges for:

  * Quick Purge (by URL)
  * Surrogate/key purge using tags to purge specific HTML, images, categories, and so on
  * Purge all, which clears everything in the cache
* GeoIP extension support
* Force unencrypted requests over to TLS

We highly recommend enabling and using Fastly for your caching and CDN. The only situation you may not want to enable is for a headless deployment.

We strongly recommend installing Fastly module 1.2.33或更新.

## Fastly and 503 timeouts {#timeouts}
When you receive a 503 error from Fastly, it may be due to a lengthy operation or performing bulk actions. Fastly has a default 60 second time out. Any request that takes longer than 60 seconds will return a 503 error.

If you receive a 503 error, make the request directly to the origin or review logs. For details, see [快速故障排查]({{ page.baseurl }}/cloud/trouble/trouble_fastly.html#timeouts).

Fastly can be bypassed for the Magento Admin to perform long running or bulk actions and API access to avoid 503s. For Fastly module 1.2.22 and later, the timeout for the Magento Admin was extended to three minutes.

We provide [VCL snippet instructions]({{ page.baseurl }}/cloud/configure/fastly-vcl-extend-timeout.html) for extending the timeout for the Magento Admin.

## Backends and Origin shields {#backend}
后台设置为Fastly的Origin shielding执行和超时提供微调。_后台_是一个有为检查和提供缓存内容配置了Origin shield和超时设置的是一个指定的位置(IP或域名)

_Origin shielding_为你的网店路由所有的请求到一个指定点(POP)。当接收到一个请求，POP检查缓存的内容并提供它，如果它没有被缓存，会被继续路由到Shied POP,然后到缓存了内容的原始服务器上。shields减少了直接到原始站的流量。

We provide detailed instructions for configuring backends when you [configure Fastly]({{ page.baseurl }}/cloud/access-acct/fastly.html).

## Basic authentication {#basic-auth}
Basic authentication is a feature to protect every page and asset on your site with a username and password. We **do not recommend** activating basic authentication on your Production environment. You can configure it on Staging to protect your site when completing development.

If you add user access and enable basic authentication on Staging, you can still access the Magento Admin without requiring additional credentials to enter.

## Custom VCLs and actions {#custom-vcl}
Fastly provides an extremely custom code friendly method for creating lists of items like IPs and domains to complete actions via Fastly and Varnish code blocks. 例如， with edge and ACL dictionaries and VCL code, you could allow, block, or redirect access for specific users or IPs.

After you have [set up Fastly]({{ page.baseurl }}/cloud/access-acct/fastly.html), you can create [自定义VCL代码片段]({{ page.baseurl }}/cloud/configure/cloud-vcl-custom-snippets.html) using these edge dictionaries and ACLs.

### Edge dictionaries {#dictionary}
Save key-value pairs on Fastly Edge nodes of dictionary containers and items to invoke with VCL snippets in your site. You have up to 1,000 entries per dictionary.

You create an edge dictionary then add items to it of a key and its value. 例如， you could create an edge dictionary of banned bad refer sites from accessing your site. The key-value pairs would be the refer site URLs (www.example.com) and a value of 1. Then create a custom VCL snippet to return a 403 Forbidden to those sites when they access your site.

Another example routes to a different WordPress backend for an edge dictionary of WordPress URLs.

### Edge ACLs {#acl}
ACLs are access control lists that allow you to manage IP addresses to allow or block access to resources. You could use edge ACLs with VCL snippets to block IP addresses or provide access. 例如， use edge ACLs and a custom VCL snippet to white list IPs to access your site.

### VCL snippets {#vcl}
With edge dictionaries and edge ACLs, you can create custom Varnish Configuration Language (VCL) snippets to Fastly and your site. VCL snippets are small chunks of logic and code that can be included directly into your service configuration. They are generated, compiled, and transmitted to all Fastly caches, loaded, and activated without waiting for maintenance windows without server downtime.

For a few examples, you can create VCL snippets to:

* Block access to the site using an edge dictionary of domains
* Whitelist and allow access using an edge ACL
* Redirect blog links from your store to a blog site
* Extend timeouts for Fastly and Magento

After you have [set up Fastly](#install-configure), we provide detailed instructions on creating [custom Fastly VCL snippets]({{ page.baseurl }}/cloud/configure/cloud-vcl-custom-snippets.html).

## Force TLS {#tls}
Fastly supports forcing unencrypted requests to TLS through the Force TLS feature. Set up a secure base URL in Magento and turn on the Force TLS option in the Fastly extension. For details and instructions, see Fastly's [Force TLS guide](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/FORCE-TLS.md){:target="_blank"}.

## GeoIP service support {#geoip}
Fastly provides a GeoIP service and supports some GeoIP functionality. GeoIP handling manages visitor redirection (automatically) and store matching (select from list) based on their obtained country code. For more information, see Fastly's [GeoIP documentation](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/CONFIGURATION.md#geoip-handling){:target="_blank"}.

## 安装和配置 {#install-configure}
The installation and configuration process is:

* Install the Fastly module in an Integration branch, without configuring settings or entering credentials.
* Deploy the code to `integration` then to Staging and Production
* 快速配置 in Staging and Production, not in Integration or your local
* Test Fastly for caching

For instructions, see [快速设置]({{ page.baseurl }}/cloud/access-acct/fastly.html). After you have configured it, you can continue with advanced options including 自定义VCL代码片段.

