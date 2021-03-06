---
group: config-guide
subgroup: 04_CLI
title: 代码编译器
menu_title: 代码编译器
menu_node:
menu_order: 175
version: 2.0
github_link: config-guide/cli/config-cli-subcommands-compiler.md
redirect_from:
  - /guides/v1.0/config-guide/cli/config-cli-subcommands-compiler-single.html
  - /guides/v2.0/config-guide/cli/config-cli-subcommands-compiler-single.html
  - /guides/v2.0/config-guide/cli/config-cli-subcommands-compiler-multi.html
functional_areas:
  - Configuration
  - System
  - Setup
---

{% include config/cli-intro.md %}

## 概述 of code compilation {#config-cli-subcommands-compile-overview}
This section discusses the basics of code compilation. Code compilation consists of all of the following (in no particular order):

-   Application code generation (factories, proxies, and so on)
-   Area configuration aggregation (that is, optimized {% glossarytooltip 2be50595-c5c7-4b9d-911c-3bf2cd3f7beb %}依赖注入{% endglossarytooltip %} configurations per area)
-   Interceptor generation (that is, optimized code generation of interceptors)</li>
-   Interception {% glossarytooltip 0bc9c8bc-de1a-4a06-9c99-a89a29c30645 %}缓存{% endglossarytooltip %} generation
-   Repositories code generation (that is, generated code for APIs)
-   Service data attributes generation (that is, generated {% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}扩展{% endglossarytooltip %} classes for data objects)

You can find code compilation in classes in the <a href="{{ site.mage2000url }}setup/src/Magento/Setup/Module/Di/App/Task/Operation" target="\_blank">\Magento\Setup\Module\Di\App\Task\Operation</a> {% glossarytooltip 621ef86b-7314-4fbc-a80d-ab7fa45a27cb %}命名空间{% endglossarytooltip %}.

## Run the single-tenant compiler {#config-cli-subcommands-single}
Run the command as follows (there are no options):

	bin/magento setup:di:compile

The following message displays to confirm success:

	Generated code and dependency injection configuration successfully.

<div class="bs-callout bs-callout-warning" markdown="1">
In Magento versions 2.0.5 and earlier, there is a known issue with the single-tenant compiler; it does not currently compile proxies. Therefore, if you're preparing to deploy to production, you must use the multi-tenant compiler.

The issue was resolved in Magento versions 2.0.6 and later.
</div>

## Run the multi-tenant compiler {#config-cli-subcommands-run}
Use this command if you have multiple *tenants*, which means more than one independent Magento application. In other words:

-   There is one Magento 2 code base instance
-   There is one database instance per tenant
-   Independent configurations in the {% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento管理面板{% endglossarytooltip %} per tenant
-   The storefronts are independent of each other

If you do not have multiple tenants, use the <a href="#config-cli-subcommands-single">single-tenant compiler</a> instead.

命令参数：

	bin/magento setup:di:compile-multi-tenant [--serializer="{serialize|igbinary}"] [--extra-classes-file="<path>"] [--generation="<path and
	filename>"] [--di="<path and filename>"] [--exclude-pattern="<regex>"]

The following table discusses the meanings of this command's parameters and values.

<table>
	<col width="25%">
	<col width="65%">
	<col width="10%">
	<tbody>
		<tr>
			<th>参数</th>
			<th>值</th>
			<th>是否必需?</th>
		</tr>

	<tr>
		<td><p>--serializer</p></td>
		<td><p>Specify either <code>serialize</code>或<a href="https://github.com/phadej/igbinary" target="\_blank">igbinary</a>. Default is <code>serialize</code>.</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--extra-classes-file</p></td>
		<td><p>Specify the absolute file system path to proxies and factories that are not declared in the dependency injection or code..</p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--generation</p></td>
		<td><p>Absolute file system path to a directory for generated classes. Default is <code>&lt;你的Magento的安装目录>/var/generation</code></p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--di</p></td>
		<td><p>Absolute file system path to a directory to generate the object manager configuration. Default is <code>&lt;你的Magento的安装目录>/var/di</code></p></td>
		<td><p>否</p></td>
	</tr>
	<tr>
		<td><p>--exclude-pattern</p></td>
		<td><p>Regular expression that enables you to exclude paths from compilation. Default is <code>#[\\/]m1[\\/]#i)</code></p></td>
		<td><p>否</p></td>
	</tr>

	</tbody>
</table>

例如， to run the compiler and specify the `igbinary` serializer:

	bin/magento setup:di:compile-multi-tenant --serializer=igbinary

命令行将有以下输出信息：

	Generated classes:
        Magento\Rss\Controller\Adminhtml\Feed\Interceptor
        Magento\Quote\Model\Quote\Config\Interceptor
        Magento\Checkout\Block\Cart\Shipping\Interceptor
        Magento\Framework\View\Layout\Interceptor
        Magento\Integration\Service\V1\Integration\Interceptor
        Magento\Catalog\Block\Product\Compare\ListCompare\Interceptor
        Magento\Framework\View\TemplateEngineFactory\Interceptor
        Magento\Catalog\Model\Product\Attribute\Backend\Price\Interceptor
        Magento\Catalog\Api\ProductRepositoryInterface\Interceptor
        Magento\Catalog\Model\Product\Interceptor
        Magento\Quote\Model\Quote\Item\ToOrderItem\Interceptor
        Magento\Catalog\Controller\Adminhtml\Product\Initialization\Helper\Interceptor
        Magento\Catalog\Model\Product\CartConfiguration\Interceptor
        Magento\Catalog\Model\Product\TypeTransitionManager\Interceptor
        Magento\Catalog\Model\Product\Type\Interceptor
        ... more messages ...
        On \*nix systems, verify the Magento application has permissions to modify files created by the compiler in the "var" directory.
        For instance, if you run the Magento application using Apache, the owner of the files in the "var" directory should be the Apache user
        (example command: "chown -R www-data:www-data <MAGENTO_ROOT>/var" where MAGENTO_ROOT is the Magento root directory).

#### 相关主题

-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cache.html">管理缓存</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-index.html">管理索引</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cron.html">配置和执行定时任务</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-mode.html">设置Magento的模式</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-urn.html">统一资源名称(URN)高亮</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-depen.html">依赖报告</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html">翻译字典和语言包</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html">部署静态视图文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-less-sass.html">创建软链接到LESS文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-test.html">运行单元测试</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-layout-xml.html">转换布局的XML文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-perf-data.html">为性能测试生成数据</a>
