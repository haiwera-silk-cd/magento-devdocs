---
group: config-guide
subgroup: 04_CLI
title: 配置和执行定时任务
menu_title: 配置和执行定时任务
menu_node:
menu_order: 100
version: 2.0
github_link: config-guide/cli/config-cli-subcommands-cron.md
redirect_from: /guides/v1.0/config-guide/cli/config-cli-subcommands-cron.html
functional_areas:
  - Configuration
  - System
  - Setup
---

## 概述 of cron {#config-cli-cron-overview}
{% include config/cron-overview.md %}

To run cron in a web browser, see <a href="{{ page.baseurl }}/config-guide/secy/secy-cron.html">确保cron.php文件在浏览器上的安全</a>

## Run cron from the command line {#config-cli-cron-group-run}
命令参数：

	bin/magento cron:run [--group="<cron group name>"]

Where `--group` specifies the cron group to run. Omit this option to run cron for all groups.

To set up custom cron jobs and groups, see [Configure custom cron jobs and cron groups]({{ page.baseurl }}/config-guide/cron/custom-cron.html).

<div class="bs-callout bs-callout-info" id="info" markdown="1">
You must run cron twice: the first time to discover tasks to run and the second time to run the tasks themselves. The second cron run must occur on or after the `scheduled_at` time for every task.
</div>

## Run cron in the background {#config-cli-cron-bkg}
This section discusses how to run all Magento cron jobs every minute, which is the recommended interval for both {{site.data.var.ce}} and {{site.data.var.ee}}.

Run Magento cron jobs as the [Magento文件系统所有者]({{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html).

{% include config/setup-cron.md %}

#### 相关主题

-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cache.html">管理缓存</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-index.html">管理索引</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-compiler.html">代码编译器</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-mode.html">设置Magento的模式</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-urn.html">统一资源名称(URN)高亮</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-depen.html">依赖报告</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html">翻译字典和语言包</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html">部署静态视图文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-less-sass.html">创建软链接到LESS文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-test.html">运行单元测试</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-layout-xml.html">转换布局的XML文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-perf-data.html">为性能测试生成数据</a>
