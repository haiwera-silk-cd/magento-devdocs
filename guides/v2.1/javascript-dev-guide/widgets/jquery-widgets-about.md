---
group: jsdg
subgroup: 3_Widgets
title: Magento jq小工具
menu_order: 1
menu_node: parent
version: 2.1
github_link: javascript-dev-guide/widgets/jquery-widgets-about.md
redirect_from:
  - guides/v2.0/frontend-dev-guide/javascript/jquery-widgets-about.html
  - guides/v1.0/frontend-dev-guide/javascript/jquery-widgets-about.html
---

The Magento system uses a {% glossarytooltip 5bfa8a8e-6f3e-4fed-a43e-62339916f02e %}jQuery{% endglossarytooltip %} {% glossarytooltip 312b4baf-15f7-4968-944e-c814d53de218 %}JavaScript{% endglossarytooltip %} {% glossarytooltip 08968dbb-2eeb-45c7-ae95-ffca228a7575 %}库{% endglossarytooltip %} to implement client functionality. This includes a wide usage of standard, customized, and custom jQuery widgets.

This guide discusses the following widgets:
<ul>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_accordion.html" target="_blank">手风琴菜单小工具</a> </li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_alert.html" target="_blank">提示弹框小工具</a> </li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_calendar.html" target="_blank">日历小工具</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_collapsible.html" target="_blank">可折叠窗小工具</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_confirm.html" target="_blank">Confirm widget</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_dialog.html" target="_blank">下拉弹窗小工具</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_gallery.html" target="_blank">相册小工具</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_list.html" target="_blank">列表小工具</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_loader.html" target="_blank">加载小工具</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_menu.html" target="_blank">菜单小工具</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_modal.html" target="_blank">模态弹窗小工具</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_navigation.html" target="_blank">导航栏小工具</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_prompt.html" target="_blank">问询弹框小工具</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_quickSearch.html" target="_blank">快速搜索小工具</a></li>
<li><a href="{{ page.baseurl }}/javascript-dev-guide/widgets/widget_tabs.html" target="_blank">标签页小工具</a></li>

</ul>


<div class="bs-callout bs-callout-info" id="info">
  <p>Magento 2 supports <a href="http://blog.jqueryui.com/2012/11/jquery-ui-1-9-2/" target="_blank">jQuery UI 1.9.2</a>, {% glossarytooltip f0dcf847-ce21-4b88-8b45-83e1cbf08100 %}小工具{% endglossarytooltip %} options added in later versions might be unavailable.</p>
</div>

<div class="bs-callout bs-callout-info" id="info">
  <p>Magento out of the box does not contain jQuery UI styles. Also, it is not recommended to download them as is, because it can break the default Magento design. To use certain jQuery UI styles, you need to add them manually in your custom stylesheets in the <code>{your_theme_dir}/web/css</code>或<code>{your_module_dir}/view/{area}/web/css</code> directory.</p>
</div>
