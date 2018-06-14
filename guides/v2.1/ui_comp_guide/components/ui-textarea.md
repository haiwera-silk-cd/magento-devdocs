---
group: UI_组件_guide
subgroup: 组件
title: 文本输入框组件
menu_title: 文本输入框组件
version: 2.1
github_link: ui_comp_guide/components/ui-textarea.md
---

## 概述

The 文本输入框组件 implements the `<textarea>` form field.

## Textarea configuration
Extends all `abstract` configuration.

Textarea-specific options:

<table>
  <tr>
    <th>
      Option
    </th>
    <th>
      Description
    </th>
    <th>
      Type
    </th>
    <th>
      Default
    </th>
  </tr>
  <tr>
    <td>
      <code>cols</code>
    </td>
    <td>
      The number of columns that will be specified in the
      <code>cols</code> attribute of the textarea DOM element.
    </td>
    <td>
      Number
    </td>
    <td>
      <code>15</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>component</code>
    </td>
    <td>
      The path to the component’s .js file in terms of RequireJS.
    </td>
    <td>
      String
    </td>
    <td>
      <code>'Magento_Ui/js/form/element/textarea'</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>elementTmpl</code>
    </td>
    <td>
      The path to the <code>.html</code> template of the particular
      type of field (textarea).
    </td>
    <td>
      String
    </td>
    <td>
      <code>'ui/form/element/textarea'</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>rows</code>
    </td>
    <td>
      The number of columns that will be specified in the
      <code>rows</code> attribute of the textarea DOM element.
    </td>
    <td>
      Number
    </td>
    <td>
      <code>2</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>template</code>
    </td>
    <td>
      The path to the general field <code>.html</code> template.
    </td>
    <td>
      String
    </td>
    <td>
      <code>'ui/form/field'</code>
    </td>
  </tr>
</table>
