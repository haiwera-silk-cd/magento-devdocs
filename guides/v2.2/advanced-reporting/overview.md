---
group: reporting
title: 高级报表
version: 2.2
github_link: advanced-reporting/overview.md
functional_areas:
    - Reports
---

[高级报表功能]{:target="_blank"}是通过集成提供，由Magento集成[Magento商业智能]{:target="_blank"} (MBI).
Magento收集数据并发送这些信息到MBI用于分析
 
**Magento Admin > Dashboard > "Go to 高级报表"** 使用相应的身份在`https://advancedreporting.rjmetrics.com/report`打开报表
 
## 先决条件

1. 站点必须运行在一个能上公网的服务器上
2. 域名必须拥有有效的(SSL)证书
3. Magento必须已经安装或更新成功，没有出现错误。
4. 在Magento配置中, 网店的[基础URL(安全)设置][base url]{:target="_blank"}必须指向安全的URL. 例如: https://yourdomain.com.
5. 在Magento配置中, **在网店前台使用安全的URL**, **和在管理面板使用安全的URL** 必须[设置成 **是** ]{:target="_blank"}.
6. 确保[Magento定时任务]{:target="_blank"}已经创建并且定时任务已经在你安装的服务器上运行。


<div class="bs-callout bs-callout-info" markdown="1">
在订阅成功后Magento和MBI的第一次同步可能要花一整天的时间才能完成
</div>

## 强烈建议

为了避免在重要的时刻过载，你可以设置一个你想要的时间来收集数据

**Magento Admin > Stores > Settings > Configuration > General > 高级报表**

## 可扩展性

虽然分析(Analytics)模块提供的API,可以指定用于与MBI互换数据，但在这个版本我们不推荐扩展高级报表的功能。


## 相关主题

[Magento模块功能实现][modules]{:target="_blank"}

[数据收集配置和设置][collection]{:target="_blank"}


<!-- LINK DEFINITIONS -->

[modules]: modules.html
[collection]: data-collection.html

[高级报表功能]: http://docs.magento.com/m2/ce/user_guide/reports/advanced-reporting.html
[base url]: http://docs.magento.com/m2/ce/user_guide/stores/store-urls.html
[Magento商业智能]: https://magento.com/products/business-intelligence
[Magento定时任务]: http://devdocs.magento.com/guides/v2.2/config-guide/cli/config-cli-subcommands-cron.html
[设置成 **是** ]: http://docs.magento.com/m2/ce/user_guide/Resources/Images/config-general-web-base-urls-secure.png