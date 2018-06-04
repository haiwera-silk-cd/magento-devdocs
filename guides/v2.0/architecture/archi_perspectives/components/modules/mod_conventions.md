---
group: arch-guide
subgroup: Components
title: 模块规范
menu_title: 模块规范
menu_order: 5
level3_menu_node: level3child
level3_subgroup: modules
version: 2.0
github_link: architecture/archi_perspectives/components/modules/mod_conventions.md
redirect_from:
  - /guides/v1.0/architecture/modules/mod_conventions.html
  - /guides/v2.0/architecture/modules/mod_conventions.html
---

## 概述 {#m2arch-module-conventions-overview}

模块必须符合Magento习惯，涉及代码位置和文件名。工作和开发的时候请记住这些习惯.

务必要去研究附加的Magento的习惯，这超出了本文讨论可应用于模块的范围，更多信息请参考<a href="{{ page.baseurl }}/coding-standards/bk-coding-standards.html">编码规范</a>.

## 模块位置习惯 {#m2arch-module-conventions-location}

下面的表格展示了 *推荐的* Magento文件系统内的指定组件的位置

({% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %}在其根目录下必须包含一个`registration.php`文件)

我们提供组件根目录，作为你开发组件代码的最顶层目录。典型地，这些目录是以下Magento根目录下的目录之一:

|实体|位置|
|---|---|
|你定义的模块代码目录|`/app/code/<Vendor>/<Module>`|
|自定义主题文件(网店前台)|`/app/design/frontend/<Vendor>/<theme>`|
|自定义主题文件(模块)|`<Module>/<theme>`|
|如果你想使用一个库|`/lib/<Vendor_Library>`|
