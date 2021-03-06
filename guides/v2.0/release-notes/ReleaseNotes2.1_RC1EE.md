---
group: release-notes
subgroup: 02_rel-notes
title: Magento Commerce 2.1 Release Candidate 1 (RC1) Release Notes 
menu_title: Magento Commerce 2.1 Release Candidate 1 (RC1) Release Notes 
menu_order: 421
version: 2.0
level3_menu_node: level3child
level3_subgroup: rc20-relnotes
github_link: release-notes/ReleaseNotes2.1_RC1EE.md
---

We are pleased to present Magento 2.1 Release Candidate 1 (RC1). This release candidate build is not intended for production purposes. Instead, it provides the development community opportunities to: 

* preview the new features and fixes that Magento 2.1 GA will contain

* contribute to the Magento 2.1 code base by identifying unresolved issues

* test your 2.0 extensions against  2.1 

We welcome your participation in this process! Magento Commerce customers can provide feedback in these two ways: 

* Magento Commerce GitHub repository.  For more information on how to provide feedback and contribute on GitHub, see <a href="{{ page.baseurl }}/contributor-guide/contributing.html" target="_blank">Code contributions</a>. 

* 邮箱 to DL-Magento-2.1-Feedback@magento.com.


This Release Candidate is available from `repo.magento.com` if you have an Magento Commerce license or GitHub  if you have previously signed an agreement to access Magento Commerce 2.0 beta software on GitHub.


Backward-incompatible changes are documented in <a href="http://devdocs.magento.com/guides/v2.0/release-notes/changes_2.0.html" target="_blank">Magento 2.0 Backward Incompatible Changes</a>.


<h3>Highlights</h3>

Magento Commerce (formerly Enterprise Edition) 2.1 includes several new features:

* **Content Staging and Preview** improves productivity by enabling business teams to easily create, preview, and schedule a wide range of content updates without involving IT. Merchants can make updates to products, categories, {% glossarytooltip f3944faf-127e-4097-9918-a2e9c647d44f %}CMS{% endglossarytooltip %} content, promotions, and pricing and can preview these changes based on specific dates and times or store views. User-friendly dashboards provide greater visibility into all planned site changes and updates can be automatically deployed at scheduled times.
 
* **Elasticsearch is a next-generation search technology** that is replacing Solr in Magento Commerce 2.1. It is simpler to set up, able to handle large catalogs, and can easily scale as search volume grows. It supports 33 languages out-of-the-box, and merchants can configure stop words and synonyms to ensure high quality search results.

* **PayPal in-context {% glossarytooltip 278c3ce0-cd4c-4ffc-a098-695d94d73bde %}checkout{% endglossarytooltip %} helps to increase {% glossarytooltip 38c73ce4-8f01-4f74-ab30-1134cec5664f %}conversion{% endglossarytooltip %} rates** by allowing shoppers to pay with PayPal without leaving the merchant’s site. PayPal saved credit card capabilities allow merchants to securely store credit cards with PayPal so shoppers can make future purchases without re-entering their credit card information.
 
* **Braintree enhancements enable merchants to qualify for the simplest set of PCI compliance** requirements by using Braintree Hosted Fields to collect all sensitive {% glossarytooltip 117df0a3-29a6-4636-9c29-8f696b3ad737 %}cardholder{% endglossarytooltip %} information in checkout. Merchants retain complete control over their checkout style and {% glossarytooltip 73ab5daa-5857-4039-97df-11269b626134 %}布局{% endglossarytooltip %} because Braintree uses small, transparent iframes to replace individual payment fields. Merchants can now also access Braintree {% glossarytooltip 73a87074-8de7-4e69-a97f-12c65c6f5582 %}settlement{% endglossarytooltip %} reports from within the {% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento管理面板{% endglossarytooltip %}.
 
* **Improved management interfaces** make it faster and easier to search for information in the Admin, set up global search synonyms, and create new product, category, and CMS content.


<h3>Known issue</h3>

<b>Issue:</b> Enabling Varnish causes the {% glossarytooltip 50e49338-1e6c-4473-8527-9e401d67ea2b %}category{% endglossarytooltip %} menu to switch from http to https<a href="https://github.com/magento/magento2/issues/4540" target="_blank"> (GITHUB-4540)</a>

<b>Work-around:</b> To use Varnish caching with an HTTP site, add rewrite rules such as the following in Magento's root `.htaccess`: 

<pre>RewriteCond %{HTTPS} on
RewriteCond %{REQUEST_URI} /yellow-fruit.html
RewriteRule (.*) http://%{HTTP_HOST}%{REQUEST_URI} [L]</pre>

<pre>RewriteCond %{HTTPS} on
RewriteCond %{REQUEST_URI} /red-fruit.html
RewriteRule (.*) http://%{HTTP_HOST}%{REQUEST_URI} [L]</pre>

 
<h3>Fixed issues</h3>

This release includes fixes for the following GitHub issues:

<!--- 52414 --> * Integration test syntax error has been fixed. <a href="https://github.com/magento/magento2/issues/4343" target="_blank">(GITHUB-4343)</a> 

<!--- 50611--> * Web APIs no longer allow anonymous access by default. <a href="https://github.com/magento/magento2/issues/3786" target="_blank">(GITHUB-3786)</a>

<!--- 51292 --> * The OAuth Token exchange expiration period is now calculated correctly. <a href="https://github.com/magento/magento2/issues/3449" target="_blank">(GITHUB-3449)</a> 

<!--- 46720 --> * Shipping Address is now exposed for the Orders {% glossarytooltip 786086f2-622b-4007-97fe-2c19e5283035 %}API{% endglossarytooltip %}. <a href="https://github.com/magento/magento2/issues/2628" target="_blank">(GITHUB-2628)</a>


<!--- 52613 --> * A {% glossarytooltip 6a9783a3-cdec-4fed-843d-8eda12819804 %}Credit Memo{% endglossarytooltip %} REST API issue with updating attributes has been fixed. Previously, certain attributes (such as Order Status) were not updated when the user took action through the API. However, Magento updates these attributes when the same action is completed in the {% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}Admin{% endglossarytooltip %} interface. <a href="https://github.com/magento/magento2/issues/4329" target="_blank">(GITHUB-4329)</a>  

<!--- 52607 --> *  Varnish caching performance has been enhanced. <a href="https://github.com/magento/magento2/issues/3926" target="_blank">(GITHUB-3926)</a> 

<!--- 52316 --> *  Product update operations by either customers or store administrators no longer result in locking queries on {% glossarytooltip 8d40d668-4996-4856-9f81-b1386cf4b14f %}catalog{% endglossarytooltip %} category product index. <a href="https://github.com/magento/magento2/issues/4342" target="_blank">(GITHUB-4342)</a> 

<!--- 52079 --> * The Order Repository GetList method no longer returns the same shipping address for all orders. <a href="https://github.com/magento/magento2/issues/4019" target="_blank">(GITHUB-4019)</a> 

<!--- 51181 --> * A configurable product's last attribute with price of zero (0) no longer results in an error. The user can configure the product, and the correct price results. <a href="https://github.com/magento/magento2/issues/3912" target="_blank">(GITHUB-3912)</a> 

<!--- 48175 --> * An error message that users typically received during upgrade has been improved. The message now clearly states when a user must login first to `magento.com` before continuing the upgrade process. <a href="https://github.com/magento/magento2/issues/3059" target="_blank">(GITHUB-3059)</a> 

<!--- 47440 --> *  Magento now displays the correct product prices on the {% glossarytooltip 2fd4d100-28d2-45ca-bec1-128444ea98e6 %}Configurable product{% endglossarytooltip %} page when catalog prices include tax. <a href="https://github.com/magento/magento2/issues/2471" target="_blank">(GITHUB-2471)</a> 

<!--- 47439 --> * The `i18n:collect-phrases -m` command now works correctly. Previously, this command would not find all important Magento phrases. <a href="https://github.com/magento/magento2/issues/2630" target="_blank">(GITHUB-2630)</a>

<!--- 47009 --> *  Plugins/interceptors now work with early stage single instance objects in Developer mode. <a href="https://github.com/magento/magento2/issues/2674" target="_blank">(GITHUB-2674)</a> 

<!--- 46808 --> * Admin order creation no longer fails when the "Include Tax In Order Total" option is set to yes. <a href="https://github.com/magento/magento2/issues/2675" target="_blank">(GITHUB-2675)</a> 

<!--- 47639 --> * The `setup:di:compile` script now compiles all files as expected. <a href="https://github.com/magento/magento2/issues/2888" target="_blank">(GITHUB-2888)</a>

<!--- 46044 --> * Synonyms now work as expected with Magento 2.x.  <a href="https://github.com/magento/magento2/issues/2519" target="_blank">(GITHUB-2519)</a> 

<!--- 40320 --> * Attribute 'setup_version' is missing for {% glossarytooltip c1e4242b-1f1a-44c3-9d72-1d5b1435e142 %}模块{% endglossarytooltip %} error when defined as optional. <a href="https://github.com/magento/magento2/issues/1493" target="_blank">(GITHUB-1493)</a>

<h3>技术栈</h3>

Our technology stack is built on {% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %} and MySQL. Magento 2.1 RC3 supports:

* PHP 5.6
* PHP 7.0.2
* PHP 7.0.6 + up until 7.1
* MySQL 5.6.

We do not support PHP 5.5.x or 7.0.5. 

## Installation and upgrade instructions
You can install Magento Commerce 2.1 Release Candidate 1 (RC1) using {% glossarytooltip d85e2d0a-221f-4d03-aa43-0cda9f50809e %}Composer{% endglossarytooltip %}. 

This Release Candidate is for test purposes only. Do not install it in a production environment.

See one of the following sections:

*	[使用Composer安装](#install-rc-composer)
*	[Upgrade existing installations](#upgrade-rc-nosamp)
*	[Upgrade to an RC with sample data](#upgrade-rc-samp)

## 使用Composer安装 {#install-rc-composer}
This Release Candidate is available from `repo.magento.com`. Before installing this Release Candidate using Composer,  familiarize yourself with these  <a href="{{ page.baseurl }}/install-gde/prereq/integrator_install.html" target="_blank">先决条件</a>, then run:

		composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition=2.1.0-rc2 <installation directory name>

## Upgrade existing installations {#upgrade-rc-nosamp}
This section discusses how to upgrade to a Release Candidate *without* sample data.

If you installed optional sample data, see [Upgrade to an RC with sample data](#upgrade-rc-samp) instead.

<div class="bs-callout bs-callout-warning">
    <p><em>Do not</em> upgrade to a Release Candidate on a production system. Upgrade to a Release Candidate on a development system only.</p>
</div>

### Upgrade using the Setup Wizard
Use the instructions in [开始系统升级]({{ page.baseurl }}/comp-mgr/upgrader/upgrade-start.html). When prompted to choose a version, choose a Release Candidate.

### Upgrade an existing installation from the GitHub repository
Developers who contribute to the Open Source codebase can <a href="{{ page.baseurl }}/comp-mgr/bk-compman-upgrade-guide.html" target="_blank">upgrade manually</a> from the Magento Open Source GitHub repository.

1.	Go to the <a href="{{ page.baseurl }}/install-gde/install/cli/dev_update-magento.html" target="_blank">Contributing Developers</a> page.

2.	Follow the instructions to pull the updates from the repository and update using Composer.

### Upgrade using the command line

{% collapsible To upgrade to a Release Candidate using the command line: %}

1.	Log in to your Magento server as, or switch to, the Magento文件系统所有者.
2.	Change to the directory in which you installed the Magento software.

	例如， `cd /var/www/html/magento2`
2.	Enter the following commands in the order shown:

		composer require <product> 2.1.0-rc1 --no-update
		composer update

	To upgrade to Magento Open Source 2.1 RC1, enter:

		composer require magento/product-community-edition 2.1.0-rc1 --no-update
		composer update

	To upgrade to Magento Commerce 2.1 RC1, enter:

		composer require magento/product-enterprise-edition 2.1.0-rc1 --no-update
		composer update
	
3.	If prompted, enter your [authentication keys]({{ page.baseurl }}/comp-mgr/prereq/prereq_auth-token.html).
4. Update the database schema and data:

		php bin/magento setup:upgrade

{% endcollapsible %}

## Upgrade to an RC with sample data {#upgrade-rc-samp}

{% include install/sampledata/sample-data-rc1-cli.md %}











