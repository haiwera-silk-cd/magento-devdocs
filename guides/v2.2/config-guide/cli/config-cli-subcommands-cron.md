---
group: config-guide
subgroup: 04_CLI
title: 配置和执行定时任务
menu_title: 配置和执行定时任务
menu_node:
menu_order: 100
version: 2.2
github_link: config-guide/cli/config-cli-subcommands-cron.md
functional_areas:
  - Configuration
  - System
  - Setup
---

## Overview of cron {#config-cli-cron-overview}
{% include config/cron-overview.md %}

To run cron in a web browser, see <a href="{{ page.baseurl }}/config-guide/secy/secy-cron.html">确保cron.php文件在浏览器上的安全</a>

## Create or remove the Magento crontab
This section discusses how to create or remove your Magento crontab (that is, the configuration for Magento cron jobs).

{% include config/setup-cron_2.2_about.md %}

{% include config/setup-cron_2.2_how-to.md %}

### Remove the Magento crontab {#config-cron-remove}
You should remove the Magento crontab only before uninstalling the Magento application.

To remove the Magento crontab:

1.  Log in as or switch to the [Magento文件系统所有者]({{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html).
2.  Change to the Magento installation directory.
3.  Enter the following command:

      php bin/magento cron:remove

<div class="bs-callout bs-callout-info" id="info" markdown="1">
This command has no effect on cron jobs outside the `#~ MAGENTO START` and `#~ MAGENTO END` comments in your crontab.
</div>

## Run cron from the command line {#config-cli-cron-group-run}
命令参数：

  bin/magento cron:run [--group="<cron group name>"]

where `--group` specifies the cron group to run (omit this option to run cron for all groups)

To run the indexing cron job, enter:

`php bin/magento cron:run --group index`


To run the default cron job, enter:

`php bin/magento cron:run --group default`


To set up custom cron jobs and groups, see [Configure custom cron jobs and cron groups]({{ page.baseurl }}/config-guide/cron/custom-cron.html).

<div class="bs-callout bs-callout-info" id="info" markdown="1">
You must run cron twice: the first time to discover tasks to run and the second time — to run the tasks themselves. The second cron run must occur on or after the `scheduled_at` time for every task.
</div>

## Logging
System logs provide detailed information for debugging. The following attributes apply to Magento cron logs:

-   All exceptions from cron jobs are logged by `\Magento\Cron\Observer\ProcessCronQueueObserver::execute`.

-   Failed jobs with `ERROR` and `MISSED` statuses are logged to the `<your Magento install dir>/var/log` directory.

-   Jobs with an `ERROR` status are always logged as `CRITICAL` in `<your Magento install dir>/var/log/exception.log`.

-   Jobs with a `MISSED` status are logged as `INFO` in the `<your Magento install dir>/var/log` directory (developer mode only).

<div class="bs-callout bs-callout-tip" markdown="1">
All cron data is also written to the `cron_schedule` table in the Magento database. The table provides a history of cron jobs, including:

-   Job ID and code
-   Status
-   Created date
-   Scheduled date
-   Executed date
-   Finished date

To see records in the table, log in to the Magento database on the command line and enter `SELECT * from cron_schedule;`.
</div>

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
