---
group: install_cli
title: 创建、编辑或解锁 Magento管理员账号
version: 2.0
github_link: install-gde/install/cli/install-cli-subcommands-admin.md
redirect_from: /guides/v2.0/install-gde/install/install-cli-subcommands-admin.html
functional_areas:
  - Install
  - System
  - Setup
---

## 第一步
{% include install/first-steps-cli.html %}

我们不止在这里讨论命令参数，更多请参考[Common arguments]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands.html#instgde-cli-subcommands-common).

## 先决条件
在你使用这个命令之前，你必须做以下事情：

-   [创建布署配置]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html)
-   [最低限度启用Magento_Authorization和Magento_User模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html)
-   创建Magento的{% glossarytooltip 66b924b4-8097-4aea-93d9-05a81e6cc00c %}数据库表结构{% endglossarytooltip %}

<div class="bs-callout bs-callout-info" id="info" markdown="1">
一个最简单的创建数据库的方式是通过命令`magento setup:upgrade`.
</div>

## 创建或编辑一个管理员
使用命令行来创建或修改一个已经存在的管理员，如果你编辑一个管理员，只能修改他的姓名和密码。

命令用法：

	magento admin:user:create [--<parameter_name>=<value>, ...]

可以在下面的表格中找到对应的参数和值：

<table>
  <col width="20%">
  <col width="55%">
  <col width="15%">
  <tbody>
    <tr>
      <th>名称</th>
      <th>值</th>
      <th>是否必需?</th>
    </tr>
    <tr>
      <td>
        <p>--admin-firstname</p>
      </td>
      <td>
        <p>Magento管理员的姓.</p>
      </td>
      <td>
        <p>是</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>--admin-lastname</p>
      </td>
      <td>
        <p>Magento管理员的名.</p>
      </td>
      <td>
        <p>是</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>--admin-email</p>
      </td>
      <td>
        <p>Magento管理员的电子邮箱</p>
      </td>
      <td>
        <p>是</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>--admin-user</p>
      </td>
      <td>
        <p>Magento管理员的用户名</p>
      </td>
      <td>
        <p>是</p>
      </td>
    </tr>
    <tr>
      <td>
        <p>--admin-password</p>
      </td>
      <td>
        <p>Magento管理员的密码.</p>
        <p>密码至少7位，必须包含至少一个字母和数字.</p>
        <p我们推荐使用一个长的，更复杂的密码，用引号引住，例如, <code>--admin-password=''A0b9%t_3g'</code>.</p>
      </td>
      <td>
        <p>是</p>
      </td>
    </tr>
  </tbody>
</table>

## 解锁管理员账号
使用命令来解锁一个被锁定的账号，典型地，因为多次输错密码而被锁的账号。

	magento admin:user:unlock {user name}

你必需指定管理员的用户名，例如：

	magento admin:user:unlock admin
	The user account "admin" has been unlocked

如果解锁失败或出现问题，下面将显示下面的信息：

	The user account "admin" was not locked or could not be unlocked

搞清楚这个账户是不是管理员，是不是激活的，是不是被锁了。要想在管理面板看到被锁的用户，用管理员登录到管理面板，点击**System** > **Permissions** > **Locked Users**.

如果账户不存在，将显示下面的信息:

	Couldn't find the user account "bob"

#### 相关主题

-   [Installing the Magento software using the command line]({{ page.baseurl }}/install-gde/install/cli/install-cli-install.html)
-   [移除样本数据模块或更新样本数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-sample-data-other.html)
-   [启用或禁用模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-enable.html)
-   [显示或更改管理面板的URI]({{ page.baseurl }}/install-gde/install/cli/install-cli-adminurl.html)
-   [卸载模块]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-mods.html)
-   [建立或更新部署配置]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-deployment.html)
-   [开启或关闭维护模式]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-maint.html)
-   [Create the Magento database schema]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db.html)
-   [更新数据库表结构和数据]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-db-upgr.html)
-   [配置网店]({{ page.baseurl }}/install-gde/install/cli/install-cli-subcommands-store.html)
-   [备份和还原文件系统，媒体文件和数据库]({{ page.baseurl }}/install-gde/install/cli/install-cli-backup.html)
-   [卸载主题]({{ page.baseurl }}/install-gde/install/cli/install-cli-theme-uninstall.html)
-   [卸载语言包]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall-langpk.html)
-   [Uninstall the Magento software]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-uninstall)
-   [Update the Magento software]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-update)
-   [重装Magento]({{ page.baseurl }}/install-gde/install/cli/install-cli-uninstall.html#instgde-install-magento-reinstall)
