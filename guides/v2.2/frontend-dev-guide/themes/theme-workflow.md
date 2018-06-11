---
group: fedg
subgroup: A_Themes
title: 主题开发 workflow
menu_title: 主题开发 workflow
menu_order: 10
version: 2.2
github_link: frontend-dev-guide/themes/theme-workflow.md
functional_areas:
  - Frontend
  - Theme
---


<div class="flow-intro" markdown="1">
Continue From:<br />
**安装Magento**
</div>

<div class="flow-arrow"> </div>

<div class="flow-block" markdown="1">

### Enable development mode

In the Magento root directory, run:

`php bin/magento deploy:mode:set developer`



* [关于Magento的模式]({{ page.baseurl }}/config-guide/bootstrap/magento-modes.html)
* [命令行配置起步]({{ page.baseurl }}/config-guide/cli/config-cli-subcommands.html)

<div class="bs-callout bs-callout-tip" markdown="1">
To check the current mode of your Magento instance, in the root directory, run:

`php bin/magento deploy:mode:show`
</div>
</div>

<div class="flow-arrow"> </div>

<div class="flow-block" markdown="1">
### Create basic theme files
In the `<magento_root>/app/design/frontend/<Your_Vendor>/<your_theme>` directory, create the following files:

- `theme.xml`
- `registration.php`
- (optionally) `composer.json`

For details, see [创建一个新的前台主题]({{ page.baseurl }}/frontend-dev-guide/themes/theme-create.html)
</div>

<div class="flow-arrow"> </div>

<div class="flow-block" markdown="1">
### Apply the theme

1. In the Admin Panel, go to **CONTENT** > **Design** > **Configuration**
2. Find the record corresponding to your store view and click **Edit**.
3. In the **Applied Theme** drop-down, select your newly created theme.
4. Click **Save Configuration**.

For details, see [应用和配置前台主题]({{ page.baseurl }}/frontend-dev-guide/themes/theme-apply.html)
</div>

<div class="flow-arrow"></div>

<div class="flow-block" markdown="1">

### Choose .less compilation mode
</div>
<div class="flow-arrow"></div>

<div class="flow-row">

<div class="flow-column">
<div class="flow-block" markdown="1">
#### Grunt (recommended)

* [Setup Grunt]({{ page.baseurl }}/frontend-dev-guide/tools/using_grunt.html)
* [Add the theme to Grunt configuration]({{ page.baseurl }}/frontend-dev-guide/css-topics/css_debug.html#add_theme)
* [Track changes]({{ page.baseurl }}/frontend-dev-guide/css-topics/css_debug.html#grunt_commands)

</div>
<div class="flow-nav top-bottom"></div>
</div>

<div class="flow-column">
<div class="flow-block" markdown="1">
#### Client-side compilation
See [CSS预处理#client-side compilation mode]({{ page.baseurl }}/frontend-dev-guide/css-topics/css-preprocess.html#client-side)
</div>

</div>
<div class="flow-column">
<div class="flow-block" markdown="1">
#### Server-side compilation (default)
See [CSS预处理#server-side compilation mode]({{ page.baseurl }}/frontend-dev-guide/css-topics/css-preprocess.html#server-side)
</div>

</div>

<div class="flow-column">
<div class="flow-block" markdown="1">
#### Custom preprocessor
See [使用自定义css预处理器]({{ page.baseurl }}/frontend-dev-guide/css-topics/custom-preprocess-parent.html)
</div>

</div>


</div>

<div class="flow-row">

<div class="flow-column">
<div class="flow-nav turn-right"></div>
</div>
<div class="flow-column">
<div class="flow-nav turn-left-right"></div>
</div>
<div class="flow-column">
<div class="flow-nav turn-left-right"></div>
</div>
<div class="flow-column">
<div class="flow-nav turn-left"></div>
</div>

</div>

<div class="flow-arrow"></div>



<div class="flow-block" markdown="1">
### Create your styles


* [Quick start guide to working with styles]({{ page.baseurl }}/frontend-dev-guide/css-guide/css_quick_guide_overview.html)
* [All about styles in Magento themes]({{ page.baseurl }}/frontend-dev-guide/css-topics/css-overview.html)
</div>
<div class="flow-arrow"></div>


<div class="flow-block" markdown="1">
### Debug
See:

* [Locate the CSS/Less file you need to change]({{ page.baseurl }}/frontend-dev-guide/themes/debug-theme.html)
* [CSS source maps]({{ page.baseurl }}/frontend-dev-guide/css-topics/css_debug.html#source_maps)
* [Track changes using Grunt]({{ page.baseurl }}/frontend-dev-guide/css-topics/css_debug.html#use_cases)
</div>
<div class="flow-arrow"></div>

<div class="flow-block" markdown="1">
### Clean cache and/or static files if necessary

* Certain changes in styles require cleaning previously pre-processed and published static view files. Run `grunt clean <theme>` or manually clear the `pub/static` and `var/view_preprocessed` directories. Do this after any changes in server-side compilation mode. For the client-side or Grunt compilation, see [Сlean static files]({{ page.baseurl }}/frontend-dev-guide/css-topics/css-preprocess.html#css_exception) for details.

* Changes in layout and templates requires cleaning cache. See [Clean cache]({{ page.baseurl }}/frontend-dev-guide/cache_for_frontdevs.html#clean_cache) for details.

</div>
<div class="flow-arrow"></div>

<div class="flow-block flow-block-optional" markdown="1">
### Make sure that the same styles are delivered to production (optional)

When you finish developing and your styles are ready to go to production, you can configure your Grunt/Gulp less compiler to minify compiled code, disable source maps generation and then copy the compiled files to `/app/design/frontend/<Vendor>/<theme>/web/css` directory next to source files. They will be used in static content deploy instead of running backend compilation (and static content deployment process will run faster).
</div>
<div class="flow-arrow"></div>

<div class="flow-block" markdown="1">
### Switch to production mode

In the Magento root directory, run:

`php bin/magento deploy:mode:set production`

See [Magento modes]({{ page.baseurl }}/config-guide/bootstrap/magento-modes.html#production-mode) for details.
</div>
<div class="flow-arrow"></div>

<div class="flow-block" markdown="1">
### Deploy static content

To publish your static files to the `pub/static` directory when your Magento instance is set to production mode, [run the static content deployment tool]({{ page.baseurl }}/config-guide/cli/config-cli-subcommands-static-view.html).
