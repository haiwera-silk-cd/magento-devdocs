<div markdown="1">

1. Access your account. You can open the email you received from Magento Cloud (accounts@magento.cloud) and click the _Access your project now_ link. Or you can log in to [你的Magento账号](https://accounts.magento.cloud){:target="_blank"}.
2. Click the _This project has no code yet_ link next to the Project name.

	![没有代码的项目]({{ site.magentourl }}/common/images/cloud_project_empty.png)

3. 填写项目名称。

	![项目名称]({{ site.magentourl }}/common/images/cloud_project_name.png)

4. Click **从模板创建一个空站点** and click **继续**. We recommend starting with the Magento template as your initial project option. If you have an existing Magento deployment, you can later import code, extensions, themes, and data after fully deploying this base Magento code.

	![使用样本Magento项目创建一个站点]({{ site.magentourl }}/common/images/cloud_project_template.png){:width="650px"}

5. 当弹出提示时，在弹出的输入框输入你的{{site.data.var.ee}}的[Magento authentication keys]({{ page.baseurl }}/install-gde/prereq/connect-auth.html)。你之前在Magento市场创建了这些密钥。输入私钥和公钥然后点击 **完成**

	![输入认证密钥]({{ site.magentourl }}/common/images/cloud-project-magento-auth-creds.png){:width="650px"}

	The keys are added to the `auth.json` file in the repository `master` branch, required for all created branches and deployments.

6. 你的项目部署要等几分钟，完成这前会显示 _Pending_  的状态，如下图所示：

	![你的样本Magento项目]({{ site.magentourl }}/common/images/cloud_project_template2.png){:width="650px"}

7. 项目部署完后，**成功** 会显示在你的项目名称旁边
