---
group: cloud
subgroup: 080_setup
title: 导入现存的代码到项目
menu_title: 导入现存的代码到项目
menu_order: 151
menu_node:
level3_menu_node: level3child
level3_subgroup: import
version: 2.0
github_link: cloud/access-acct/first-time-setup_import-first-steps.md
redirect_from:
  - /guides/v2.0/cloud/access-acct/first-time-setup_import-prereq.html
  - /guides/v2.1/cloud/access-acct/first-time-setup_import-prereq.html
  - /guides/v2.2/cloud/access-acct/first-time-setup_import-prereq.html
  - /guides/v2.3/cloud/access-acct/first-time-setup_import-prereq.html
functional_areas:
  - Cloud
  - Setup
---

你可以从一个空模板创建一个{{site.data.var.ece}}的项目，或导入现有代码来创建。我们推荐使用一个空模板来开始，然后这之基础上导入现有的Magento代码

<div class="bs-callout bs-callout-info" markdown="1">
你不能以导入现存代码的方式创建试验项目。
</div>

## 导入代码的先决条件 {#prereqs}
开始之前, 请完成以下操作:

-   添加现存{{site.data.var.ee}}的代码到git仓库。我们推荐使用[GitHub]({{ page.baseurl }}/cloud/project/project-integrate-github.html).
-   设置你的 [本地开发环境]({{ page.baseurl }}/cloud/access-acct/first-time-setup.html).
-   收集必要的信息：

    -    目标环境的[SSH访问链接](#ssh)
    -    [数据库认证信息](#db-creds)

### SSH访问云环境 {#ssh}
要传输数据库备份和文件到{{site.data.var.ece}},你必须知道SSH访问链接。你可以使用[`magento-cloud`命令行工具]({{ page.baseurl }}/cloud/reference/cli-ref-topic.html)找到SSH的访问链接

  magento-cloud environment:ssh --pipe

<div class="bs-callout bs-callout-info" id="info" markdown="1">
你必须在你的存有Cloud SSH密钥的机器上输入所有{{site.data.var.ece}}的命令，更多信息请参考[启用ssh密钥登录]({{ page.baseurl }}/cloud/before/before-workspace-ssh.html)和[SSH和sFTP]({{ page.baseurl }}/cloud/env/environments-ssh.html).
</div>

### 数据库认证信息 {#db-creds}
你须要你的{{site.data.var.ece}}数据库名和认证信息，如些你便导入{{site.data.var.ee}}的数据。你可以在`$MAGENTO_CLOUD_RELATIONSHIPS`环境变量中找到数据库名和认证信息。

要找到{{site.data.var.ece}}的数据库访问信息：

1. 使用[SSH]({{ page.baseurl }}/cloud/env/environments-ssh.html#ssh)登录到你的远程仓库。

        magento-cloud ssh -p <project ID> -e <environment ID>

1.  列出所有数据库信息：

        echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp

        <pre class="no-copy">database" : [
              {
                 "username" : "user",
                 "query" : {
                    "is_master" : true
                 },
                 "path" : "main",
                 "port" : 3306,
                 "host" : "database.internal",
                 "password" : "",
                 "scheme" : "mysql",
                 "ip" : "192.0.2.150"
              }
           ]</pre>

上例中，数据库名是`main`，端口是`3306`，主机名是`database.internal`，root用户名是`user`，并且此用户没有密码。

### 云非安全基础URL
在你导入 {{site.data.var.ee}}数据库信息到{{site.data.var.ece}}之后，你必须修改基础URL，这样你就可以访问Magento管理面板和网店前台了。

使用magento-cloud命令行工具查看基础URL:

    magento-cloud url

## 导入现存代码的工作流 {#import}
导入现存代码的完整的工作流程包括以下的步骤：

1.  如果你没有项目，[从模板创建一个新的项目](#cloud-import-proj).新的项目有针对{{site.data.var.ece}}的文件和目录。
1.  例用Git用自己的代码[替换内容]({{ page.baseurl }}/cloud/access-acct/first-time-setup_import-import.html) of this project with your code using Git.
1.  [导入你的Magento数据库]({{ page.baseurl }}/cloud/access-acct/first-time-setup_import-import.html#cloud-import-db)到{{site.data.var.ece}}工程。
1.  [导入静态文件]({{ page.baseurl }}/cloud/access-acct/first-time-setup_import-import.html#media)到你的{{site.data.var.ece}}工程。
1.  拷贝你的{{site.data.var.ee}}的[密钥]({{ page.baseurl }}/cloud/access-acct/first-time-setup_import-import.html#encryption-key)到你的{{site.data.var.ece}}工程，这个密钥在数据迁移和访问时是必需的。
1.  清除{% glossarytooltip 0bc9c8bc-de1a-4a06-9c99-a89a29c30645 %}缓存{% endglossarytooltip %}并验证项目是否导入成功.

## 创建一个新的{{site.data.var.ece}}项目 {#cloud-import-proj}

1.  访问你的账号，打开你从Magento Cloud(accounts@magento.cloud)收到的邮件并点击 _立即访问你的项目_ ，或你也可以登录到[你的Magento账号](https://accounts.magento.cloud){:target="\_blank"}.

1.  点击 _此项目暂时还没有代码_ 下一步到填写项目名称

	![没有代码的项目]({{ site.magentourl }}/common/images/cloud_project_empty.png)

1.  填写项目名称。

	![项目名称]({{ site.magentourl }}/common/images/cloud_project_name.png)

1.  点击 **从模板创建一个空站点** 然后点击 **继续**。我们推荐你以Magento模板作为你的初始项目选项开始，如果你有一个已经存在的Magento部署，你可以在之后导入现存代码。

	![使用样本Magento项目创建一个站点]({{ site.magentourl }}/common/images/cloud_project_template.png){:width="650px"}

1. 当弹出提示时，在弹出的输入框输入你的{{site.data.var.ee}}的[Magento authentication keys]({{ page.baseurl }}/install-gde/prereq/connect-auth.html)。你之前在Magento市场创建了这些密钥。输入私钥和公钥然后点击 **完成**

	![输入认证密钥]({{ site.magentourl }}/common/images/cloud-project-magento-auth-creds.png){:width="650px"}

	密钥会被添加到`auth.json`文件中，并且此文件所有分支和部署环境都要有。

1.  你的项目部署要等几分钟，完成这前会显示 _Pending_  的状态，如下图所示：

	![你的样本Magento项目]({{ site.magentourl }}/common/images/cloud_project_template2.png){:width="650px"}

1.  项目部署完后，**成功** 会显示在你的项目名称旁边

#### 下一步
[准备你的现存的Magento企业版的安装]({{ page.baseurl }}/cloud/access-acct/first-time-setup_import-prepare.html)
