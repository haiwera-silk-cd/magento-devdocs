---
group: arch-guide
title: Magento 1.x GDPR compliance
version: 2.1
github_link: architecture/gdpr/magento-1x.md
---

欧盟颁布[通用数据保护规则](https://www.eugdpr.org/) (GDPR)来给他们公民的个人数据更多控制，GDPR应用到在欧盟内运转的任何组织。它也应用到一些欧盟之外的为欧盟的的客户或企业提供产品或服务的组织。

我们发布这个遵守信息来帮助我们的店主和系统集成人员遵守GDPR，一个系统集成员可以使用数据流图和数据库信息来构建脚本以解决类似下面的情况：

* 客户询问店主要一份存储了他相关信息的数据的备份。
* 客户要求删除关于他的所有信息

参考[Magento官网](https://magento.com/gdpr)的描述来获取更多关于Magento如何帮助店主遵守GDPR的信息

## 数据流图

数据流图展示了这类数据，它们可以在网店前台或管理面板被客户和管理员接收和输入。

### 前台数据接口

用户注册后，用户可以在结算等类似的过程中为这个账号输入客户、地址及支付信息。

![前端数据接口](frontend-data-entry-points.svg)

### 前端数据访问接口

当客户登录并查看一些不同页面或结算的时修改，Magento会加载客户信息

![前端数据访问接口](frontend-data-access-points.svg)

### 后端数据访问接口

店主可以在使用管理面板时输入客户、地址及支付信息来创建客户或定单。

![后端数据接口](backend-data-entry-points.svg)

### 后端数据访问接口

在店主查看一些表格数据，点击查看详细信息及执行其它任务时Magento加载客户信息。

![后端数据访问接口](backend-data-access-points.svg)

## 数据库实体

Magento 1存储了客户的信息在客户、销售及其它数据库表中

### 客户的数据 {#customer-data}

Magento 1 存储客户信息在`customer_entity`表及`customer_address_entity`表，这两者都有一些可能包含客户属性的引用表。

#### `customer_entity`及引用表

`customer_entity`表的以下字段包含客户的信息：

字段 | 数据类型
--- | ---
`email` | varchar(255)

这些表引用`customer_entity`并且可能包含定制的客户属性：

表名 | 字段 | 数据类型
--- | --- | ---
`customer_entity_datetime` | `value` | datetime
`customer_entity_decimal` | `value` | decimal(12,4)
`customer_entity_int` | `value` | int(11)
`customer_entity_text` | `value` | text
`customer_entity_varchar` | `value` | varchar(255)

#### `customer_address_entity`及引用表

以下表引用了`customer_address_entity`且包含客户属性：

表名 | 字段 | 数据类型
--- | --- | ---
`customer_address_entity_datetime` | `value` | datetime
`customer_address_entity_decimal` | `value` | decimal(12,4)
`customer_address_entity_int` | `value` | int(11)
`customer_address_entity_text` | `value` | text
`customer_address_entity_varchar` | `value` | varchar(255)

### 订单数据

`sales_flat_order`表和关联表包含了客户的名字、账单及物流地址与相关信息

#### `sales_flat_order`表

`sales_order`表的以下字段包含客户的信息:

字段 | 数据类型
--- | ---
`customer_id` | int(10)
`customer_email` | varchar(128)
`customer_firstname` | varchar(128)
`customer_gender` | int(11)
`customer_lastname` | varchar(128)
`customer_middlename` | varchar(128)
`customer_prefix` | varchar(32)
`customer_suffix` | varchar(32)
`customer_taxvat` | varchar(32)
`remote_ip` | varchar(32)

#### `sales_flat_order_address`表

`sales_flat_order_address` 表包含客户地址

字段 | 数据类型
--- | ---
`customer_id` | int(10)
`fax` | varchar(255)
`region` | varchar(255)
`postcode` | varchar(255)
`lastname` | varchar(255)
`street` | varchar(255)
`city` | varchar(255)
`email` | varchar(255)
`telephone` | varchar(255)
`firstname` | varchar(255)
`prefix` | varchar(255)
`suffix` | varchar(255)
`middlename` | varchar(255)
`company` | varchar(255)
`vat_id`| text

#### `sales_flat_order_grid`表

`sales_flat_order_grid`表的以下字段包含客户的信息:

字段 | 数据类型
--- | ---
`customer_id` | int(10)
`shipping_name` | varchar(255)
`billing_name` | varchar(255)

#### `sales_flat_order_payment`表

`sales_flat_order_payment`表的以下字段包含客户的信息:

字段 | 数据类型
--- | ---
`cc_exp_month` | varchar(255)
`cc_ss_start_year` | varchar(255)
`echeck_bank_name` | varchar(128)
`echeck_type` | varchar(255)
`cc_ss_start_month` | varchar(255)
`cc_owner` | varchar(255)
`cc_exp_year` | varchar(255)
`echeck_routing_number` | varchar(255)
`echeck_account_name` | varchar(255)


### 报价数据

报价包含客户的名字，邮箱，地址及相关数据。

#### `sales_flat_quote`表

`sales_flat_quote`表的以下字段包含客户的信息:

字段 | 数据类型
--- | ---
`customer_id` | int(10)
`customer_tax_class_id` | int(10)
`customer_group_id` | int(10)
`customer_email` | varchar(255)
`customer_prefix` | varchar(40)
`customer_firstname` | varchar(255)
`customer_middlename` | varchar(40)
`customer_lastname` | varchar(255)
`customer_suffix` | varchar(40)
`customer_dob` | datetime
`customer_note` | varchar(255)
`remote_ip` | varchar(255)
`customer_gender` | varchar(255)

#### `sales_flat_quote_address`表

`sales_flat_quote_address`表的以下字段包含客户的信息:

字段 | 数据类型
--- | ---
`email` | varchar(255)
`prefix` | varchar(40)
`firstname` | varchar(255)
`middlename` | varchar(40)
`lastname` | varchar(255)
`suffix` | varchar(40)
`company` | varchar(255)
`street` | varchar(255)
`city` | varchar(255)
`region` | varchar(255)
`postcode` | varchar(255)
`fax` | varchar(255)

#### `sales_flat_quote_payment`表

`sales_flat_quote_payment`表包含信用卡信息及其它交易信息

字段 | 数据类型
--- | ---
`cc_last_4` | varchar(255)
`cc_owner` | varchar(255)
`cc_exp_month` | smallint(5)
`cc_exp_year` | smallint(5)
`cc_ss_owner` | varchar(255)
`cc_ss_start_month` | smallint(5)
`cc_ss_start_year` | smallint(5)

### 归档数据

以下表和字段包含了客户信息：

表名 | 字段 | 数据类型
--- | --- | ---
`enterprise_sales_creditmemo_grid_archive` | `billing_name` | varchar(255)
`enterprise_sales_invoice_grid_archive` | `billing_name` | varchar(255)
`enterprise_sales_order_grid_archive` | `billing_name` | varchar(255)
`enterprise_sales_order_grid_archive` | `customer_id` | int(10)
`enterprise_sales_order_grid_archive` | `shipping_name` | varchar(255)
`enterprise_sales_shipment_grid_archive` | `shipping_name` | varchar(255)

### 销售数据

以下表和字段包含了客户信息：

表名 | 字段 | 数据类型
--- | --- | ---
`sales_flat_creditmemo_grid` | `billing_name` | varchar(255)
`sales_flat_invoice_grid` | `billing_name` | varchar(255)

### RMA data

下面的RMA表及字段包含了客户信息：

表名 | 字段 | 数据类型
--- | --- | ---
`enterprise_rma` | `customer_custom_email` | varchar(255)
`enterprise_rma_grid` | `customer_id` | int(10)
`enterprise_rma_grid` | `customer_name` | varchar(255)

### 其它数据

以下表和字段包含了客户信息：

表名 | 字段 | 数据类型
--- | --- | ---
`core_email_queue_recipients` | `recipient_email` | varchar(128)
`core_email_queue_recipients` | `recipient_name` | varchar(255)
`customer_flowpassword` | `email` | varchar(255)
`customer_flowpassword` | `ip` | varchar(50)
`enterprise_giftregistry_person` | `email` | varchar(150)
`enterprise_giftregistry_person` | `firstname` | varchar(100)
`enterprise_giftregistry_person` | `lastname` | varchar(100)
`enterprise_giftregistry_person` | `middlename` | text
`enterprise_invitation` | `customer_id` | int(10)
`enterprise_invitation` | `email` | varchar(255)
`enterprise_invitation` | `referral_id` | int(10)
`enterprise_reminder_rule_coupon` | `customer_id` | int(10)
`enterprise_reminder_rule_coupon` | `emails_failed` | smallint(5)
`enterprise_scheduled_operations` | `email_receiver` | varchar(150)
`enterprise_scheduled_operations` | `email_sender` | varchar(150)
`gift_message` | `customer_id` | int(10)
`gift_message` | `recipient` | varchar(255)
`gift_message` | `sender` | varchar(255)
`newsletter_subscriber` | `customer_id` | int(10)
`newsletter_subscriber` | `subscriber_email` | varchar(150)
`persistent_session` | `customer_id` | int(10)
`persistent_session` | `info` | text
`poll_vote` | `customer_id` | int(10)
`poll_vote` | `ip_address` | varbinary(16)
`rating_option_vote` | `customer_id` | int(10)
`rating_option_vote` | `remote_ip` | varchar(50)
`rating_option_vote` | `remote_ip_long` | varbinary(516)
`send_friend_log` | `ip` | varbinary(16)

其它引用了客户的表

* `catalog_compare_item`
* `downloadable_link_purchased`
* `enterprise_customerbalance`
* `enterprise_customersegment_customer`
* `enterprise_giftregistry_entity`
* `enterprise_reminder_rule_log`
* `enterprise_reward`
* `log_customer`
* `log_visitor_online`
* `oauth_token`
* `product_alert_price`
* `product_alert_stock`
* `report_compared_product_index`
* `report_viewed_product_index`
* `review_detail`
* `sales_billing_agreement`
* `sales_flat_shipment`
* `sales_recurring_profile`
* `salesrule_coupon_usage`
* `salesrule_customer`
* `tag`
* `tag_relation`
* `wishlist`
