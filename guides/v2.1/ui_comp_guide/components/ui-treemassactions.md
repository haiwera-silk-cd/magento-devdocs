---
group: UI_组件_guide
subgroup: 组件
title: 树形下拉操作组件
menu_title: 树形下拉操作组件
version: 2.1
github_link: ui_comp_guide/components/ui-treemassactions.md
---

## 概述

The 树形下拉操作components is a decorator for [MassActions]({{ page.baseurl }}/ui_comp_guide/components/ui-massactions.html) that adds the support of nested actions.

Constructor: [app/code/Magento/Ui/view/base/web/js/grid/tree-massactions.js]({{ site.mage2200url }}app/code/Magento/Ui/view/base/web/js/grid/tree-massactions.js)

## TreeMassActions configuration

Extends all [MassActions]({{ page.baseurl }}/ui_comp_guide/components/ui-massactions.html) configuration.

TreeMassActions-specific configuration:

<table>
  <tr>
    <th>Option</th>
    <th>描述</th>
    <th>Type</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><code>submenuTemplate</code></td>
    <td>Path to the <code>.html</code> template used to render nested actions.</td>
    <td>String</td>
    <td><code>ui/grid/submenu</code></td>
  </tr>
  <tr>
    <td><code>template</code></td>
    <td>Path to the component’s <code>.html</code> template.</td>
    <td>String</td>
    <td><code>ui/grid/tree-massactions</code></td>
  </tr>
  <tr>
    <td><code>actions</code></td>
    <td>A list of available actions.</td>
    <td><code>(MassActionContainer | MassAction)[]</code></td>
    <td>-</td>
  </tr>
</table>

## MassActionContainer interface
<table>
  <tr>
    <th>Option</th>
    <th>描述</th>
    <th>Type</th>
    <th>必需</th>
  </tr>
  <tr>
    <td><code>label</code></td>
    <td>Action's label displayed in the list of actions.</td>
    <td>String</td>
    <td>必需</td>
  </tr>
  <tr>
    <td><code>type</code></td>
    <td>Action's identifier.</td>
    <td>String</td>
    <td>必需</td>
  </tr>
  <tr>
    <td><code>actions</code></td>
    <td>A list of child elements that may contain both MassActionContainer and MassAction instances.</td>
    <td>(MassActionContainer | MassAction)[]</td>
    <td>必需</td>
  </tr>
</table>
