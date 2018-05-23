<div markdown="1">

### Find the Magento software version {#magento-version}
To find the version of the Magento software:

*	If you downloaded the Magento software using a Composer metapackage, enter the following command:

		php <your Magento install dir>/bin/magento --version
*	If you cloned the Magento 2 GitHub repository, enter the following commands:

		cd <your Magento 2 clone directory>
		git branch

	If you're currently in the `develop` branch, you must change to a <a href="{{ page.baseurl }}/install-gde/install/cli/dev_downgrade.html">released branch</a> before you continue.

### Find the 数据迁移工具 version {#migration-tool-version}

To find the version of the migration tool: 

* Change to your 数据迁移工具 directory: `vendor/magento/data-migration-tool`.
* Open `composer.json` in a text editor.
* Find the value of "version"

	This is the version of your 数据迁移工具.
