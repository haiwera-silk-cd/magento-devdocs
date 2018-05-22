---
group: install2
subgroup: 起步
title: 什么是docroot?
menu_title: 什么是docroot?
menu_node:
menu_order: 200
level3_menu_node: level3child
level3_subgroup: basics
version: 2.1
github_link: install-gde/basics/basics_docroot.md
redirect_from: /guides/v1.0/install-gde/basics/basics_docroot.html
functional_areas:
  - Install
  - System
  - Setup
---

web服务的根目录 (通常提供类似_docroot_)来表示你的网站所提供功能的文件的存放的位置，你可以你的web服务默认的docroot,[不放在那将更安全]({{ page.baseurl }}/install-gde/tutorials/change-docroot-to-pub.html). 例如, 安装完成之后你应当严格地限制浏览器访问Magento的某些特定文件。.

不同人的默认的docroot路径是不同的，具体要看
-   所用的操作系统
-   web服务软件(nginx/apache)
-   主机提供商 (如果你用到了)

<div class="bs-callout bs-callout-warning" markdown="1">
作为Magento2安装过程的一部分，你应在docroot下指定一个子目录（通常叫"magento2")，把所有Magento的文件存放在这。所以知道如何找到docroot是百常重要的。
</div>

## 联系你的主机提供商
如果你用到了主机提供商提供的主机，联系他们找到web服务的docroot,例如
 <a href="http://support.hostgator.com/articles/cpanel/what-is-a-document-root-folder" target="\_blank">cPanel</a>默认使用`public_html`作为docroot, 但你要根据你的情况找服务商确认.

## 找到你自己的docroot
这里假设你已经安装好了[Apache服务](https://httpd.apache.org/docs/2.4/vhosts/){:target="\_blank"}或[nginx服务](https://www.nginx.com/resources/wiki/start/topics/examples/server_blocks/){:target="\_blank"}.

<div class="bs-callout bs-callout-info" id="info" markdown="1">
你可以配置_虚拟主机(apache)_和_服务站点(nginx)_在一台主机上运行多个站点，比如(e.g., `company1.example.com`和`company2.example.com`)，也可以直接覆盖服务器默认的docroot，而不用更改apache的或nginx的配置.
</div>

找到你自己的docroot:

1.  用编辑器打开下面的文件:

    -   **Ubuntu**

        ```
        /etc/apache2/sites-available/000-default.conf (Apache)
        /etc/nginx/sites-available/default (nginx)
        ```

    -   **CentOS**

        ```
        /etc/httpd/conf/httpd.conf (Apache)
        /etc/nginx/nginx.conf (nginx)
        ```

2.  搜索`DocumentRoot`或`root`.

    典型地, Apache的docroot在Ubuntu _和_ CentOS下者是 `/var/www/html` 而nginx的docroot在CentOS下则是`/usr/share/nginx/html`. 例如:

    -   **Apache + Ubuntu/CentOS**

        ```
        DocumentRoot "/var/www/html"
        ```

    -   **nginx + CentOS**

        ```
        root      /usr/share/nginx/html
        ```
