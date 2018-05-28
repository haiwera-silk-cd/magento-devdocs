---
group: compman
subgroup: 02_prereq
title: 为升级和更新设置定时任务(cron)
menu_title: 为升级和更新设置定时任务(cron)
menu_order: 3
menu_node:
version: 2.2
github_link: comp-mgr/prereq/prereq_cron.md
functional_areas:
  - Upgrade
---

To enable us to update or upgrade your system, you must have two cron jobs. Each cron job should run every minute.

The cron jobs schedule tasks for the Setup Wizard and for the updater application. These applications work together to install, update, and upgrade the Magento application and 组件.

{% include config/setup-cron_2.2_about.md %}

{% include config/setup-cron_2.2_how-to.md %}

For more information about cron, including how to remove a crontab and run cron from the command line, see [配置和执行定时任务]({{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cron.html).


