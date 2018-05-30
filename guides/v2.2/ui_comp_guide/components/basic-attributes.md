---
group: UI_组件_guide
subgroup: 组件
title: Basic attributes
menu_title: Basic attributes
menu_order: 1
version: 2.2
github_link: ui_comp_guide/components/basic-attributes.md
---

## Overview

This topic describes the general UI components configuration attributes. There's a set of attributes available for all UI components, and a set of attributes which are specific for [basic components]({{ page.baseurl }}/ui_comp_guide/bk-ui_comps.html#general-structure) only. 

## General attributes 

The following attributes are available for all UI 组件, including the basic UI 组件.

<table>
  <tr>
    <th>Option </th>
    <th>描述</th>
    <th>Type</th>
  </tr>
  <tr>
    <td><code>class</code></td>
    <td>The name of associated PHP interface.</td>
    <td>String</td>
  </tr>
  <tr>
    <td><code>component</code></td>
    <td>The path to the component’s <code>.js</code> file.</td>
    <td>String</td>
  </tr>
  <tr>
    <td><code>displayArea</code></td>
    <td>The name of parent component's template region where component needs to be rendered (the list of available regions defined by the template).</td>
    <td>String</td>
  </tr>
  <tr>
    <td><code>sortOrder</code></td>
    <td>Component's sort order.</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td><code>template</code></td>
    <td>The path to the component’s <code>.html</code> template.</td>
    <td>String</td>
  </tr>
</table>


## Basic 组件' options

The following options are available for all basic 组件:

<table>
  <tr>
    <th>Option </th>
    <th>描述</th>
    <th>Type</th>
  </tr>
  <tr>
    <td><code>extends</code></td>
    <td>Reference to a UI component whose configuration to inherit. Only a basic component can be specified.</td>
    <td>String</td>
  </tr>
  <tr>
    <td><code>provider</code></td>
    <td>The path in the <a href="{{ page.baseurl }}/ui_comp_guide/concepts/ui_comp_uiregistry.html">registry</a> to the linked data provider.</td>
    <td>String</td>
  </tr>
</table>


