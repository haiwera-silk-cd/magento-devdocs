---
group: reporting
title: 高级报表数据集
version: 2.2
github_link: advanced-reporting/data-collection.md
functional_areas:
    - Reports
---

Magento收集Magento商业智能(MBI)服务用于构建高级报表的数据。
所有这些数据存储在一个可以安全传输到MBI的加密的归档文件中
数据收集器声明在`etc/analytics.xml`配置文件中。 它声明了:

- 哪些报表文件必须被包含到这个归档中
- 哪些提供器类必须为每个报表文件提供数据
- 哪些报表数据配置必须被应用到收集到的数据

<div class="bs-callout bs-callout-warning" markdown="1" >
这篇文章旨在提供更好的解释，关于数据收集器是如何工作。
配置文件的作何改变都会导致问题，因为MBI服务不希望在当前的版本中，配置文件有任何更改。
</div>

## 例如

这是一个`etc/analytics.xml`的示例文件

```xml
<?xml version="1.0"?>

<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_Analytics:etc/analytics.xsd">
    <file name="modules">
        <providers>
            <reportProvider name="modules" class="Magento\Analytics\ReportXml\ReportProvider">
                <parameters>
                    <name>modules</name>
                </parameters>
            </reportProvider>
        </providers>
    </file>
    <file name="store_config">
        <providers>
            <customProvider name="store_config" class="Magento\Analytics\Model\StoreConfigurationProvider"/>
        </providers>
    </file>
    <file name="stores">
        <providers>
            <reportProvider name="stores" class="Magento\Analytics\ReportXml\ReportProvider">
                <parameters>
                    <name>stores</name>
                </parameters>
            </reportProvider>
            <customProvider name="store_config" class="Magento\Analytics\Model\StoreConfigurationProvider"/>
        </providers>
    </file>
</config>
```

上面的示例配置声明了以下内容:

*   `modules.csv`, `store_config.csv`, `stores.csv`报表文件必须被包含在准备给MBI服务的归档文件中
*   `modules.csv`必须包含数据提供器`\Magento\Analytics\ReportXml\ReportProvider`类提供的数据.
 提供的数据必根据在`modules`报表申明的在`etc/reports.xml`文件中定义的进行配置.
*   `store_config.csv`必须包含数据提供器`Magento\Analytics\Model\StoreConfigurationProvider`类提供的数据.
*   `stores.csv`必须包含数据提供器`\Magento\Analytics\ReportXml\ReportProvider` 类提供的数据.
 提供的数据根据在`store_config`报表中声明在`etc/reports.xml`文件中定义的进行配置.
 同样, 报表文件必须包含数据提供器`Magento\Analytics\Model\StoreConfigurationProvider` 类提供的数据.

## 可扩展性

数据集的配置可以在任何模块被修改或扩展，添加对应的`<module_name>/etc/analytics.xml`文件并且必须修改或添加其节点。

## 结构

`etc/analytics.xsd`文件声明了`etc/analytics.xml`文件要遵遁的结构.

{% include_relative img/analytics_xsd.svg %}

### `<config>`

xml的配置

|属性|描述|常量|用法|
|---|---|---|---|
|`xmlns:xsi`|默认命令空间声明|`"http://www.w3.org/2001/XMLSchema-instance"`|必需|
|`xsi:noNamespaceSchemaLocation`|一个没有目标命名空间的XML结构的文档|`"urn:magento:module:Magento_Analytics:etc/reports.xsd"`|必需|

### `<file>`

收集了数据并将被归档到归档文件的报表文件(默认是`.csv`)
T`\Magento\Analytics\Model\ReportWriter` 类将决定响应的数据和文件类型，可以是 (`.csv`, `.json`, 等.).

|属性|描述|示例值|用法|
|---|---|---|---|
|`name`|文件名，不包含扩展名|`"modules"`|必需|
|`prefix`|保留|--|--|

```xml
<config ...>

    <!-- Adds a report file `module.csv` to the archive file -->
    <file name="modules"> 
        ...
    </file>
    
    <!-- Adds a report file `stores.csv` to the archive file -->
    <file name="stores">
        ...
    </file>
    
</config>
```

### `<providers>`

节点必须包含`<reportProvider>`或`<customProvider>`，或两者都包含。

```xml
...
    <file ...>    
        <!-- A report provider adds data to the report file  -->
        <providers>
            <reportProvider ...>   
        </providers>
    </file>
    
    <file ...>
        <!-- A custom provider adds data to the report file  -->
        <providers>
            <customProvider ...>        
        </providers>
    </file>
    
    <file ...>
        <providers>
            <!-- A report provider and a custom provider add data to the report file  -->
            <reportProvider ...>
            <customProvider ...>        
        </providers>
    </file>
...
```

### `<reportProvider>`

一个为报表文件提供数据的类.
可以包含参数。

|属性|描述|示例值|用法|
|---|---|---|---|
|`name`|数据提供器的名字|`modules`|必需|
|`class`|完整的数据提供器的类名|`"Magento\Analytics\ReportXml\ReportProvider"`|必需|

当前仅支持一种有效的数据提供器`Magento\Analytics\ReportXml\ReportProvider`.

```xml
...
    <providers>
        <!-- A report provider `stores` uses the `Magento\Analytics\ReportXml\ReportProvider` class to collect report data -->
        <reportProvider name="stores" class="Magento\Analytics\ReportXml\ReportProvider">
            ...
        </reportProvider>
    </providers>
...
```

### `<parameters>`

用于`<reportProvider>`的参数。
当前只有一个可用参数`<name>`

```xml
...
    <reportProvider name="stores" class="Magento\Analytics\ReportXml\ReportProvider">
        <!-- The report provider `stores` uses a configuration of a report with name `store_report` declared in `etc/reports.xml` -->
        <parameters>
            <name>store_report</name>
        </parameters>
    </reportProvider>            
...
```

如果提供器是`reportProvider class="Magento\Analytics\ReportXml\ReportProvider"`，那么可以直接在`reports.xml`使用`<report name />`

### `<customProvider>`

一个为报表文件提供数据的类.
可以包含任何参数

|属性|描述|示例值|用法|
|---|---|---|---|
|`name`|数据提供器的名字|"store_config"|必需|
|`class`|完整的数据提供器的类名|`"Magento\Analytics\Model\StoreConfigurationProvider"`|必需|

```xml
...
    <providers>
        <!-- A report provider `store_config` uses the `Magento\Analytics\Model\StoreConfigurationProvider` class to collect report data -->
        <customProvider name="store_config" class="Magento\Analytics\Model\StoreConfigurationProvider"/>
    </providers>
...
```

## 相关主题

[各模块提供的高级报表][modules]


<!-- LINK DEFINITIONS -->

[modules]: data-collection.html

<!-- ABBREVIATIONS -->
*[MBI]: Magento商业分析