---
group: mrg
subgroup: 30_B2B
title: Magento_GiftCardSharedCatalog模块
menu_title: GiftCardSharedCatalog
menu_order: 130
version: 2.2
github_link: mrg/b2b/GiftCardSharedCatalog.md
functional_areas:
  - B2B
---

## 概述

The `Magento_GiftCardSharedCatalog` module enables gift cards to be added to a shared catalog in an B2B environment. This module extends `Magento_SharedCatalog` and `Magento_GiftCard` modules.

The `Magento_GiftCardSharedCatalog` module provides the following features:

* Display and manage prices for gift cards within a shared catalog.

* Control the visibility of gift cards in quotes and orders. Only those gift card products that have been added to a shared catalog will be available for searches via the "Add by SKU" feature in quotes and orders.

## Installation details

The `Magento_GiftCardSharedCatalog` module has a dependency on the `Magento_SharedCatalog` and `Magento_GiftCard` modules, which must be installed and enabled first. This module does not create any backward incompatible changes. It can be uninstalled or deactivated at any time.

## 结构

[Learn about a typical file structure for a Magento 2 module]({{ page.baseurl }}/extension-dev-guide/build/module-file-structure.html).

## 可扩展性

Extension developers can interact with the Magento_GiftCardSharedCatalog模块. For more information about the Magento extension mechanism, see [Magento plug-ins]({{ page.baseurl }}/extension-dev-guide/plugins.html).

[The Magento dependency injection mechanism]({{ page.baseurl }}/extension-dev-guide/depend-inj.html) enables you to override the functionality of the Magento_GiftCardSharedCatalog模块.

### Layouts

You can extend and override layouts in the `Magento\GiftCardSharedCatalog\view\adminhtml\layout` directories.

For more information about layouts, see the [Layout documentation]({{ page.baseurl }}/frontend-dev-guide/layouts/layout-overview.html).

### UI 组件

The following directory contains extensible UI 组件:

* `Magento\GiftCardSharedCatalog\view\adminhtml\ui_component` - renderer for pricing and structure listings

For more information, see [UI Listing/Grid Component]({{ page.baseurl }}/ui_comp_guide/components/ui-listing-grid.html).

## Additional information

You can track [backward incompatible changes made in a Magento B2b mainline after the Magento 2.2 release]({{ page.baseurl }}/release-notes/changes/b2b_changes.html).
