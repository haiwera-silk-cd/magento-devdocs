---
group: install_trouble
subgroup: 10_php
title: 安装期间出现date警告
menu_title: 安装期间出现date警告
menu_node:
menu_order: 360
version: 2.1
github_link: install-gde/trouble/php/tshoot_php-date.md
redirect_from:
  - /guides/v1.0/install-gde/trouble/tshoot_php-date.html
  - /guides/v2.0/install-gde/trouble/tshoot_php-date.html
functional_areas:
  - Install
  - System
  - Setup
---

### Details

During the installation, the following message displays: 

	PHP Warning:  date(): It is not safe to rely on the system's timezone settings. [more]

### Solution

Set the [PHP timezone]({{ page.baseurl }}/install-gde/prereq/php-settings.html) properly.

