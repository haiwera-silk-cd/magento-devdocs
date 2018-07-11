---
group: install
subgroup: 01_Verify
title: 验证你的安装
menu_title: 验证你的安装
menu_node: parent
menu_order: 1
version: 2.1
github_link: install-gde/install/verify.md
redirect_from: /guides/v1.0/install-gde/install/verify.html
functional_areas:
  - Install
  - System
  - Setup
---

<h2 id="instgde-verify-front-sample">验证网店 (with optional sample data)</h2>
Go to the {% glossarytooltip 1a70d3ac-6bd9-475a-8937-5f80ca785c14 %}网站前台{% endglossarytooltip %} in a web browser. 例如， if your Magento installation base {% glossarytooltip a05c59d3-77b9-47d0-92a1-2cbffe3f8622 %}URL{% endglossarytooltip %} is `http://www.example.com`, enter it in your browser's address or location bar.

The following figure shows a sample storefront page. If it displays as follows, your installation was a success!

<p><img src="{{ site.baseurl }}/common/images/install-success_store-luma.png" alt="Magento storefront with the Luma theme"></p>


<h2 id="instgde-verify-front">验证网店 (no sample data)</h2>

Go to the storefront in a web browser. 例如， if your Magento installation base URL is `http://www.example.com`, enter it in your browser's address or location bar.

The following figure shows a sample storefront page. If it displays as follows, your installation was a success!

<p><img src="{{ site.baseurl }}/common/images/install-success_store.png" width="450px" alt="Magento storefront which verifies a successful installation"></p>

If the page displays a 404 (Not Found) or unconfigured (no styles, only text), see <a href="{{ page.baseurl }}/install-gde/trouble/tshoot_no-styles.html">安装后图片和样式缺失，显示错乱</a>.

<h2 id="instgde-verify-admin">Verify the Magento Admin</h2>

Go to the {% glossarytooltip 18b930cf-09cc-47c9-a5e5-905f86c43f81 %}Magento管理面板{% endglossarytooltip %} in a web browser. 例如， if your Magento installation base URL is `http://www.example.com`, and the Admin URI is `admin_au1nT`, enter `http://www.example.com/admin_au1nT` in your browser's address or location bar.

(The {% glossarytooltip 29ddb393-ca22-4df9-a8d4-0024d75739b1 %}Admin{% endglossarytooltip %} URI is specified by the value of the `backend-frontname` installation parameter.)

When prompted, log in as a Magento Administrator.

The following figure shows a sample Magento Admin page. If it displays as follows, your installation was a success!

<p><img src="{{ site.baseurl }}/common/images/install_success_admin.png" alt="Magento Admin which verifies a successful installation"></p>

If the page displays unconfigured (no styles, only text), see <a href="{{ page.baseurl }}/install-gde/trouble/tshoot_no-styles.html">安装后图片和样式缺失，显示错乱</a>.

If you get a 404 (Not Found) error similar to the following, see <a href="{{ page.baseurl }}/install-gde/trouble/tshoot_access-browser.html">使用浏览器无法访问Magento</a>.

`The requested URL /magento2index.php/admin/admin/dashboard/index/key/0c81957145a968b697c32a846598dc2e/ was not found on this server.`
