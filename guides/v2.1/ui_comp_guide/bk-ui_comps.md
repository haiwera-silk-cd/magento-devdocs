---
group: UI_组件_guide
subgroup:
title: UI组件概述
landing-page: UI 组件
menu_title: UI组件概述
menu_order: 1
version: 2.1
github_link: ui_comp_guide/bk-ui_comps.md
redirect_from:
  - /guides/v2.1/ui-components/ui-component.html
  - /guides/v2.2/ui-components/ui-component.html
  - /guides/v2.1/ui-components/ui-definition.html
  - /guides/v2.1/ui-components/ui-secondary.html
  - /guides/v2.1/ui-components/ui_components_js.html
  - /guides/v2.1/ui-components/ui-listing-grid.html
  - /guides/v2.1/ui_comp_guide/concepts/ui_comp_architecture_concept.html
  - /guides/v2.1/ui_comp_guide/ui_component_explained.html
---

## UI组件概述
*Magento UI 组件 are used to represent distinct UI elements, such as tables, buttons, dialogs, and others*.

They are designed for simple and flexible user interface (UI) rendering. 组件 are responsible for rendering result page fragments and providing/supporting further interactions of {% glossarytooltip 312b4baf-15f7-4968-944e-c814d53de218 %}JavaScript{% endglossarytooltip %} 组件 and server.

Magento UI 组件 are implemented as a standard {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %} named Magento_UI.

To use UI components in your custom module, you need to add a dependency for the Magento_UI模块 in [your component's composer.json file]({{ page.baseurl }}/extension-dev-guide/build/composer-integration.html).

The following XSD file contains rules and limitations shared between all 组件 (both definitions and instance configurations):

`<your module root dir>/Magento/Ui/etc/ui_definition.xsd`

{% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}Extension{% endglossarytooltip %} developers cannot extend this XSD scheme and introduce new 组件, but can customize existing ones.

### General structure
In Magento 2 there are basic and secondary UI 组件.

Basic 组件 are:
* [Listing component]({{ page.baseurl }}/ui_comp_guide/components/ui-listing-grid.html)

* [表单components]({{ page.baseurl }}/ui_comp_guide/components/ui-form.html)

All other UI 组件 are secondary.

Basic components are declared in the [page layout files]({{ page.baseurl }}/frontend-dev-guide/layouts/layout-types.html#layout-types-page); secondary 组件 are declared in the top-level 组件’ instances configuration files.

All 组件 can be configured both for {% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}Admin{% endglossarytooltip %} and {% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}storefront{% endglossarytooltip %}.

<div class="bs-callout bs-callout-info" id="info">
  <p>You need to configure styles manually for 组件 on storefront.</p>
</div>

## When to use UI 组件?

With Magento, you may apply different approaches to implementing a UI element, and use:

* {% glossarytooltip ae0f1f68-c466-4189-88fd-6cd8b23c804f %}PHTML{% endglossarytooltip %} template with inline JavaScript

* PHTML template with declaration of related JavaScript file via {% glossarytooltip 8c0645c5-aa6b-4a52-8266-5659a8b9d079 %}XML{% endglossarytooltip %} {% glossarytooltip 73ab5daa-5857-4039-97df-11269b626134 %}布局{% endglossarytooltip %}

* {% glossarytooltip 5bfa8a8e-6f3e-4fed-a43e-62339916f02e %}jQuery{% endglossarytooltip %} {% glossarytooltip f0dcf847-ce21-4b88-8b45-83e1cbf08100 %}小工具{% endglossarytooltip %}

* Magento 2 {% glossarytooltip 9bcc648c-bd08-4feb-906d-1e24c4f2f422 %}UI component{% endglossarytooltip %}

We recommend using UI 组件 as much as possible and tend to do the same in Magento core.

UI components work well together: they communicate with each other via the [uiRegistry service]({{ page.baseurl }}/ui_comp_guide/troubleshoot/ui_comp_troubleshoot_js.html#debugging-using-the-uiregistry) that tracks their asynchronous initialization. Therefore, if we need to extend something that has already been implemented as a hierarchy of UI 组件 or add a new feature that should interact with other UI 组件, it's easier and more effective to use a UI component.

## What is a UI component?

UI component is a combination of:

1. **XML declaration** that specifies the component's configuration settings and inner structure.

2. **JavaScript** class inherited from one of the Magento JavaScript framework UI components base classes (such as [UIElement]({{ page.baseurl }}/ui_comp_guide/concepts/ui_comp_uielement_concept.html), [UIClass]({{ page.baseurl }}/ui_comp_guide/concepts/ui_comp_uiclass_concept.html) or [UICollection]({{ page.baseurl }}/ui_comp_guide/concepts/ui_comp_uicollection_concept.html)).


3. **Related template(s)**

### XML Declaration

XML is widely used in Magento 2, which allows developers to easily reuse existing functionalities and add customizations.

Comparing to XML layouts, UI сomponents use more semantical approach to declare and configure user interface.

An instance of UI component is usually based on the hierarchy of child UI 组件. 例如:

* the 表单组件 has Fieldsets, Tabs, and inner fields

* the Listing component has Filters, Columns, Bookmark component, and others

### JavaScript class

The picture below shows how the JavaScript class of a UI component is implemented.

![JavaScript class implementation of a UI component]({{ site.magentourl }}/common/images/ui_comp_js_class.png)

### Templates

A UI component can be bound to one or more {% glossarytooltip a2aff425-07dd-4bd6-9671-29b7edefa871 %}HTML{% endglossarytooltip %} templates using the KnockoutJS bindings.

## Configuring a UI component

A particular instance of a UI component is defined primarily by the following:

1. [definition.xml]({{ site.mage2100url }}app/code/Magento/Ui/view/base/ui_component/etc/definition.xml): default 组件' configuration. Can be extended in custom modules.
2. [UI component's XML declaration]({{ page.baseurl }}/ui_comp_guide/concepts/ui_comp_xmldeclaration_concept.html).
3. [Backend/PHP modifiers]({{ page.baseurl }}/ui_comp_guide/concepts/ui_comp_modifier_concept.html).
4. Configuration inside the JavaScript classes.

## Things to remember when working with UI 组件

**UI 组件 have different settings**

Configuration settings (their list and names) are different among UI 组件; these settings contain constants, optional and required settings. Developers need to treat every UI component separately.

**Beware of mistakes in XML config**

Surprisingly, most issues occur because of the typos and other mistakes in the UI component's XML configuration. Naming is critical because UI 组件 are heavily cross-referenced.
