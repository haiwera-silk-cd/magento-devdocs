---
group: UI_组件_guide
subgroup: 组件
title: 单/复选框组组件
menu_title: 单/复选框组组件
version: 2.2
github_link: ui_comp_guide/components/ui-checkboxset.md
---

## 概述

The 单/复选框组组件 implements a group of `<input type="checkbox">`或`<input type="radio">` selection elements.

## Configuration options

Extends all `abstract` configuration.

Checkboxset-specific configuration:

<table>
  <tr>
    <th>Option </th>
    <th>描述</th>
    <th>Type</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><code>component</code></td>
    <td>The path to the component’s <code>.js</code> file in terms of RequireJS.</td>
    <td>String</td>
    <td><code>Magento_Ui/js/form/element/checkbox-set</code></td>
  </tr>
  <tr>
    <td><code>multiple</code></td>
    <td>Set the input type in the UI: <code>true</code> for checkbox, <code>false</code> for radio button.</td>
    <td>Boolean</td>
    <td><code>true</code></td>
  </tr>
  <tr>
    <td><code>options</code></td>
    <td>The array of the options to be displayed in the list for selection.</td>
    <td>Array</td>
    <td><code>[]</code></td>
  </tr>
  <tr>
    <td><code>template</code></td>
    <td>The path to the component’s <code>.html</code> template.</td>
    <td>String</td>
    <td><code>ui/form/element/checkbox-set</code></td>
  </tr>
</table>
