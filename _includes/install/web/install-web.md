<div markdown="1">

This section discusses how to install the Magento software using a web-based wizard interface. To install Magento from the command line, see <a href="{{ page.baseurl }}/install-gde/install/cli/install-cli.html">Install Magento software using the command line</a>.

<h2 id="instgde-install-prereq">在你开始安装之前</h2>

在你开始之前，请确保：

1.	你的系统已经满足我们在<a href="{{ page.baseurl }}/install-gde/system-requirements.html">Magento系统要求</a>中所讨论的要求.
2.	你已经完成了我们在<a href="{{ page.baseurl }}/install-gde/prereq/prereq-overview.html">先决条件</a>讨论的所有必要的任务.
4.	在你登录到Magento服务器之后，<a href="{{ page.baseurl }}/install-gde/prereq/file-sys-perms-over.html">切换到Magento文件所有者身份</a>.

<h3 id="instgde-install-web-enable-mod">Enabling and disabling modules</h3>
The Setup Wizard enables you to 启用或禁用模块 before you install the Magento software. Before you do so, make sure you understand the following.

{% include install/enable-disable-modules.html %}

<h2 id="instgde-install-magento-web">Running the Setup Wizard</h2>
The Setup Wizard is a multi-page wizard that enables you to go back and forward one page at a time. You *cannot* skip pages, and you must enter all required information on every page before you can proceed to the next page.

In the event of errors, you can run the installer again or you can return to a previous page to fix errors on that page.

<h3 id="instgde-install-magento-web-step0">Getting started</h3>
To install the Magento software using the Setup Wizard:

1.	Start a web browser.

2.	Enter the following URL in the browser's address or location bar:

		http://<Magento host or IP>/<path to Magento root>/setup
	
	For example, if the Magento server's IP address is 192.0.2.10 and you installed Magento 2 in the <tt>magento2</tt> directory relative to the web server's docroot, and you did not configure a Virtual Host, enter:
	
		http://192.0.2.10/magento2/setup
	
3.	On the initial page, click **Agree and Set Up Magento**.

4.	Continue with the following topics in the order presented to complete the installation.

