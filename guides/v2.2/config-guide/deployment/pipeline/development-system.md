---
group: config-guide
subgroup: 045_pipeline
title: 开发系统设置
menu_title: 开发系统设置
menu_node:
menu_order: 1300
version: 2.2
github_link: config-guide/deployment/pipeline/development-system.md
functional_areas:
  - Configuration
  - Deploy
  - System
  - Setup
---

You can have any number of development systems, provided the following is true of all of them:

*	They all run Magento 2.2或更新
*	All Magento code is under source control in the same repository as the build and production systems
*	Each development system should use either [default mode]({{ page.baseurl }}/config-guide/bootstrap/magento-modes.html#default-mode) or [开发者模式]({{ page.baseurl }}/config-guide/bootstrap/magento-modes.html#developer-mode)
*	It has Magento文件系统所有者和权限 set as discussed in [Prerequisite for your development, build, and production systems]({{ page.baseurl }}/config-guide/deployment/pipeline/technical-details.html#config-deploy-prereq).
*	Make sure all of the following are _excluded_ from source control:

	*	`vendor` directory (and subdirectories)
	*	`generated` directory (and subdirectories)
	*	`pub/static` directory (and subdirectories)
	*	`app/etc/env.php` file
*	Make sure `app/etc/config.php` is _included_ in source control

If you use Git, Magento's `.gitignore` provides most of the preceding. See the [`.gitignore` reference]({{ page.baseurl }}/config-guide/prod/config-reference-gitignore.html) for more information.

#### 下一步
[Set up a build system]({{ page.baseurl }}/config-guide/deployment/pipeline/build-system.html)
