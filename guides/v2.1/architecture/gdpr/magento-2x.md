---
group: arch-guide
title: Magento 2.x GDPR compliance
version: 2.1
github_link: architecture/gdpr/magento-2x.md
---

欧盟颁布[通用数据保护规则](https://www.eugdpr.org/) (GDPR)来给他们公民的个人数据更多控制，GDPR应用到在欧盟内运转的任何组织。它也应用到一些欧盟之外的为欧盟的的客户或企业提供产品或服务的组织。

我们发布GDPR遵守信息来帮助我们的店主和系统集成人员遵守GDPR. 系统集成员可以使用数据流图和数据库信息来构建脚本以解决类似下面的问题：

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

店主可以使用管理面板输入客户信息，地址及支付信息来创建一个客户或订单。

![后端数据接口](backend-data-entry-points.svg)

### 后端数据访问接口

在店主查看一些表格数据，点击查看详细信息及执行其它任务时Magento加载客户信息。

![后端数据访问接口](backend-data-access-points.svg)

## 数据库实体

Magento2 主要存储客户相关的信息到客户、地址、订单、报价及支付表，其它的表包含引用到客户的ID。。

### 客户的数据 {#customer-data}

Magento2存储以下客户属性：

* 出生日期
* 邮箱
* 姓氏
* 性别
* 名字
* 中间名/首字母
* 名字前缀
* 名字后缀

#### `customer_entity`及引用表

`customer_entity`表的以下字段包含客户的信息：

字段 | 数据类型
--- | ---
`email` | varchar(255)
`prefix` | varchar(40)
`firstname` | varchar(255)
`middlename` | varchar(255)
`lastname` | varchar(255)
`suffix` | varchar(40)
`dob` | date
`gender` | smallint(5)

这些表引用`customer_entity`并且可能包含定制的客户属性：

表名 | 字段 | 数据类型
--- | --- | ---
`customer_entity_datetime` | `value` | datetime
`customer_entity_decimal` | `value` | decimal(12,4)
`customer_entity_int` | `value` | int(11)
`customer_entity_text` | `value` | text
`customer_entity_varchar` | `value` | varchar(255)

#### `customer_grid_flat`表

`customer_grid_flat`表的以下字段包含客户的信息：

字段 | 数据类型
--- | ---
`name` |text
`email` | varchar(255)
`dob` | date
`gender` | int(11)
`shipping_full` | text
`billing_full` | text
`billing_firstname` | varchar(255)
`billing_lastname` | varchar(255)
`billing_telephone` | varchar(255)
`billing_postcode` | varchar(255)
`billing_country_id` | varchar(255)
`billing_region` | varchar(255)
`billing_city` | varchar(255)
`billing_fax` | varchar(255)
`billing_vat_id` | varchar(255)
`billing_company` | varchar(255)


### Address data

Magento2存储以下客户属性：

* City
* Company
* Country
* Fax
* 姓氏
* 名字
* 中间名/首字母
* 名字前缀
* 名字后缀
* Phone Number
* State/Province
* State/Province ID
* Street Address
* VAT Number
* Zip/Postal Code

#### `customer_address_entity`及引用表

`customer_address_entity`表的以下字段包含客户的信息：

字段 | 数据类型
--- | ---
`city` | varchar(255)
`company` | varchar(255)
`country_id` | varchar(255)
`fax` | varchar(255)
`firstname` | varchar(255)
`lastname` | varchar(255)
`middlename` | varchar(255)
`postcode` | varchar(255)
`region` | varchar(255)
`region_id` | int(10)
`street` | text
`suffix` | varchar(40)
`telephone` | varchar(255)
`vat_id` | varchar(255)

这些表引用`customer_address_entity`并且可能包含定制的客户属性：

表名 | 字段 | 数据类型
--- | --- | ---
`customer_address_entity_datetime` | `value` | datetime
`customer_address_entity_decimal` | `value` | decimal(12,4)
`customer_address_entity_int` | `value` | int(11)
`customer_address_entity_text` | `value` | text
`customer_address_entity_varchar` | `value` | varchar(255)

### 订单数据

`sales_order`表和相关的表包含客户的名字，账单及物流地址与相关数据。

#### `sales_order`表

`sales_order`表的以下字段包含客户的信息:

字段 | 数据类型
--- | ---
`customer_dob` | datetime
`customer_email` | varchar(128)
`customer_firstname` | varchar(128)
`customer_gender` | int(11)
`customer_group_id` | int(11)
`customer_id` | int(10)
`customer_lastname` | varchar(128)
`customer_middlename` | varchar(128)
`customer_prefix` | varchar(32)
`customer_suffix` | varchar(32)
`customer_taxvat` | varchar(32)
`quote_address_id` | int(11)
`remote_ip` | varchar(32)
`x_forwarded_for` | varchar(32)

#### `sales_order_address`表

The `sales_order_address` table contains the customer's address.

字段 | 数据类型
--- | ---
`customer_address_id` | int(11)
`quote_address_id` | int(11)
`region_id` | int(11)
`customer_id` | int(11)
`fax` | varchar(255)
`region` | varchar(255)
`postcode` | varchar(255)
`lastname` | varchar(255)
`street` | varchar(255)
`city` | varchar(255)
`email` | varchar(255)
`telephone` | varchar(255)
`country_id` | varchar(2)
`firstname` | varchar(255)
`suffix` | varchar(255)
`company` | varchar(255)

#### `sales_order_grid`表

`sales_order_grid`表的以下字段包含客户的信息:

字段 | 数据类型
--- | ---
`customer_id` | int(10)
`shipping_name` | varchar(255)
`billing_name` | varchar(255)
`billing_address` | varchar(255)
`shipping_address` | varchar(255)
`shipping_information` | varchar(255)
`customer_email` | varchar(255)
`customer_name` | varchar(255)

### 报价数据

报价包含客户的名字，邮箱，地址及相关数据。

#### `quote`表

`quote`表的以下字段包含客户的信息:

字段 | 数据类型
--- | ---
`customer_id` | int(10)
`customer_email` | varchar(255)
`customer_prefix` | varchar(40)
`customer_firstname` | varchar(255)
`customer_middlename` | varchar(40)
`customer_lastname` | varchar(255)
`customer_dob` | datetime
`remote_ip` | varchar(32)
`customer_taxvat` | varchar(255)
`customer_gender` | varchar(255)

#### `quote_address`表

`quote_address`表的以下字段包含客户的信息:

字段 | 数据类型
--- | ---
`customer_id` | int(10)
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
`region_id` | int(10)
`postcode` | varchar(20)
`country_id` | varchar(30)
`telephone` | varchar(255)
`fax` | varchar(255)

### 支付数据

`sales_order_payment`表包含信用卡信息及其它的交易信息。

字段 | 数据类型
--- | ---
`cc_exp_month` | varchar(12)
`echeck_bank_name` | varchar(128)
`cc_last_4` | varchar(100)
`cc_owner` | varchar(128)
`po_number` | varchar(32)
`cc_exp_year` | varchar(4)
`echeck_routing_number` | varchar(32)
`cc_debug_response_body` | varchar(32)
`echeck_account_name` | varchar(32)
`cc_number_enc` | varchar(128)
`additional_information` | text

### 发票数据

Magento可以被配置成客户可以发送发票到私人销售和事件

#### `magento_invitation`表

`magento_invitation`表包含客户ID,邮箱，及referral ID

字段 | 数据类型
--- | ---
`customer_id` | int(10)
`email` | varchar(255)
`referral_id` | int(10)

#### `magento_invitation_track`表

`magento_invitation_track`表也包含客户信息。

字段 | 数据类型
--- | ---
`inviter_id` | int(10)
`referral_id` | int(10)

### 其它引用客户信息的表

下面的表都包含`customer_id`字段：

* `catalog_compare_item`
* `catalog_product_frontend_action`
* `downloadable_link_purchased`
* `magento_customerbalance`
* `magento_customersegment_customer`
* `magento_reward`
* `magento_rma`
* `oauth_token`
* `paypal_billing_agreement`
* `persistent_session`
* `product_alert_price`
* `product_stock_alert`
* `report_compared_product_index`
* `report_viewed_product_index`
* `review_detail`
* `salesrule_coupon_usage`
* `salesrule_customer`
* `wishlist`
