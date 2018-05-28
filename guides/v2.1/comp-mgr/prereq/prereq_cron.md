---
group: compman
subgroup: 02_prereq
title: 为升级和更新设置定时任务(cron)
menu_title: 为升级和更新设置定时任务(cron)
menu_order: 3
menu_node:
version: 2.1
github_link: comp-mgr/prereq/prereq_cron.md
redirect_from: /guides/v2.0/comp-mgr/prereq/prereq_compman-updater.html
functional_areas:
  - Upgrade
---

To enable us to update or upgrade your system, you must configure two cron jobs. Each cron job should run every minute.

The cron jobs schedule tasks for the Setup Wizard and for the updater application. These applications work together to install, update, and upgrade the Magento application and 组件.

Enable the cron jobs as <a href="http://ss64.com/bash/crontab.html" target="_blank">crontabs</a> for the [Magento文件系统所有者]({{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html) because that user runs the updater application for the 网页安装向导. 

{% include config/setup-cron.md %}

