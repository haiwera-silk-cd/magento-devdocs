---
group: arch-guide
subgroup: 架构基础
title: 安全概述
menu_title: Security
menu_order:
version: 2.1
github_link: architecture/security_intro.md
---

## 增强的密码管理

Magento在密码管理中强化了哈希算法(SHA-256)

## 提升了跨站脚本攻击的防护，默认开启数据转义。

Magento框架采用规定在输出时数据转义的习惯。这个习惯包括为{% glossarytooltip a2aff425-07dd-4bd6-9671-29b7edefa871 %}HTML{% endglossarytooltip %}页面(HTML, JSON, 和JavaScript)及email转义输出的能力。在可能的地方，转义对客户端代码来说是透明的，参考{% glossarytooltip b00459e5-a793-44dd-98d5-852ab33fc344 %}前端{% endglossarytooltip %}工程师手册中的<a href="{{ page.baseurl }}/frontend-dev-guide/templates/template-security.html">防范XSS攻击的安全措施</a>了解更多

## 更灵活的文件系统所有者和权限

从2.0.6开始，Magento不再明确设置文件权限。相反地，我们推荐某些文件和目录在开发环境中能被写，而在生产环境中只读。

要提供给你一个简单的方式限制在生产环境中访问文件系统，这们为你提供了使用[umask](http://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html){:target="_blank"}去限制权限的灵活性。

概述请参考所有者和权限概述]({{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html)./install-gde/prereq/file-sys-perms-over.html).

更多关于生产环和开发环境的所有者和权限的细节请参考[Magento开发环境和生产环境的所有者和权限]({{ page.baseurl }}).

## 提升点击劫持的防护

Magento使用X-Frame-Options HTTP请求头保护你的网店避免点击劫持攻击，参考<a href="{{ page.baseurl }}/config-guide/secy/secy-xframe.html"> X-Frame-Options头</a>.

## 使用非默认的Magento管理面板URL

一个简单的{% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento管理面板{% endglossarytooltip %} {% glossarytooltip a05c59d3-77b9-47d0-92a1-2cbffe3f8622 %}URL{% endglossarytooltip %} (像`admin`或`backend`)很容易使其成为攻击目标，用自动密码猜测软件进行攻击。要保护使网店不受这类攻击，Magento默认创建一个随机的管理面板的URI，在安装的时候。如果你忘记了命令行可以被用来查看这个URI，也可以用它来修改此URI。 虽然非默认的管理面板URI不能用于保护站点，但对大规模地自动攻击，是非常有效的。参考配置手册的<a href="{{ page.baseurl }}/install-gde/install/cli/install-cli-adminurl.html">显示和修改管理面板URI</a>了解更多信息

## 相关主题

<a href="{{ page.baseurl }}/config-guide/bk-config-guide.html">配置手册</a>
