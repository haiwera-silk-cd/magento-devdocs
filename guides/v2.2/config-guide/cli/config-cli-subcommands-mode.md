---
group: config-guide
title: 设置Magento的模式
version: 2.2
github_link: config-guide/cli/config-cli-subcommands-mode.md
functional_areas:
  - Configuration
  - System
  - Setup
---

{% include config/cli-intro.md %}

## 概述 of setting Magento modes {#config-mode-over}
To improve security and ease-of-use, we added a command that switches <a href="{{ page.baseurl }}/config-guide/bootstrap/magento-modes.html">Magento modes</a> from developer to production and vice versa.

Production mode also has better performance because static view files are populated in the `pub/static` directory and because of code compilation.

<div class="bs-callout bs-callout-info" id="info" markdown="1">
-   In version 2.0.6 and later, Magento does not explicitly set file or directory permissions when you switch between default, develop, and production modes.
-   Unlike other Magento modes, developer and production modes are set in `env.php`.
-   <a href="{{ page.baseurl }}/cloud/bk-cloud.html">{{site.data.var.ece}}</a> supports production mode only.
</div>

Refer to [Magento开发环境和生产环境的所有者和权限]({{ page.baseurl }}/config-guide/prod/prod_file-sys-perms.html) for more information.

When you change to developer or production mode, we clear the contents of following directories:

	var/cache
	generated/metadata
	generated/code
	var/view_preprocessed
	pub/static

Exceptions:

-   `.htaccess` files are not removed
-   `pub/static` contains a file that specifies the version of static content; this file is not removed

<div class="bs-callout bs-callout-info" id="info" markdown="1">
By default, Magento uses the `var` directories to store the cache, logs, and compiled code. You can customize this directory but in this guide, it's assumed to be `var`.
</div>

## Display the current mode {#config-mode-show}
The easiest way to do that is to run this command as the <a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">Magento文件系统所有者</a>. If you have shared hosting, this is the user your provider gives you to log in to the server. If you have a private server, it's typically a local user account on the Magento server.

命令用法：

``` bash
bin/magento deploy:mode:show
```

类似下面的消息会显示：

```
Current application mode: developer.
```

## Change modes {#config-mode-change}
命令用法：

``` bash
bin/magento deploy:mode:set {mode} [-s|--skip-compilation]
```

where:

  -   **`{mode}`** is required; it can be either `developer`或`production`

  -   **`--skip-compilation`** is an optional parameter you can use to skip <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-compiler.html">code compilation</a> when you change to production mode.

Examples follow.

### Change to production mode

``` bash
bin/magento deploy:mode:set production
```

命令行将有以下输出信息：

	Enabled maintenance mode
	Requested languages: en_US
	=== frontend -> Magento/luma -> en_US ===
	... more ...
	Successful: 1884 files; errors: 0
	---

	=== frontend -> Magento/blank -> en_US ===
	... more ...
	Successful: 1828 files; errors: 0
	---

	=== adminhtml -> Magento/backend -> en_US ===
	... more ...
	---

	=== Minify templates ===
	... more ...
	Successful: 897 files modified
	---

	New version of deployed files: 1440461332
	Static content deployment complete
Gathering css/styles-m.less sources.
Successfully processed LESS and/or {% glossarytooltip 45f1f76d-91cd-4789-a8b5-1e3f321a6280 %}SASS{% endglossarytooltip %} files
{% glossarytooltip 6c5cb4e9-9197-46f2-ba79-6147d9bfe66d %}CSS{% endglossarytooltip %} deployment complete
Generated classes:
        Magento\Sales\Api\Data\CreditmemoCommentInterfacePersistor
        Magento\Sales\Api\Data\CreditmemoCommentInterfaceFactory
        Magento\Sales\Api\Data\CreditmemoCommentSearchResultInterfaceFactory
        Magento\Sales\Api\Data\CreditmemoComment\Repository
        Magento\Sales\Api\Data\CreditmemoItemInterfacePersistor
        ... more ...
	Compilation complete
	Disabled maintenance mode
	Enabled production mode.

### Change to developer mode
When you change from production to developer mode, you should clear generated classes and Object Manager entities like proxies to prevent unexpected errors. After doing so, you can change modes. Use the following steps:

1.  If you're changing from production mode to developer mode, delete the contents of the `generated/code` and `generated/metadata` directories:

		rm -rf <your Magento install dir>/generated/metadata/* <your Magento install dir>/generated/code/*

2.  Set the mode:

		bin/magento deploy:mode:set developer

	The following message displays:

		Switched to developer mode.

### Change to default mode

``` bash
bin/magento deploy:mode:set default
```

The following message displays:

    Enabled default mode.

### Run Magento CLI commands from anywhere
[Run Magento CLI commands from anywhere]({{ page.baseurl }}/config-guide/cli/config-cli.html#config-install-cli-first).

If you haven't added `<magento-install-directory>/bin` to your system `PATH`, then you can expect an error when running the Magento command by itself.

#### 相关主题

-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cache.html">管理缓存</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-index.html">管理索引</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cron.html">配置和执行定时任务</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-compiler.html">代码编译器</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-urn.html">统一资源名称(URN)高亮</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-depen.html">依赖报告</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html">翻译字典和语言包</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html">部署静态视图文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-less-sass.html">创建软链接到LESS文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-test.html">运行单元测试</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-layout-xml.html">转换布局的XML文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-perf-data.html">为性能测试生成数据</a>
