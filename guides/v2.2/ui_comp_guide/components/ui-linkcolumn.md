---
group: UI_组件_guide
subgroup: 组件
title: Link表格列组件
menu_title: Link表格列组件
version: 2.2
github_link: ui_comp_guide/components/ui-linkcolumn.md
---

## Overview

The Link表格列组件 implements a column that can display the anchor elements instead of plain text.

Constructor: [app/code/Magento/Ui/view/base/web/js/grid/columns/link.js]({{ site.mage2200url }}app/code/Magento/Ui/view/base/web/js/grid/columns/link.js)

## LinkColumn configuration

Extends all [Column]({{ page.baseurl }}/ui_comp_guide/components/ui-column.html) configuration.

LinkColumn-specific configuration:

<table>
  <tr>
    <th>Option</th>
    <th>描述</th>
    <th>Type</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><code>link</code></td>
    <td>The key in a field's record object that contains the link value.</td>
    <td>String</td>
    <td><code>link</code></td>
  </tr>
</table>
