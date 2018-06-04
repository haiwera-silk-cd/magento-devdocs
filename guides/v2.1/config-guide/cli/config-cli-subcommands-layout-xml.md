---
group: config-guide
subgroup: 04_CLI
title: 转换布局的XML文件
menu_title: 转换布局的XML文件
menu_node:
menu_order: 700
version: 2.1
github_link: config-guide/cli/config-cli-subcommands-layout-xml.md
redirect_from: /guides/v1.0/config-guide/cli/config-cli-subcommands-layout-xml.html
functional_areas:
  - Configuration
  - System
  - Setup
---

{% include config/cli-intro.md %}

## Overview of layout XML conversion
Use this command to update your {% glossarytooltip 73ab5daa-5857-4039-97df-11269b626134 %}布局{% endglossarytooltip %} {% glossarytooltip 8c0645c5-aa6b-4a52-8266-5659a8b9d079 %}XML{% endglossarytooltip %} files if you update the corresponding Extensible Stylesheet Language Transformations (XSLT) stylesheet.

For more information about layout XML files, see:

-   [布局指令]({{ page.baseurl }}/frontend-dev-guide/layouts/xml-instructions.html)
-   [布局文件类型]({{ page.baseurl }}/frontend-dev-guide/layouts/layout-types.html)

## 转换布局的XML文件
命令参数：

	bin/magento dev:xml:convert [-o|--overwrite] {xml file} {xslt stylesheet}

here:

-   **`{xml file}`** is the full path and file name of a layout XML file to convert (required)
-   **`{xslt stylesheet}`** is the full path and file name of an XSLT stylesheet file to use for {% glossarytooltip 38c73ce4-8f01-4f74-ab30-1134cec5664f %}conversion{% endglossarytooltip %} (required)
-   **`-o|--overwrite`** include this option to overwrite the existing XML file

#### 相关主题

-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cache.html">管理缓存</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-index.html">管理索引</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-cron.html">配置和执行定时任务</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-compiler.html">代码编译器</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-mode.html">设置Magento的模式</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-urn.html">统一资源名称(URN)高亮</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-depen.html">依赖报告</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-i18n.html">翻译字典和语言包</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html">部署静态视图文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-less-sass.html">创建软链接到LESS文件</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-test.html">运行单元测试</a>
-   <a href="{{ page.baseurl }}/config-guide/cli/config-cli-subcommands-perf-data.html">为性能测试生成数据</a>
