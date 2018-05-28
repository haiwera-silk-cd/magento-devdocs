---
group: UI_组件_guide
subgroup: 组件
title: 数据列组件
menu_title: 数据列组件
version: 2.1
github_link: ui_comp_guide/组件/ui-datecolumn.md
---

## Overview

The 数据列组件 implements a table column that displays dates.

DateColumn сonstructor: [app/code/Magento/Ui/view/base/web/js/grid/columns/date.js]({{ site.mage2200url }}app/code/Magento/Ui/view/base/web/js/grid/columns/date.js)

## Сonfiguration options

Extends all [Column]({{ page.baseurl }}/ui_comp_guide/components/ui-column.html) configuration.

DateColumn specific configuration:

<table>
  <tr>
    <th>Option</th>
    <th>描述</th>
    <th>Type</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><code>dateFormat</code></td>
    <td>Date format for the displayed column's values.</td>
    <td>String</td>
    <td><code>MMM d, YYYY h:mm:ss A</code></td>
  </tr>
</table>
