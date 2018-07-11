---
group: migration
subgroup: C_DMTool
title: 升级数据迁移工具
menu_title: 升级数据迁移工具
menu_node:
menu_order: 3
version: 2.1
github_link: migration/migration-tool-upgrade.md
functional_areas:
  - Tools
---

## Why do I need to upgrade?

To make sure the versions of your current Magento 2 installation and the 数据迁移工具 match exactly, you may need to upgrade the Tool.

## 先决条件 {#data-migrate-prereq}

Before upgrading the 数据迁移工具, you must:

*	Upgrade your Magento software to get the latest version

*	Back up the `vendor/magento/data-migration-tool` directory

* Make sure the 数据迁移工具 version matches the Magento application version

### Upgrade your Magento software {#data-migrate-upgr-magento}

If you haven't already done so, run the <a href="{{ page.baseurl }}/comp-mgr/upgrader/upgrade-start.html">System Upgrade utility</a> to upgrade the Magento software.

### Back up the `vendor/magento/data-migration-tool` directory

Before you upgrade the 数据迁移工具, back up at least the `vendor/magento/data-migration-tool` directory. During upgrade, it could be deleted and replaced by the updated code.

You can also back up the entire Magento codebase and database using the following command:

	php <your Magento install dir>/bin/magento setup:backup --code --db

<div class="bs-callout bs-callout-warning">
    <p>The <code>vendor/magento/data-migration-tool</code> directory contains your custom code. Failure to back it up means you can lose your customizations during upgrade.</p>
</div>

### Make sure versions match

The versions of the 数据迁移工具 and your Magento software must match exactly. 例如， Magento 2.1.2 requires version 2.1.2 of the 数据迁移工具.

See the [安装数据迁移工具]({{ page.baseurl }}/migration/migration-tool-install.html) topic to know how to:

* [Check]({{ page.baseurl }}/migration/migration-tool-install.html#magento-version) your Magento 2 version

* [Find]({{ page.baseurl }}/migration/migration-tool-install.html#migration-tool-release-version) released versions of the 数据迁移工具

* [Check]({{ page.baseurl }}/migration/migration-tool-install.html#migration-tool-install-version) the 数据迁移工具 version

## 升级数据迁移工具 {#data-migrate-upgr}

1.	Log in to your Magento server as, or switch to, <a href="{{ page.baseurl }}/install-gde/prereq/apache-user.html">the Magento文件系统所有者</a>.
2.	Change to Magento 2 root directory.
3. 	输入下面的命令：

	`composer require magento/data-migration-tool:<version>`

	where `<version>` must match the version of the Magento 2 codebase.

	例如， for version 2.1.2, enter:

	`composer require magento/data-migration-tool:2.1.2`
4.	Wait while the command completes.

## 相关主题

* <a href="{{ page.baseurl }}/migration/migration-tool-configure.html">配置迁移</a>
* <a href="{{ page.baseurl }}/migration/migration-tool-preconditions.html">先决条件</a>
