---
group: arch-guide
subgroup: 架构基础
title: 网店前台自定义策略
menu_title: 网店前台自定义策略
menu_order:
version: 2.1
github_link: architecture/storefront_customization.md
---

## 概述

我们可以对Magento支持的{% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网站前台{% endglossarytooltip %}定制的范围进行概括。这个范围跨越最简单的定制，仅涉及一个小添加到Magento设置，到完全替换Magento提供的{% glossarytooltip a2aff425-07dd-4bd6-9671-29b7edefa871 %}HTML{% endglossarytooltip %}和{% glossarytooltip 6c5cb4e9-9197-46f2-ba79-6147d9bfe66d %}CSS{% endglossarytooltip %}.

## 网店前台定制级别

以下依复杂性排序列出了四个级别的潜在的前端定制

### 扩展Magento提供的CSS
Magento提供一套默认的{% glossarytooltip d2093e4a-2b71-48a3-99b7-b32af7158019 %}主题{% endglossarytooltip %}和基于LESS的CSS。你可以仅使用CSS基本上改变网店前台.这种不复杂的策略应该适合有限的项目预算，或应该引起为站点创建不同外观的开发者石感兴趣。小的业务可以走这个前端定制的过程，在Magento市场买一个第三方开发的主题来扩展默认的外观。

### 替换PHTML模板文件
除了扩展默认的CSS，你还可以生成不同的HTML{% glossarytooltip 8f407f13-4350-449b-9dc5-217dcf01bc42 %}标签{% endglossarytooltip %}.比如，你可能要添加一个缺失的CSS类名，或添加一个额外的`<div>`标签来达到一种可视的效果。你也可能须要稍稍调整一些{% glossarytooltip 312b4baf-15f7-4968-944e-c814d53de218 %}JavaScript{% endglossarytooltip %}来处理不同的HTML标签。这种修改比只简单扩展Magento CSS要求更高，但仍是小项目和初级团队力所能及的。

### 替换Magento提供的CSS
相较于编辑Magento提供的默认的CSS，你可能决定要去替换所有的默认的前端CSS代码。这种策略避免把自己的项目和Magento提供的CSS捆到一起，但却使项目开发和集成面临更大的负担。它也允许使用Magento没有提供的不同的CSS工具和技术。构建他们自己CSS库的合作者可以在不同的额户项目中重用这些库。（这些单独的CSS库可以帮助区分合作者和市场上的其它人）

除了替换CSS文件，你可以须要替换少量HTML和Javascript.

### 替换Magento提供的CSS, HTML, 和JavaScript
交付一个与默认Magento完全不同的购物体验是一个更大的任务。然而，在未来集成附加的扩展到你的安装中，权衡是更加复杂的体验，

<div class="bs-callout bs-callout-info" id="info">
  <p>如果你一直遵循最佳实践把代码按类区分任何网店前台的定制将最佳的工作且将为后面的升级提供最简单的途径。例如，保持所有HTML在{% glossarytooltip ae0f1f68-c466-4189-88fd-6cd8b23c804f %}PHTML{% endglossarytooltip %}文件中，所有的Javascript在Javascript文件上中。</p>
</div>

### 相关主题s

<a href="{{ page.baseurl }}/frontend-dev-guide/bk-frontend-dev-guide.html" target="_blank">前端工程师手册</a>

<a href="{{ page.baseurl }}/javascript-dev-guide/bk-javascript-dev-guide.html" target="_blank">js开发者手册</a>
