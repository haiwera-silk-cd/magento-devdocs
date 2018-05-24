---
group: extension-dev-guide
subgroup: 99_Module Development
title: 迁移消息队列配置
menu_title: 迁移消息队列配置
menu_order: 19
ee_only: True
level3_menu_node: level3child
level3_subgroup: mq
version: 2.1
github_link: extension-dev-guide/message-queues/queue-migration.md
redirect_from: /guides/v2.1/config-guide/mq/queue-migration.html
functional_areas:
  - Configuration
  - System
  - Setup
---

### Migrate from Magento 2.0 to 2.1 ###

The `communication.xml` file was not changed between Magento 2.0 and 2.1. Replace the `queue.xml` file for each {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %} that sends messages to the message queue.

#### Replace the `queue.xml` file ####

The structure of the `queue.xml` file is substantially different in Magento. 2.1. Make a copy of your 2.0 `queue.xml` file and create a new one with the structure listed below.

| 2.1 Attribute  | 2.0 Equivalent |
| ---------------- | ----------- |
`<broker>/topic` | `<bind>/topic`
`<broker>/type` | `<consumer>/connection`
`<broker>/exchange` | `<bind>/exchange`
`<broker>/<queue>/name` | `<consumer>/queue`
`<broker>/<queue>/consumer` | `<consumer>/name`
`<broker>/<queue>/consumerInstance` | `<consumer>/executor`
`<broker>/<queue>/handler` | Use the values from `<consumer>/class` and `<consumer>/method` in the format `<Vendor>\Module\<ServiceName>::<methodName>`.
`<broker>/<queue>/maxMessages` | `<consumer>/max_messages`

#### 相关主题
*	<a href="{{ page.baseurl }}/config-guide/mq/rabbitmq-overview.html">消息队列概述</a>
*	<a href="{{ page.baseurl }}/extension-dev-guide/message-queues/config-mq.html">配置消息队列</a>
