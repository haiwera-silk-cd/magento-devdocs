# Magento 中文文档

欢迎使用Magento中文文档，由于此文档使用Jekyll在github上编译会出现超时问题，故本文档每周五从master由笔者本地编译到gh-pages分支。请不要直接在gh-pages分支上进行翻译。本仓库起于[magento/devdocs ddec2e4af6d](https://github.com/magento/devdocs/commit/ddec2e4af6d9d96579ac58ef98207a8eaaa8f688),最后更新日期为2018年5月27. 英文文档请参考[Magento Devdocs](https://devdocs.magento.com)

为了减小本仓库大小以方便贡献者克隆，本文档所有图片、PDF、zip文件引用[Magento Devdocs](https://devdocs.magento.com)原网站内容，在`_config.yml`中定义了变量`magentourl`，笔者已悉数修改，若有遗漏，欢迎参与修改。

# 站点环境构建

你可以使用下面的方式在本地构建文档站点:

- [安装本地项目依赖](#build-using-jekyll) (Mac, Linux)
- [使用docker容器](#build-using-docker) (Mac, Linux)
- [使用Vagrant虚拟机](#build-using-vagrant) (Mac, Linux, Windows)

## 使用Jekyll构建

为了保证能在本地进行构建，你须要安装Ruby 2.4或更新。

要检查您的系统的Ruby版本，可以在终端执行

```shell
$ ruby -v
```

### 安装最新版的Ruby (如果您的Ruby版本小于2.4)

**MacOS 用户**

1. 安装 Homebrew. 安装指令请参考[Homebrew site](https://brew.sh).
2. 使用homebrew安装最新版的Ruby:
 
   ```
   $ brew install ruby
   ```

**Unix, Windows或其它系统的用户**

请参考[Ruby site](https://www.ruby-lang.org/en/documentation/installation)安装.

### 安装Bundler

安装[Bundler](http://bundler.io/) gem,用于解决Ruby依赖:

```
$ gem install bundler
```

一但你完成上述步骤，你便可以在本地构建并使用浏览器来查看你的文档站点了。

### 安装devdocs

克隆或下载本仓库，完成后首先你会进到`devdocs`目录，执行

```
$ bundle install
```

### 本地构建:

#### 使用rake

[rake](https://github.com/ruby/rake)是一个本地的Ruby工具，用于自动化任务。 

1.使用rake请求所有依赖并启动[Jekyll](https://jekyllrb.com/)服务:

   ```
   $ rake preview
   ```

1. 按`Ctrl+C`终止命令.

如果rake在你的环境出现错误，请[using jekyll](#using-jekyll)

#### 使用Jekyll

1. 首先来到`devdocs`目录，当你要应用你的`Gemfile.lock`改变时（比如，主题改变)请使用下面的命令来重新解决依赖.

   ```
   $ bundle install
   ```

1. 生成本地预览

   ```
   $ bundle exec jekyll serve --incremental
    
    Configuration file: /Users/username/Github/devdocs/_config.yml
                Source: /Users/username/Github/devdocs
           Destination: /Users/username/Github/devdocs/_site
     Incremental build: enabled
          Generating...
                        done in x.x seconds.
     Auto-regeneration: enabled for '/Users/username/Github/devdocs'
        Server address: http://127.0.0.1:4000//
      Server running... press ctrl-c to stop.
   ```

1. 使用 **服务器地址** `http://127.0.0.1:4000/`在浏览器查看站点

1. 按`Ctrl+C`终止命令

> ***小提示***  
> 离开服务终端打开并执行，每当你保存某个文件的修改，它将自动重成重新生成站点，因此你可以立即测试输出的内容。修改`_config.yml`文件必须要重新构建。使用`--incremental`选项将限制重新构建修改的页面

### 本地最小化构建时间

1. 在项目跟目录创建一个`_config.local.yml`文件，排除所有你不须要的版本

下面的例子将只生成Magento2.2的文档

   ```yaml
    exclude:
     - community/
     - swagger/
     - vagrant/
     - guides/m1x/
     - guides/v2.0/
     - guides/v2.1/
    # - guides/v2.2/
     - guides/v2.3/
    
    # Excluded in config.yml
     - scss/
     - bin/
     - node_modules/
     - vendor/
     - .*
     - Rakefile
   ```

1. 执行预览命令

   ```
   $ rake preview
   ```
   此命令将：
   * 根据`Gemfile.lock`检查你的环境所需的依赖:
   * 删除包含了之前生成结果的`_site/`目录
   * 生成新的预览并在浏览器打开
   
如果在你的`devdocs/`目录下没有`_config.local.yml`文件,rank将为所有版本生成文档

## 使用docker构建


本仓库已经有了docker必要的用于构建Devdocs的配置文件,参考[Docker](https://docs.docker.com/), 使用[Docker Compose](https://docs.docker.com/compose/overview/).

要使用docker和docker compose，首先要下载并安装与你的系统相应的docker，然后安装docker composer来执行`docker-composer.yml`配置文件

### Mac下使用Docker
- 参考 [这里](https://docs.docker.com/docker-for-mac/install/),了解官方的安装命令. 

### Docker for Windows
- 参考 [这里](https://docs.docker.com/docker-for-windows/install/),了解官方的安装命令.

### Docker Compose
- 参考 [这里](https://docs.docker.com/compose/install/),了解官方的安装命令.

### 执行步骤
1. 使用 [git](https://git-scm.com/), [clone](https://help.github.com/articles/cloning-a-repository/)本仓库.
2. 定位到你的安装目录
3. 执行 `docker-compose up`来初始化构建过程. 参考 [这里](https://docs.docker.com/compose/gettingstarted/#step-build-and-run-your-app-with-compose)，了解更多`docker-compose`的细节.
4. 在浏览器访问`http://localhost:4000/`, 你可以看到一个本地的devdocs文档. 你可以在[docker-compose.yml](https://github.com/magento/devdocs/blob/develop/docker-compose.yml)文件中找到你默认配置的端口 (默认情况下是`4000`).如果你要使用其它端口, 请参考[这里](https://docs.docker.com/compose/compose-file/compose-file-v2/#ports),了解Docker composer端口映射的特性及细节。

### docker构建的问题定位
1. 验证你的系统的docker引擎是否安装
2. 验证docker composer是否安装 
3. 验证仓库是否克隆正确
4. 验证你是否在`docker-composer.yml`相同的目录下执行了正确的docker compose命令
5. 如果还有问题，请在此向我们提交你的[问题](https://help.github.com/articles/creating-an-issue/)

## 使用Vagrant构建

你可以在本地使用[this Vagrant project](https://github.com/magento-devdocs/vagrant-for-magento-devdocs)部署devdocs站点

***

如果你遇到任何问题，请向我们提交你的问题，我们将密切关注

*	<a href="https://twitter.com/MagentoDevDocs" class="twitter-follow-button" data-show-count="false">Follow @MagentoDevDocs</a>

*	<a href="mailto:DL-Magento-Doc-Feedback@magento.com">发送邮件</a>

*	<a href="http://magento.haiwera.xyz">打开中文文档</a>, 构建[GitHub pages](https://pages.github.com/).
*	<a href="http://devdocs.magento.com">打开英文文档</a>

## 支持

*   <a href="http://www.silksoftware.com">成都思而科软件有限公司</a> - <a href="http://haiwera.xyz">Haiwera</a>
