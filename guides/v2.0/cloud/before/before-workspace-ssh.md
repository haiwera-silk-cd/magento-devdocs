---
group: cloud
subgroup: 080_setup
title: 启用ssh密钥登录
menu_title: 启用ssh密钥登录
menu_order: 20
menu_node:
version: 2.0
github_link: cloud/before/before-workspace-ssh.md
redirect_from:
  - /guides/v2.0/cloud/before/before-setup-env-1_get-start.html
  - /guides/v2.1/cloud/before/before-setup-env-1_get-start.html
  - /guides/v2.2/cloud/before/before-setup-env-1_get-start.html
functional_areas:
  - Cloud
  - Setup
---

#### 前提:
[安装Magento所需的必要软件]({{ page.baseurl }}/cloud/before/before-workspace-magento-prereqs.html)

The [SSH protocol ](https://en.wikipedia.org/wiki/Secure_Shell){:target="_blank"} is designed to maintain a secure connection between two systems&mdash;in this case, your local working environment and your {{site.data.var.ece}} Git project.

When initially setting up your local environment, you need to add the SSH keys to the following specific environments:

* Starter: Add to Master (Production) and any environments you create by branching from Master
* Pro: Add to Master Integration environment. After your Staging and Production environments are provisioned, you can add the SSH keys to those environments through the Project Web Interface or via SSH and CLI commands.

{% include cloud/enable-ssh.md %}


#### 下一步:
[设置Magento文件系统所有者]({{ page.baseurl }}/cloud/before/before-workspace-file-sys-owner.html)
