---
group: install_cli
subgroup: 99_contrib
title: 贡献开发者&mdash;更新、重装Magento
menu_title: 贡献开发者&mdash;更新、重装Magento
menu_order: 1
menu_node: parent
version: 2.1
github_link: install-gde/install/cli/dev_options.md
redirect_from:
  - guides/v2.0/install-gde/install/dev_updater.html
  - guides/v2.1/install-gde/install/dev_updater.html
functional_areas:
  - Install
  - System
  - Setup
---

下面所讲的仅适用于你是通过`git clone`从GitHub上克隆{{site.data.var.ce}}的情况. 这通常意味着你是{{site.data.var.ce}}基础代码的贡献者.

<div class="bs-callout bs-callout-warning">
    <p>如果你是克隆的Magento 2仓库的代码, 你不能直接布署到生产环境. You cannot have a live store that accepts orders and so on.</p>
</div>

*	要<a href="{{ page.baseurl }}/install-gde/install/cli/dev_update-magento.html">更新Magento</a>, 使用 `git pull origin`和`composer update`, 然后更新Magento的数据库
*	要从`develop`<a href="{{ page.baseurl }}/install-gde/install/cli/dev_downgrade.html">切换版本</a> 到一个如`2.0.4`的版本, 你必须先卸载Magento然后再重新安装对应的发布版.
*	要<a href="{{ page.baseurl }}/install-gde/install/cli/dev_add-update.html">添加、移除或更新组件</a>, 请修正改`composer.json`然后运行`composer update`，再然后更新Magento的数据库
*	要<a href="{{ page.baseurl }}/install-gde/install/cli/dev_reinstall.html">重装Magengo</a>, 在`composer.json`中修改Magento的版本，然后执行`composer update`, 再然后重新安装Magento

<div class="bs-callout bs-callout-info" id="info">
	<span class="glyphicon-class">
		<p>如果你不是一个贡献开发者，要更新或升级Magento我们在<a href="{{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html">更新或升级magento及其组件</a>进行讨论.</p> </span>
</div>

<!-- ABBREVIATIONS -->

*[贡献开发者]: 参与Magento 2 CE基础代码开发的开发者
