---
group: install_cli
title: 显示或更新管理员面板的URI
version: 2.1
github_link: install-gde/install/cli/install-cli-adminurl.md
redirect_from:
  - /guides/v1.0/install-gde/install/install-cli-adminurl.html
  - /guides/v2.0/install-gde/install/install-cli-adminurl.html
functional_areas:
  - Install
  - System
  - Setup
---

<h2 id="instgde-cli-before">第一步</h2>
{% include install/first-steps-cli.html %}
我们除了在这里讨论这个命令行参数，你还可以参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common">命令行参数</a>.

<h2 id="instgde-cli-subcommands-db-prereq">先决条件</h2>
在你执行这个命令之前，你必须<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">创建或更新布署配置</a>.

<h2 id="instgde-cli-displayurl">显示管理员面板的URI</h2>
这一节讨论了如何使用命令行来显示管理员面板的 {% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}管理员面板{% endglossarytooltip %}的统一资源定位(<a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.2" target="_blank">URI</a>).

命令选项:

	magento info:adminuri

下页是一个示例结果:

	Admin Panel URI: /admin_1wgrah

您也可以在`<your Magento install dir>/app/etc/env.php`文件中看到你的管理员面板的URI.如下代码片段:

{% highlight php startinline=true %}
  'backend' =>
  array (
    'frontName' => 'admin_1wgrah',
  ),
{% endhighlight %}

<h2 id="instgde-cli-changeurl">修改管理员面板URI</h2>
要想修改管理员面板的URI,请使用<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html">magento setup:config:set</a>命令.