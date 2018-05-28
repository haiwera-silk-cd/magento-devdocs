---
group: compman
subgroup: 06_UseExtMan
title: Readiness check failure
menu_title: Readiness check failure
menu_node:
menu_order: 7
level3_menu_node: level3child
level3_subgroup: readiness
version: 2.2
github_link: comp-mgr/extens-man/extensman-readiness-fail.md
functional_areas:
  - Upgrade
---

## Readiness check failure {#compman-readiness-fail}
Messages similar to the following display if any readiness check fails. 

![You must resolve all readiness check failures before you continue]({{ site.magentourl }}/common/images/cman_readiness-fail-ex.png)

<div class="bs-callout bs-callout-info" id="info">
	<p>If you're updating multiple extensions, see <a href="{{ page.baseurl }}/comp-mgr/extens-man/extensman-readiness-multi.html#extensman-readiness-multi-fail">Readiness check with multiple 扩展更新s</a> instead.</p>
</div>

In the {% glossarytooltip c57aef7c-97b4-4b2b-a999-8001accef1fe %}event{% endglossarytooltip %} of failure, see one of the following sections:

*	<a href="{{ page.baseurl }}/comp-mgr/trouble/cman/updater.html">Updater check failure</a>
*	<a href="{{ page.baseurl }}/comp-mgr/trouble/cman/cron.html">Cron script check failure</a>
*	<a href="{{ page.baseurl }}/comp-mgr/trouble/cman/component-depend.html">Component dependency check failure</a>
*	<a href="{{ page.baseurl }}/comp-mgr/trouble/cman/php-version.html">PHP版本就绪检查的问题</a>
*	<a href="{{ page.baseurl }}/install-gde/trouble/php/tshoot_php-set.html">PHP配置错误</a>
*	<a href="{{ page.baseurl }}/install-gde/system-requirements.html">PHP extensions check failure</a>
