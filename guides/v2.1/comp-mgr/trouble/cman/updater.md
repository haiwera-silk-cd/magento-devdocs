---
group: compman
subgroup: 50_trouble
title: 排除更新器程序的问题
menu_title: 排除更新器程序的问题
menu_node:
menu_order: 10
version: 2.1
github_link: comp-mgr/trouble/cman/updater.md
functional_areas:
  - Upgrade
---

If the updater application is not available, the following message displays in the readiness check:

	更新器程序 is not available. 
	Please, download and install 更新器程序.

To resolve this issue, see if there is a `<your Magento install dir>/update` directory that contains files and subdirectories. If not, see <a href="{{ page.baseurl }}/install-gde/prereq/prereq_updater.html">Set up the updater</a>.
