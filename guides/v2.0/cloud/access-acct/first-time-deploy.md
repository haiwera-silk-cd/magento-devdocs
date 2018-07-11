---
group: cloud
subgroup: 080_setup
title: 首次部署
menu_title: 首次部署
menu_order: 60
version: 2.0
github_link: cloud/access-acct/first-time-deploy.md
functional_areas:
  - Cloud
  - Setup
  - Deploy
---

#### 前提:
[安装Magento]({{ page.baseurl }}/cloud/before/before-setup-env-install.html)

<div class="bs-callout bs-callout-info" id="info" markdown="1">
对于一个新的 **Pro project** 你仅须要完成此步一次，起步项目的代码已经在`master`上。作为最佳实践，你必须有Magento项目模板(或`master`分支)完整部署到所有环境以确保所有未来代码的推送正确部署。
</div>

完全设置你本地工作环境之后，为了 **定制化开发**， 你本地应有克隆的集成`master`分支。要完成初始化设置，我们 **强列推荐完全部署** `master`分支到准生产及生产环境。你只须要从集成环境一次推送代码到准生产及生产环境，不进行任何更改。这就已经完整安装了基础Magento应用到两个环境中了。

初始化推送提供了下面的好处：

* 完全安装Magento到每个环境
* 允许构建/部署脚本使用`setup:upgrade`代替`setup:install` ，(对添加扩展是重要的)
* 推送Magento密钥到所有环境
* 在安装和添加模块或扩展时项目不会报错或失败

  在 setup:install 命令和应用程序模式下，不是所有的扩展都是被正确测试过的。如果你初始安装Magento代码时添加了三方扩展或自定义代码，可能会报错或构建/部署失败。而部署没有修改的Magento模板，所有未来的对准生产和生产环境的开发通常不会遇到三方库或自定义代码的安装问题。

## 先决条件 {#prereqs}
要部署，你需要：

* 一个没有修改的Magento的模板项目的`master`分支(创建的项目使用导入选项可能会遇到问题)
* 准生产和生产环境
* SSH访问到准生产和生产环境

## 创建工单 {#ticket}
如果你须要提供的环境和SSH访问，可以发起一个[支持工单]({{ page.baseurl }}/cloud/trouble/trouble.html).

要请求环境供应，你必须要支付了Magento企业版(云支持版)的订阅并与Magento完成了一个电话沟通

<div class="bs-callout bs-callout-info" id="info" markdown="1">
如果你只是进行专业试验而没有准生产和生产环境，你是不能完成初始部署的，要继续部署，从集成`master`创建一个分支。不要合并这些代码到你的`master`分支，直到你已经部署它到你的提供的准生产和生产环境。
</div>

要进行SSH访问，请在工单为环境提供SSH公钥，你会从Magento返回的项目信息中收到环境的SSL访问URL。

## 部署到准生产和生产环境 {#deploy}
项目的Web接口为起步和定制计划提供了完整的特性来创建，管理，和部署代码分支到你的集成、准生产、生产环境。你也可以使用SSH和CLI命令来完成这些过程。先前，为定制划，你只能在准生产和生产环境使用SSH和CLI命令

为了定制计划，部署你创建的分支到准生产和生产不境。

1. [登录](https://accounts.magento.cloud)到你的项目.
2. 选择你创建的分支。
3. 选择 **合并** 选项部署到准生产环境。
4. 选项准生产环境的分支。
5. 选择 **合并** 选项部署到生产环境。

![使用合并选项部署]({{ site.magentourl }}/common/images/cloud_project-merge.png)

## 使用SSH部署 {#ssh}
如果你更喜欢使用命令行来部署，你将必须配置附加的SSH设置和Git仓库来使用命令。你可以SSH登录到准生产环境和生产环境来推送`master`分支。

你将需要你有项目ID的SSH和git，格式如下

*	Git URL格式:

	*	准生产环境: `git@git.ent.magento.cloud:<project ID>_stg.git`
	*	生产环境: `git@git.ent.magento.cloud:<project ID>.git`

*	SSH URL格式:

	*	准生产环境: `<project ID>_stg@<project ID>.ent.magento.cloud`
	*	生产环境: `<project ID>@<project ID>.ent.magento.cloud`

作为推送代码的一部分，你可能要：

* [设置远程Git仓库](#cloud-live-migrate-git)
* 在环境中[设置SSH代理](#cloud-live-migrate-agent)

完成以上设置之后，你可以使用SSH登录到环境并使用git命令来推送分支了。

### 设置远程GIT仓库 {#cloud-live-migrate-git}
当你知道你的git URL时，你必须设置它作为远程上游仓库，这样你就可以推送代码上去了。

命令语法:

	git remote add <remote repository name> <remote repository URL>

例如，

	git remote add staging git@git.ent.magento.cloud:dr5q6no7mhqip_stg.git
	git remote add prod git@git.ent.magento.cloud:dr5q6no7mhqip.git

### 设置你的SSH代理 {#cloud-live-migrate-agent}
你可以使用任何一个你更喜欢的ssh客户端或参考[推荐工具]({{ page.baseurl }}/cloud/before/before-workspace.html#recommended-tools)。这里我们以OpenSSH客户端为例。

SSH代码转发验证请求从准生产或生产环境来你的Magento工作的系统上(这表示，你本地的环境)，SSH代理允许你使用一个本地的私钥从准生产和生产环境主机登录到远程服务器。有了这个SSH代理，你可以非常方便地在准生产或生产环境与本地或其它远程主机之间复制文件

设置SSH代理：

1.	登录到本地开发机。
2.	输入下面的命令：

		ssh-add -l

	会显示下面的信息之一：

	*	Working SSH agent: `2048 ab:de:56:94:e3:1e:71:c3:4f:df:e1:62:8d:29:a5:c0 /home/magento_user/.ssh/id_rsa (RSA)`

		跳过下一步到步骤 4.
	*	SSH agent not started: `Could not open a connection to your authentication agent.`

		Continue with 步骤3.

3.	要开启动SSH代理，输入下面的命令：

		  eval $(ssh-agent -s)

	执行后，会返回代理的进程ID
4.	添加你的ssh密钥到代理：

		  ssh-add ~/.ssh/id_rsa

	类似下面的消息会显示：

		  Identity added: /home/magento_user/.ssh/id_rsa (/home/magento_user/.ssh/id_rsa)

更多关于设置SSH的信息，请参考[启用ssh密钥登录]({{ page.baseurl }}/cloud/before/before-workspace-ssh.html)作为本地设置的一部分。

### SSH和拉取git分支 {#git}

1. 打开一个SSH连接到你的准生产或生产环境：

    * 准生产环境: `ssh -A <project ID>_stg@<project ID>.ent.magento.cloud`
    * 生产环境: `ssh -A <project ID>@<project ID>.ent.magento.cloud`
2. 拉取`master`分支到服务器。

        git pull origin master

## 你可以开始写代码了！{#code}
当这些代码被部署到以上环境，你就可以开始开发、添加扩展或其它操作了。
