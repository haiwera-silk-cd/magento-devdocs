<div markdown="1">

![Magento安装是如何工作的]({{ site.magentourl }}/common/images/install_diagram.png){:width="1100px"}

图示展示了以下信息:

1.	准备服务器环境.

	安装所需软件, 包括 PHP, Apache, 和MySQL. 点击下面的链接查阅指定版本的系统要求:

	*	[2.0.x 系统要求]({{ site.gdeurl }}install-gde/system-requirements.html)
	*	[2.1.x 系统要求]({{ site.gdeurl21 }}install-gde/system-requirements-tech.html)
	*	[2.2.x 系统要求]({{ site.gdeurl22 }}install-gde/system-requirements-tech.html)

2.	获取Magento.

	*	为简单起见, 这里选择下载一个{{site.data.var.ce}}或{{site.data.var.ee}} [压缩包]({{ page.baseurl }}/install-gde/prereq/zip_install.html),把它解压到你的服务器,并开始安装.

	*	如果你足够熟悉composer, 你可以通过composer获取{{site.data.var.ce}}或{{site.data.var.ee}}的[工程包]({{ page.baseurl }}/install-gde/prereq/integrator_install.html).

	*	如果你想为{{site.data.var.ce}}贡献你的力量, 你可以在GitHub上[clone]({{ page.baseurl }}/install-gde/prereq/dev_install.html)Magento 2的仓库. (当然这要求你足够熟悉github和composer)

	<div class="bs-callout bs-callout-info" id="info">
		<p>为了能够使用网页向导来安装或升级你的Magento,或者管理你从Marketplace上下下来的扩展，你必是使用压缩包或composer来安装的</p>
		<p>如果你是克隆仓库的,那么将不能使用网页向导来安装或升级Magento及其扩展，而只能使用<a href="{{ page.baseurl }}/install-gde/install/cli/dev_options.html">Composer和git命令</a>.</p>
	</div>

3.	使用网页向导或命令行安装Magento及其扩展

	为简单起见, 图示仅展示网页向导安装.

	每个步骤，向导都会验证你的输入，如图所示，如果验证未通过，你必须修改这些问题才能继续

	如果失败原因是未正确安装所需的软件，请参考[先决条件]({{ page.baseurl }}/install-gde/prereq/prereq-overview.html).

4.	打开你的商城和后台链接，验证安装是否正确
