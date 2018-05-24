---
group: config-guide
subgroup: 04_CLI
title: 统一资源名称(URN)高亮
menu_title: 统一资源名称(URN)高亮
menu_node:
menu_order: 215
version: 2.1
github_link: config-guide/cli/config-cli-subcommands-urn.md
functional_areas:
  - Configuration
  - System
  - Setup
---

{% include config/cli-intro.md %}

## Overview of 统一资源名称(URN)高亮
Magento code references all XSD schemas as <a href="https://www.ietf.org/rfc/rfc2141.txt" target="\_blank">Uniform Resource Names (URNs)</a>. If you're developing code and need to reference XSDs, this command configures your integrated developer environment (IDE) to recognize and highlight URNs. This makes development easier.

By default, an IDE like PHPStorm is not configured to recognize URNs and, as a result, they display in red text as follows:

<img src="{{ site.baseurl }}/common/images/config_urn_before.png" width="750px">

The `bin/magento dev:urn-catalog:generate` command enables your IDE (currently, only PHPStorm) to recognize and highlight URNs like the following:

<img src="{{ site.baseurl }}/common/images/config_urn_after.png" width="750px">

Specifically, this command creates the following PHPStorm configuration:

<img src="{{ site.baseurl }}/common/images/config_urn_settings.png" width="750px">

## Configure your IDE
Currently, only PHPStorm is supported.

Command syntax:

	bin/magento dev:urn-catalog:generate <path>

Where `<path>` is the path to your PHPStorm `misc.xml` file, which is located relative to your project root. Typically, `<path>` is `.idea/misc.xml`.

#### 相关主题

-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cache.html">管理缓存</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-index.html">管理索引</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cron.html">配置和执行定时任务</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-compiler.html">代码编译器</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-mode.html">设置Magento的模式</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-depen.html">依赖报告</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html">翻译字典和语言包</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html">部署静态视图文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-less-sass.html">创建软链接到LESS文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-test.html">运行单元测试</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-layout-xml.html">转换布局的XML文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-perf-data.html">为性能测试生成数据</a>
