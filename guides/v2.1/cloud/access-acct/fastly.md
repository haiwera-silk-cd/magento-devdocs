---
group: cloud
subgroup: 090_configure
title: 快速设置
menu_title: 快速设置
menu_order: 5
menu_node:
version: 2.1
github_link: cloud/access-acct/fastly.md
functional_areas:
  - Cloud
  - Setup
  - Configuration
---

[Fastly]({{ page.baseurl }}/cloud/basic-information/cloud-fastly.html)需要是{{site.data.var.ece}}，并且是适用于准生产环境和生产环境。它以Varnish来提升缓存性能，及以{% glossarytooltip f83f1fa7-7a64-467b-b629-c2d0c25d2e7f %}内容分发网络{% endglossarytooltip %}(CDN)提供静态资源加速，Fastly不能在集成环境中运行。

这些信息帮助你开始安装和配置Fastly。我们为后台和Origin shields(一种安全产品)提供附加的信息和错误/维护页面及VCL代码片段

对于VCL代码片段，高级的配置经历写代码的开发是必要的

配置Fastly的过程包括:

* 在集成中安装Fastly模块
* 在准测试环境和生产环境布署代码
* Fastly配置证书和设置
* 高级配置，包含VCL代码块

## 多Fastly账号和分配的域名{#domain}
在启动 {{site.data.var.ece}}之前，你可能已经有一个Fastly账号或试用帐号，并且把你的顶级或子域名分配给了它。作为建议，你将须要从现存的Fastly账号上移除所有你计划使用在 {{site.data.var.ece}}上的顶级和子域名

Fastly仅允许一个顶级域名和所有子域名分配到一个简单的Fastly服务及账号上，例如，如果你有一个顶级域名mystore.com及其子域名shoes.mystore.com和socks.mystore.com，它们被一个现存的Fastly账号管理，在上线Fastly和{{site.data.var.ece}}之前，你须要从帐号中将它们移除

更多细节，请参考你的Fastly帐号和[文档](https://docs.fastly.com/)来移除这些域名，文档中也包含移除移除及更新CNAME记录等说明。

## 获取你的Fastly证书 {#cloud-fastly-creds}
要获取Fastly证书，打开一个[support ticket]({{ page.baseurl }}/cloud/trouble/trouble.html)。你必须提供你的完全合格的域名。

我们将为你的准生产环境和生产环境提供给你下面的认证信息

*	Fastly服务ID
*	Fastly API访问令牌

你也可以在准生产环境和生产环境的`/mnt/shared/fastly_tokens.txt`文件中找到这些认证信息。你可以通过SSH连接到服务器来验证是否在此路径。如果你没有找到这个文件，请提交一个工单来获取[支持]({{ page.baseurl }}/cloud/trouble/trouble.html)，要求添加这个文件，我们会帮助提供认证文件。

<div class="bs-callout bs-callout-warning" markdown="1">
记下在哪个环境使用了哪些认证信息。如果你在一个环境使用了错误的认证信息，Fastly会遇到问题
</div>

## 起步 {#cloud-fastly-start}
你须要安装Fastly在它自己的分支，微调Fastly是一个复杂的过程，依赖于你的需求和网店大小。如果你已经有一个工作的分支或知道如何创建分支，可以跳转到[安装Fastly](#cloud-fastly-setup).

创建分支:

{% include cloud/cli-get-started.md %}

## 安装Fastly到一个集成分支并部署 {#cloud-fastly-setup}
你应该在你本地安装Fastly模块，推送代码来集成和部署到准生产环境和生产环境。对于{{site.data.var.ece}} 2.2，安装Fastly模块的1.2.33或更新，来为所有更新的配置及完整的VCL代码片段上传支持。

<div class="bs-callout bs-callout-warning" markdown="1">
不要在构建和部署之前在本地配置此模块，你将在它们各自的环境中配置模块。

我们建议使用`bin/magento magento-cloud:scd-dump`命令来进行配置管理([2.1.X](https://devdocs.magento.com/guides/v2.1/cloud/live/sens-data-over.html#cloud-config-specific-recomm), [2.2.X](https://devdocs.magento.com/guides/v2.2/cloud/live/sens-data-over.html#cloud-config-specific-recomm))。如果你在准生产和生产环境中使用 `app:config:dump`命令，所有的Fastly的配置项会被锁定，不允许编辑。
</div>


我们仅为你的准生产和生产环境提供Fastly服务。你不能在集成环境中使用Fastly服务。

1.	在你本地环境根目录，使用终端按以下顺序输入下面的命：

		composer config repositories.fastly-magento2 git "https://github.com/fastly/fastly-magento2.git"
		composer require fastly/magento2

2.	等待依赖更新
3.	输入下面的命令完整更新并清除缓存

		php bin/magento setup:upgrade && php bin/magento cache:clean
4. 编辑你的composer.json文件并确保Fasty模块引入正确的版本。.

	* 在"require"节点中，要包含`"fastly/magento2": <version number>`
	* 在"repositories"节点中，要包含:

		"fastly-magento2": {
					"url": "https://github.com/fastly/fastly-magento2.git"
		}
3.	使用下面的命令添加，提交及推送修改到你的代码仓库：

		git add -A; git commit -m "Install Fastly"; git push origin <branch name>

4. 与`master`集成分支合并分支代码。
5. [部署]({{ page.baseurl }}/cloud/live/stage-prod-live.html)代码到准生产和生产环境

部署后，你可以在准生产和生产环境上登录到管理员面板来配置Fastly的认证和设置。这给了你在不同环境按需配置不同缓存特征的灵活性，包括VCL代码片段。

## 使用Magenot管理面板启用和配置Fastly {#cloud-fastly-config}
要开始配置Fastly,你须要在准生产和生产环境中输入和测试Fastly的认证信息。认证信息测试成功之后，你才可以继续高级配置和[VCL snippets](#custom-vcl)

我们为你的准生产和生产环境提供你的Fastly服务ID和API访问密钥(或令牌)。这些认证信息每个环境是不同的。请确保你使用的是正确的认证信息。

在准生产和生产环境完成以下配置步骤：

1.	以管理员身份登录你的Magento管理面板。
2.	点击 **Stores** > **Settings** > **Configuration** > **Advanced** > **System**.
3.	在右侧栏，展开**Full Page Cache**.

	![Expand to select Fastly]({{ site.magentourl }}/common/images/cloud_fastly_menu.png){:width="650px"}
4.	For **Caching Application**, uncheck the **Use system value** check box and select **Fastly CDN** from the drop-down list.

	![Choose Fastly]({{ site.magentourl }}/common/images/cloud-fastly_enable-admin.png){:width="550px"}
5.	展开**Fastly Configuration**。然后你可以[选择缓存选项](https://github.com/fastly/fastly-magento2/blob/master/Documentation/CONFIGURATION.md#configure-the-module){:target="\_blank"}.
6.	完成后，点击页面顶部的**Save Config**
7.	根据提示通知清除缓存。之后，导航回到**Stores** > **Configuration** > **Advanced** > **System** > **Fastly Configuration**续继你的配置。

配置下面的特征并启用附加的[配置选项](https://github.com/fastly/fastly-magento2/blob/master/Documentation/CONFIGURATION.md#further-configuration-options){:target="\_blank"}:

* [上传Fastly VCL代码片段](#upload-vcl-snippets)
* [配置后台及Origin shielding](#backend)
* [创建自定义错误/维护页](#fastly-errpg)

<div class="bs-callout bs-callout-info" id="info" markdown="1">
*	忽略创建免费Fastly账号的链接。我们会提供你的Fastly认证信息(服务ID和API访问令牌)
*	Fastly 1.2.0或更新(我们推荐使用1.2.33或更新),使用**Upload VCL to Fastly**按钮更新你默认的[VCL代码片段](#custom-vcl).
</div>

## 上传Fastly VCL代码片段 {#upload-vcl-snippets}
你不一定要创建或编写VCL代码片段，我们会为Fastly提供一个默认的代码片段。你只须要点击**Upload VCL to Fastly**完成这一步即可。

安装的Fastly模块包含以下默认的驱动和Fastly集成的[VCL snippets](https://github.com/fastly/fastly-magento2/tree/master/etc/vcl_snippets){:target="\blank"}，这些VCL代码片段在你上传之前是无效的。当你点击上传，你就为你的特定的服务ID和扩展推送了这些VCL代码片段到你的Fastly。

对于VCL代码片段的开发者，这些默认的代码片段是事先准备好的，名字是`magentomodule_`，优先级是50。你不应该使用这个预选准备好的名字给你自己的代码片段。完整的细节，参考我们的手册来创建和添加[自定义VCL代码片段](#custom-vcl).

要使用代码片段，你必须使用Magento管理员上传Fastly VCL，像下面这样：

1.	点击**Fastly Configuration**节点，如下图所示点击**Upload VCL to Fastly**。 

	![上传一个Magento VCL到Fastly]({{ site.magentourl }}/common/images/cloud_upload-vcl-to-fastly.png)

	<div class="bs-callout bs-callout-info" id="info" markdown="1">
  		如果**Upload VCL to Fastly**按钮没有显示，你应该要升级Fastly扩展到1.2.0或更新。我们推荐1.2.33或更新。Fastly的Composer名称是`fastly/magento2`。
	</div>

2.	一但上传完成，弹框自动地关闭，并弹出一个成功的消息

这次上传，你可以创建和上传自定义高级设置和选项的VCL代码片段。你可以使用API来添加这些VCL代码片段，依赖此动作，进一步添加它们到你的站点代码中

更金信息，参考[Fastly VCL文档](https://docs.fastly.com/guides/vcl/guide-to-vcl){:target="\_blank"} and [Fastly VCL snippets](https://docs.fastly.com/guides/vcl-snippets/about-vcl-snippets){:target="\_blank"}.

## 配置后台及Origin shielding {#backend}
后台设置为Fastly的Origin shielding执行和超时提供微调。_后台_是一个有为检查和提供缓存内容配置了Origin shield和超时设置的是一个指定的位置(IP或域名)

_Origin shielding_为你的网店路由所有的请求到一个指定点(POP)。当接收到一个请求，POP检查缓存的内容并提供它，如果它没有被缓存，会被继续路由到Shied POP,然后到缓存了内容的原始服务器上。shields减少了直接到原始站的流量。

你可以添加多个后台，重复这些指令创建多个后台，例如，你可能要一个后台提供[Wordpress]({{ page.baseurl }}/cloud/configure/fastly-vcl-wordpress.html)来处理你的博客

1. 访问并展开 **Fastly Configuration**.
2. 展开**Backend settings**并点击齿轮图标来配置默认的后台。它会打开一个对话框，上面有选项用于选择和配置。

	![修改后台]({{ site.magentourl }}/common/images/cloud_fastly-backend.png){:width="600px"}
3. 选择与你AWS所在地最近的**Sheild**(或数据中心)的位置。比如，如果你的准生产环境在美国的西海岸(us-west-1),选择`sjc-ca-us`。这有提供缓存服务POP。

	下面列出了基于AWS地区可用哪些Fastly shield位置的关系

	- ap-northeast-1 => tokyo-jp2
	- ap-southeast-1 => singapore-sg
	- ap-southeast-2 => sydney-au
	- ap-south-1 => singapore-sg
	- eu-central-1 => frankfurt-de
	- eu-west-1 => london-uk, london_city-uk
	- eu-west-2 => london-uk, london_city-uk
	- eu-west-3 => cdg-par-fr
	- sa-east-1	=> gru-br-sa
	- us-east-1 => iad-va-us
	- us-east-2 => iad-va-us
	- us-west-1 => sjc-ca-us
	- us-west-2 => sea-wa-us
    
4. 修改连接到shield超时值(毫秒)，字节之间的时间，首字节的时间。我们推荐保持默认超时设置。
5. 可选，编辑或保存之后选择激活后台和Shield。
6. 点击**Upload**保存，设置会被同步到Fastly.
7. 在Magento管理面板，点击**Save Config**.

更多Fastly的信息，参考Magento 2[后台设置向导](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/Guides/BACKEND-SETTINGS.md){:target="\_blank"}.

## 配置清缓存选项{#purge}
Fastly在Magento缓存管理页面提供多类型的清理选项，包括清理的产品目录，产品资源和内容。当启用时，Fastly监听事件来清理这些缓存。如果没有启用。你只能在缓存管理页完成更新后手动清理Fastly缓存

此选项包括：

* **Purge category**: 当你添加及更新一个简单产品时清理产品分类内容(不是产品内容)，你可能想要保持这项禁用并启用清理产品。它会同时清理产品和产品分类。
* **Purge product**: 当保存一个产品的简单修改时清理所有产品和产品分类内容，启用清理产品是有帮助的，当修改价格、添加产品选项及当产品库存不足时，它会立即反应到客户。
* **Purge CMS page**: 当更新或添加页面到Magento CMS时清理页面内容，例如，你可能想当你更新团队和条件或退货政策时清理缓存。如果你很少修改这些内容，你可以此项自动清理。
* **Soft purge**: 设置修改的内容过期并根据过期时间清理，结合过期时间，你的客户将在Fastly在后台更新内容期间快速地被老的内容响应。

![配置清理选项]({{ site.magentourl }}/common/images/cloud_fastly-purgeoptions.png){:width="650px"}

配置Fastly清理选项:

1. 在 **Fastly Configuration**节点，展开 **Advanced**。
2. 所有的清除选项会显示，选择"是"启用自动清除，选择"否"禁用自动清除，但允许你从缓存管理页面手动清除。
3. 点击页面上方的 **Save Config** 。
4. 页面重新加载后，在 *Fastly Configuration* 节点点击  **Upload VCL to Fastly** 

更多信息请参考[Fastly的配置选项](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/CONFIGURATION.md#further-configuration-options){:target="\_blank"}.

## 创建自定义错误/维护页面 {#fastly-errpg}
你可以可选地创建一个自定义的页面来表示错误，或当你的站点要维护的时候。用提供了为什么站点临时下线信息的HTML代码创建你的页面，来代替仅显示HTTP错误代码

要创建自定义错误/维护页面：

1.	在 **Fastly Configuration** 节点展开 **Error/Maintenance Page** ，如下图所示。

	![自定义Fastly错误页面]({{ site.magentourl }}/common/images/cloud-fastly_err-pg.png){:width="650px"}
2.	点击 **Set HTML**。
3.	在提供的输入框中，输入你的HTML代码， 你输入的HTML长度不能超过65,535字节。

	<div class="bs-callout bs-callout-info" id="info" markdown="1">
	避免你的Fastly不可用时在你的站点使用图片，要使用图片，请参考[站点数据URI的css技巧](https://css-tricks.com/data-uris/){:target="\_blank"}.
	</div>
4.	当你完成之后，点击 **Upload** 来更新Fastly
5.	点击页面上方的 **Save Config** 。

## 创建自定义VCL代码片段 {#custom-vcl}
要扩展指令来创建自定义VCL代码片段和需要的边缘字典或ACL,请参考[快速定制VCL片段]({{ page.baseurl }}/cloud/configure/cloud-vcl-custom-snippets.html)

## 为Magento管理员延长Fastly超时 {#bulkaction}
Fastly为Magento管理员的HTTPS请求设置一个180秒的超时，所以如果你要完成一个大块的需要3分钟以上完成的动作你可能会遇到超时。使用Fastly 1.2.41，你可以管理超时

1. 在 *Fastly Configuration* 节点，展开 **Advanced**
2. 设置 **Admin path timeout** 的值，单位是秒。这个值不能大于一个小时(3600秒)
3. 点击页面上方的 **Save Config** 。
4. 页面重新加载后，在 *Fastly Configuration* 节点点击  **Upload VCL to Fastly** 

从1.2.39开始，Fastly获取Magento管理面板路径来从`app/etc/env.php`配置文件生成VCL文件

## 配置GeoIP处理 {#geoip}
Fastly模块包含GeoIP处理来自动定向访客或提供一个网店列表匹配他们拿到的国家代码。如果你已经使用了Magento扩展来进行GeoIP处理，你可能要一起验证Fastly选项中的特性

1. 在 **Fastly Configuration**节点，展开 **Advanced**。
2. 向下滚动至选择 **Yes** 来 **启用GeoIP**,附加的配置选项会显示出来。
3. 对于GeoIP的动作，选择是否访客自动重定向 **Redirect** ，或从 **对话框**选择以提供一个网店列表
4. 对于 **Country Mapping**, 点击 **添加** 来输入一个两个字母的国家代码映射一个特定的列表中Magento网店，国家代码请参考[此链接](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2){:target="\_blank"}.

	![添加GeoIP国家映射]({{ site.magentourl }}/common/images/cloud_fastly-geo-code.png)
5. 点击页面上方的 **Save Config** 。
6. 页面刷新后，在 *Fastly Configuration*节点点击 *Upload VCL to Fastly*

Fastly 也提供了一系列的[地理位置相关的VCL特性](https://docs.fastly.com/guides/vcl/geolocation-related-vcl-features){:target="\_blank"}来定制地理位置的代码

## 为Fastly配置DNS {#fastly-dns}
当你要上线时，你必须完成这些步骤

在检查你的注册商在哪修改你的DNS配置之后，为你的指向Fastly服务`prod.magentocloud.map.fastly.net`的站点添加一个CNAME记录。如果你的站点使用了多主机名，你必须给每一个添加一个CNANE记录。

<div class="bs-callout bs-callout-info" id="info">
<p>使用<a href="https://blog.cloudflare.com/zone-apex-naked-domain-root-domain-cname-supp" target="_blank">顶级域名</a>(或提供一个<em>裸</em>域名)它是不会工作的。你必须使用一个支持转发DNS请求的DNS供应商来使用你的顶级域名。</p>
</div>

下面列出了包含DNS服务商的信息的例子，使用你的首选的DNS服务商

*	CNAME with ALIAS record from [Dyn](http://dyn.com){:target="_blank"}
*	ANAME record on [DNS Made Easy](http://www.dnsmadeeasy.com){:target="_blank"}
*	ANAME at [easyDNS](https://www.easydns.com){:target="_blank"}
*	ACNAME at [CloudFlare](https://www.cloudflare.com){:target="_blank"}
*	ALIAS at [PointDNS](https://pointhq.com){:target="_blank"}

许多其它的DNS服务商也提供完成此工作的解决办法。最通常的方法是为此域名上的`www`主机在添加一个CNAME记录，然后使用DNS提供商的重定向服务重定向顶级域名到这个域名的`www`域名上，查阅你的DNS提供商了解更多信息。

另一种方法是为顶级域名添加一个A记录，映射一个域名到Fastly的IP地址`150.101.113.124`。

参考[上线检查]({{ page.baseurl }}/cloud/live/go-live-checklist.html) 了解更多信息。

### TLS和Fastly {#fastly-tls}
如果你在Fastly环境中使用了TLS并也启用了,你必须提供给你的DNS提供商你的Fastly的一个text记录,我们提供一个验证SSL证书的启用了子项备选名的域名，由GlobalSign发行，当你要为你的DNS信息提交[支持工单]{{ page.baseurl }}/cloud/trouble/trouble.html)并要上线时，请让我们知道你用了TLS，提供你的域名并请求TXT记录。然后你可以发送这个记录到你的DNS服务商。域名认证过程会被Fastly执行。

更多关于TXT记录的信息，请参考Fastly的 [DNS TXT记录验证](https://docs.fastly.com/guides/securing-communications/domain-validation-for-tls-certificates#dns-text-record-verification){:target="\_blank"}.

## 升级Fastly {#upgrade}
Fastly通过更新Magento模块来解决问题，增强性能及提供新的特性，你可以检查[Magento Marketplace](https://marketplace.magento.com/fastly-magento2.html){:target="\_blank"} and [GitHub](https://github.com/fastly/fastly-magento2/releases){:target="\_blank"} 来获取最新的版本。

当你升级Fastly，你会获得默认VCL代码片段的升级的子集。当你完成了升级，你必须[上传升级默认的VCL代码片段到Fastly](#upload-vcl-snippets):

1. 在 *Fastly Configuration* 节点，点击 **Upload VCL to Fastly**
2. 上传完成之后，对话框会自动关闭，并弹出一个成功消息。

当你升级时，你上传的默认的VCL代码片段不应该被影响或进行其它步骤

更多关于升级模块的信息，请参考[安装，管理及升级模块]({{ page.baseurl }}/cloud/howtos/install-components.html).

如果你创建一个自定义的VCL代码片段使用了与默认代码片段相同的名字，你可能需要验证和更新这些代码片段。我们不推荐相同的名字以自定义代码片段替换现存的默认代码片段。关于自定义VCL的更多信息，请参考[快速定制VCL片段]({{ page.baseurl }}/cloud/configure/cloud-vcl-custom-snippets.html).
