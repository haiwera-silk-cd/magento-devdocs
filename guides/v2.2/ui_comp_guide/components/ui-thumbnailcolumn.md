---
group: UI_组件_guide
subgroup: 组件
title: 缩略图列组件
menu_title: 缩略图列组件
version: 2.2
github_link: ui_comp_guide/components/ui-thumbnailcolumn.md
---

## 概述

The 缩略图列组件 implements a column containing images associated with records of the table. Each field of this column contains an image preview. When a user click on the preview, a pop up window with the detailed view opens.

Constructor: [app/code/Magento/Ui/view/base/web/js/grid/columns/thumbnail.js]({{ site.mage2200url }}app/code/Magento/Ui/view/base/web/js/grid/columns/thumbnail.js)

## ThumbnailColumn configuration

Extends all [Column]({{ page.baseurl }}/ui_comp_guide/components/ui-column.html) configuration.

ThumbnailColumn-specific configuration:

<table>
  <tr>
    <th>Option</th>
    <th>描述</th>
    <th>Type</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><code>bodyTmpl</code></td>
    <td>Path to the template used for rendering a column's fields in the table's body.</td>
    <td>String</td>
    <td><code>ui/grid/cells/thumbnail</code></td>
  </tr>
  <tr>
    <td><code>fieldClass</code></td>
    <td>Additonal CSS classes added to the column's field elements.</td>
    <td><code>{[name: string]: boolean}</code></td>
    <td><code>{'data-grid-thumbnail-cell': true}</code></td>
  </tr>
</table>