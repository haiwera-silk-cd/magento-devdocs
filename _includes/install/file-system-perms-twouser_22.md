Complete the following tasks in the order shown:

*	[About the shared group](#mage-owner-about-group)
*	[步骤1. Create the Magento文件系统所有者 and give the user a strong password](#mage-owner-create-user)
*	[步骤2. Find the web server group](#install-update-depend-user-findgroup)
*	[步骤3. Put the Magento文件系统所有者 in the web server's group](#install-update-depend-user-add2group)
*	[步骤4. 获取Magento](#perms-get-software)
*	[步骤5. Set ownership and permissions for the shared group](#perms-set-two-users)

### About the shared group {#mage-owner-about-group}
To enable the web server to write files and directories in the Magento file system but to also maintain *ownership* by the Magento文件系统所有者, both users must be in the same group. This is necessary so both users can share access to Magento files (including files created using the Magento Admin or other web-based utilities).

This section discusses how to create a new Magento文件系统所有者 and put that user in the web server's group. You can use an existing user account if you wish; we recommend the user have a strong password for security reasons.

<div class="bs-callout bs-callout-info">
	Skip to <a href="#install-update-depend-user-findgroup">step 2</a> if you plan on using an existing user account.
</div>

### 步骤1. Create the Magento文件系统所有者 and give the user a strong password {#mage-owner-create-user}
This section discusses how to create the Magento文件系统所有者. (Magento文件系统所有者 is another term for the *command-line user*.)

To create a user on CentOS or Ubuntu, enter the following command as a user with `root` privileges:

	adduser <username>

To give the user a password, enter the following command as a user with `root` privileges:

	passwd <username>

Follow the prompts on your screen to create a password for the user.

<div class="bs-callout bs-callout-warning">
    <p>If you don't have <code>root</code> privileges on your Magento server, you can use another local user account. Make sure the user has a strong password and continue with <a href="#install-update-depend-user-add2group">Put the Magento文件系统所有者 in the web server group</a>.</p>
</div>

For example, to create a user named `magento_user` and give the user a password, enter:

	sudo adduser magento_user
	sudo passwd magento_user

<div class="bs-callout bs-callout-warning">
    <p>Because the point of creating this user is to provide added security, make sure you create a <a href="https://en.wikipedia.org/wiki/Password_strength" target="&#95;blank">strong password</a>.</p>
</div>

### 步骤2. Find the web server user's group {#install-update-depend-user-findgroup}
To find the web server user's group:

*	CentOS: `egrep -i '^user|^group' /etc/httpd/conf/httpd.conf`

	Typically, the user and group name are both `apache`
*	Ubuntu: `ps aux | grep apache` to find the apache user, then `groups <apache user>` to find the group

	Typically, the user name and the group name are both `www-data`

### 步骤3. Put the Magento文件系统所有者 in the web server's group {#install-update-depend-user-add2group}
To put the Magento文件系统所有者 in the web server's primary group (assuming the typical Apache group name for CentOS and Ubuntu), enter the following command as a user with `root` privileges:

*	CentOS: `usermod -a -G apache <username>`
*	Ubuntu: `usermod -a -G www-data <username>`

<div class="bs-callout bs-callout-info" id="info" markdown="1">
The `-a -G` options are important because they add `apache`或`www-data` as a _secondary_ group to the user account, which preserves the user's _primary_ group. Adding a secondary group to a user account helps [restrict file ownership and permissions](#perms-set-two-users) to ensure members of a shared group only have access to certain files.
</div>

For example, to add the user `magento_user` to the `apache` primary group on CentOS:

	sudo usermod -a -G apache magento_user

To confirm your Magento user is a member of the web server group, enter the following command:

	groups magento_user

The following sample result shows the user's primary (`magento`) and secondary (`apache`) groups.

	magento_user : magento_user apache

<div class="bs-callout bs-callout-info" id="info" markdown="1">
Typically, the user name and primary group name are the same.
</div>

To complete the task, restart the web server:

*	Ubuntu: `service apache2 restart`
*	CentOS: `service httpd restart`

### 步骤4. 获取Magento {#perms-get-software}
If you haven't done so already, 获取Magento in one of the following ways:

*	[Compressed archive]({{ page.baseurl }}/install-gde/prereq/zip_install.html)
*	[Composer metapackage]({{ page.baseurl }}/install-gde/prereq/integrator_install.html)
*	[Clone the repository (contributing developers only)]({{ page.baseurl }}/install-gde/prereq/dev_install.html)

### 步骤5. Set ownership and permissions for the shared group {#perms-set-two-users}
To set ownership and permissions before you install the Magento software:

1.	Log in to your Magento server as, or switch to, the Magento文件系统所有者.
2.	Enter the following commands in the order shown:

		cd <your Magento install dir>
		find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} \;
		find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} \;
		sudo chown -R :<web server group> .
		chmod u+x bin/magento

{% include install/file-system-perms-twouser_cmds-only_22.md %}

### 下一步
After you have set file system ownership and permissions, continue with any of the following:

*	[Command-line installation]({{ page.baseurl }}/install-gde/install/cli/install-cli.html)
*	[网页向导安装]({{ page.baseurl }}/install-gde/install/web/install-web.html)
