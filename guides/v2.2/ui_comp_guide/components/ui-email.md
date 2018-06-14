---
group: UI_组件_guide
subgroup: 组件
title:  邮件组件
menu_title: 邮件组件
version: 2.2
github_link: ui_comp_guide/components/ui-email.md
---

## 概述

The 邮件组件 implements the {% glossarytooltip a2aff425-07dd-4bd6-9671-29b7edefa871 %}HTML{% endglossarytooltip %} `<input type="email">` form field.

## Email configuration

Extends all `abstract` configuration.

Email-specific configuration:

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
    <td><code>Magento_Ui/js/form/element/abstract</code></td>
  </tr>
  <tr>
    <td><code>elementTmpl</code></td>
    <td>The path to the <code>.html</code> template of the particular field type.</td>
    <td>String</td>
    <td><code>ui/form/element/email</code></td>
  </tr>
  <tr>
    <td><code>template</code></td>
    <td>The path to the general field <code>.html</code> template.</td>
    <td>String</td>
    <td><code>ui/form/field</code></td>
  </tr>
</table>
