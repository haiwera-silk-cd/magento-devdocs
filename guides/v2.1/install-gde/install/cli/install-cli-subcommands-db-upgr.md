---
group: install_cli
title: 更新Magento表结构及数据
version: 2.1
github_link: install-gde/install/cli/install-cli-subcommands-db-upgr.md
functional_areas:
  - Install
  - System
  - Setup
---

<h2 id="instgde-cli-before">第一步</h2>
{% include install/first-steps-cli.html %}
我们不止在这里讨论命令参数，更多请参考<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common">命令参数</a>.

<h2 id="instgde-cli-subcommands-maint-prereq">先决条件</h2>
在使用这个命令之前，你必须 <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-install.html">安装Magento</a>.

## 更新Magento数据表结构和数据 {#instgde-cli-db-upgr}
只要你执行的动作导致了Magento的{% glossarytooltip 66b924b4-8097-4aea-93d9-05a81e6cc00c %}数据库表结构{% endglossarytooltip %}或数据发生改变，你必须执行我们这节讨论的命令来更新它们，基于下面的原因：

*	你使用命令行升级了Magento
*	你使用命令行安装或更新了组件
*	你使用命令行启用或禁用了组件

注意：

*	如果你使用了之前所讲到的网页向导安装，你没有必要使用这里讨论的命令。
*	Magento的*组件*可以是一个模块、主题或语言包，无论是否来自Magento Marketplace都没有关系

命令用法：

	magento setup:upgrade [--keep-generated]

`--keep-generated`是一个可选的参数，指定不更新 [静态的视图文件]({{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html).这个可选的参数被有经验的系统集成人员用于有限的情况，并且只能用在[生产模式]({{ page.baseurl }}/config-guide/bootstrap/magento-modes.html#production-mode). 不能用在[开发者模式]({{ page.baseurl }}/config-guide/bootstrap/magento-modes.html#developer-mode).