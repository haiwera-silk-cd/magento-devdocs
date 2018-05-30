---
group: reporting
title: Report XML
version: 2.2
github_link: advanced-reporting/report-xml.md
functional_areas:
    - Reports
---

**报表 XML** 是一种用于被创建用于构建高级报表的标记语言。
这种语言在XML中使用声明声明了SQL请求。

你可以使用一个报表名为集成高级报表接收数据。
报表名在`<report>`节点的`name`属性定义，描述如下.

## 报表列

报表XML不支持`*`号语名.
所有的列都必须被声明:

* 主表由`<source>`节点指定
* 要连(join)的表由`<link-source>`节点指定

添加`<attribute>`节点来指定须要的列.

## 语法和结构

所有的报表配置文件都存放在模块的`etc`目录下

```
<module_dir>/etc/reports.xml
```

下面是一个`reports.xml`的示例：
 
{% include_relative img/reports_xsd.svg %}

报表配置文件可以在依赖`Analytics`模块的任何模块(如:被创建用于收集**销售**相关数据的`SalesAnalytics`模块)中找到
每个报表配置文件声明一个`<report>`节点.

`report`节点将会被渲染成一条SQL请求.

### `<config>`

xml的配置

|属性|描述|常量|用法|
|--- |--- |--- |
|`xmlns:xsi`|默认命令空间声明.|`http://www.w3.org/2001/XMLSchema-instance`|必需|
|`xsi:noNamespaceSchemaLocation`|一个没有目标命名空间的XML结构的文档.|`urn:magento:module:Magento_Analytics:etc/reports.xsd`|必需|

### `<report>`

|属性|描述|使用|
|--- |--- |--- |
|`name`|报表配置的名称，你可以用它来合并，或作为一个引用。|必需|
|`connection`|数据库连接的名称,当Magento有多个数据库时。|可选|
|`iterator`|一个语名迭代器的完整的类名或接口名。要使用自定义的迭代器，可以添加一个包含了这个迭代器完整类名或接口名的`iterator`属性。这个迭代器可以在构造器中获取一个语句迭代器，并且可以使用自定义数据包裹或改变当前值|可选|

所有`reports.xml`文件中的有相同`name`属性的`<report>`节点都会被合并。

### `<source>`

数据源对应数据库中的表名。

|属性|描述|使用|
|--- |--- |--- |
|`name`|名称|必需|
|`alias`|表别名|可选|

主表由`<source>`标签指定.
渲染之后，这表示SQL语句中的`FROM`子句。

一个报表可以在`<source>`节点中使用`<filter>`来应用过滤.

### `<link-source>`

在`source`节点中，你也可以使用`<link-source>`标签来添加数据源.
渲染之后，它表示SQL语句中的`JOIN`子句。

`<link-source>`节点包含以下属性:

|属性|描述|使用|
|--- |--- |--- |
|`name`|名称|必需|
|`alias`|表别名|可选|
|`link-type`|连接类型|可选|

名称必须和数据库中的表名一样。
`alias`属性用途和SQL中的别名是相同的。
`link-type`属性指定SQL语句中的连接类型，可以是`INNER`或`LEFT`.

`<link-source>`节点的连接条件使用`<using>`标签描述.
渲染之后，它表示SQL中的`ON`子句。
`<using>`工作方式和过滤器相同，在本文下方描述.

### `<attribute>`

|属性|描述|使用
|--- |--- |---
|`name`|数据库中的列名|必需
|`alias`|列别名，和SQL中的列别名是相同作用|可选
|`function`|有效值有: `count`, `lower`, `date`, `sum`, `max`, `avg`, `min`, `sha1`|可选
|`group`|boolean|可选
|`distinct`|boolean|可选

### `<filter>`

报表可以使用在父节点里的`<filter>`来过滤数据。
此节点可以可以嵌套过滤器和`<conditions>`.
过滤器使用属性`glue`，帮助过滤基于多个条件查找的结果。

|属性|描述|值|使用|
|--- |--- |--- |
|`glue`|逻辑操作符|`or`, `and`|可选|

#### 示例

一个嵌套条件SQL的示例:

```sql
WHERE ((billing.entity_id IS NULL AND ((billing.entity_id < '200' AND billing.entity_id != '42') AND (billing.entity_id > '200' OR billing.entity_id != '201'))))
```

一个嵌套条件XML的示例:

```xml
<filter glue="and">
    <condition attribute="entity_id" operator="null" />
    <filter glue="and">
        <condition attribute="entity_id" operator="lt">200</condition>
        <condition attribute="entity_id" operator="neq">42</condition>
    </filter>
    <filter glue="or">
        <condition attribute="entity_id" operator="gt">200</condition>
        <condition attribute="entity_id" operator="neq">201</condition>
    </filter>
</filter>
```

### `<conditions>`

`<conditions>`节点包含以下属性:

|名称|描述|值|是否必需?|
|--- |--- |--- |
|`attribute`|数据库列名.|string|必需|
|`type`|要比较的类型|`value`表示一个标量(默认)<br/> `identifier`表示与另一列比较|可选|
|`operator`|比较操作符|必需|

比较操作符用于比较列和的值或在`<conditions>`节点中指定其它列

你可以在`\Magento\Analytics\ReportXml\DB\ConditionResolver::$conditionMap`中找到所有支持的操作符

<!-- LINK DEFINITIONS -->