---
group: mrg
title: Magento_LayeredNavigationStaging模块
version: 2.1
ee_only: true
github_link: mrg/ee/LayeredNavigationStaging.md
---

The Magento_LayeredNavigationStaging {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %} is a part of the staging functionality in {{site.data.var.ee}}.
It restricts functionality of the Magento_LayeredNavigationStaging模块 in the staging preview mode.

## Implementation details

The Magento_LayeredNavigationStaging模块 disables the Magento_LayeredNavigation模块 functionality in the staging preview mode.

## Dependencies

You can find the list of modules that have dependencies on the Magento_LayeredNavigationStaging模块 in the `require` section of the `composer.json` file. The file is located in the root directory of the module.

## Extension points

{% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}Extension{% endglossarytooltip %} points enable extension developers to interact with the Magento_LayeredNavigationStaging模块. [The Magento dependency injection mechanism](http://devdocs.magento.com/guides/v2.1/extension-dev-guide/depend-inj.html) enables you to override the functionality of the Magento_LayeredNavigationStaging模块.

### Layouts

You can extend and override layouts in the `Magento/LayeredNavigationStaging/view/frontend/layout/` directory.
For more information about layouts, see the [Layout documentation](http://devdocs.magento.com/guides/v2.1/frontend-dev-guide/layouts/layout-overview.html).

## Additional information

You can track [backward incompatible changes made in a {{site.data.var.ee}} mainline after the Magento 2.0 release](http://devdocs.magento.com/guides/v2.0/release-notes/backward-incompatible-changes/commerce.html).
