---
group: compman
subgroup: 05_UseCompMan
title: 步骤4. 卸载
menu_title: 步骤4. 卸载
menu_node:
menu_order: 50
version: 2.0
github_link: comp-mgr/module-man/compman-uninst-final.md
redirect_from: /guides/v2.0/comp-mgr/compman-uninst-final.html
functional_areas:
  - Upgrade
---

## 步骤4. 卸载
To uninstall your component, click **Uninstall** as the following figure shows.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="{{ site.baseurl }}/common/images/cman_uninst2.png" width="300px" alt="Click Uninstall">

If successful, a page similar to the following displays.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="{{ site.baseurl }}/common/images/cman_uninst-success.png" width="250px" alt="Your component was successfully uninstalled">

Messages similar to the following display in the Console Log:

	[2015-08-15 13:01:02 CDT] Job "setup:component:uninstall {"组件":[{"name":"example/module"}],"dataOption":false}" has started
	Removing from module registry in database
	Removing from module list in deployment configuration
	Cleaning cache
	Cleaning generated files
	Cleaning static view files

	[2015-08-15 13:01:02 CDT] Job "setup:component:uninstall {"组件":[{"name":"example/module"}],
	"dataOption":false}" has been successfully completed
	[2015-08-15 13:01:03 CDT] Job "uninstall {"组件":[{"name":"example/module"}]}" has been started
	[2015-08-15 13:01:03 CDT] Starting composer remove...

