---
group: UI_组件_guide
subgroup: 组件
title: 范围筛选组件
menu_title: 范围筛选组件
version: 2.1
github_link: ui_comp_guide/components/ui-range.md
---

## 概述

The 范围筛选组件 implements the range for filtering rows in a grid. Visually, this component represents two input fields of `date`或`text` type, for entering the "from" and "to" range limits.

Constructor: [app/code/Magento/Ui/view/base/web/js/grid/filters/range.js]({{ site.mage2200url }}app/code/Magento/Ui/view/base/web/js/grid/filters/range.js)

## Range configuration

Extends all [Multiline]({{ page.baseurl }}/ui_comp_guide/components/ui-multiline.html) configuration.

Range-specific configuration:

<table>
  <tr>
    <th>Option</th>
    <th>描述</th>
    <th>Type</th>
    <th>Default Value</th>
  </tr>
  <tr>
    <td><code>rangeType</code></td>
    <td>Defines what kind of input elements the range contains. For example, if the value is <code>date</code>, then range includes two date fields.</td>
    <td>String</td>
    <td>-</td>
  </tr>
  <tr>
    <td><code>template</code></td>
    <td>Path to the component’s <code>.html</code> template.</td>
    <td>String</td>
    <td><code>ui/grid/filters/elements/group</code></td>
  </tr>
</table>
