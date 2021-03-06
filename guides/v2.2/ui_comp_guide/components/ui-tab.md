---
group: UI_组件_guide
subgroup: 组件
title: 标签页组件
menu_title: 标签页组件
version: 2.2
github_link: ui_comp_guide/components/ui-tab.md
---

## 概述

The 标签页组件 implements a tab content area.

See the [管理面板用到的设计模式和库 (Tabs)]({{ page.baseurl }}/pattern-library/containers/tabs/tabs.html) topic for information about the UI design patterns that can be implemented using the 标签页组件.

## Configuration options

Extends all [`uiCollection`]({{ page.baseurl }}/ui_comp_guide/concepts/ui_comp_uicollection_concept.html) and `tab` configuration.

Tab-specific options:

<table>
  <tr>
    <th>Option </th>
    <th>描述</th>
    <th>Type</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><code>component</code></td>
    <td>The path to the component’s JS constructor, in terms of RequireJS.</td>
    <td>String</td>
    <td><code>Magento_Ui/js/form/组件/area</code></td>
  </tr>
  <tr>
    <td><code>template</code></td>
    <td>The path to the component’s <code>.html</code> template.</td>
    <td>String</td>
    <td><code>templates/layout/tabs/tab/default</code></td>
  </tr>
  <tr>
    <td><code>uniqueNs</code></td>
    <td>Unique namespace for the component.</td>
    <td>String</td>
    <td><code>params.activeArea</code></td>
  </tr>
</table>
