---
group: cloud
subgroup: 090_configure
title: VCL自定义自重向到WordPress
menu_title: VCL自定义自重向到WordPress
menu_order:
menu_node:
version: 2.0
github_link: cloud/configure/fastly-vcl-wordpress.md
functional_areas:
  - Cloud
  - Setup
---

This example details how to redirect to another backend using an Edge Dictionary and VCL. You may have a separate WordPress blog for all of your store's blog entries, kept separate from your store. For this example, you are trying to check the first part of the incoming path and redirect the visitor to your WordPress backend. You would create an Edge Dictionary called `wordpress_urls` with a list of paths to redirect traffic.

You must have the following information to complete this VCL code snippet:

* Create an Edge Dictionary in your environments
* Account access and URL to the Magento Admin for the Staging or Production environment

<div class="bs-callout bs-callout-info" id="info" markdown="1">
This information is just the code portion for setting up your VCL. Use this information with [快速定制VCL片段]({{ page.baseurl }}/cloud/configure/cloud-vcl-custom-snippets.html).
</div>

## Create WordPress Edge Dictionary {#edge-dictionary}
Edge Dictionaries create key-value pairs for running against your VCL snippet. 例如， you may want to build a dictionary of URLs to redirect to a WordPress backend. You may only want to create the edge dictionary in your Production environment. You can also create it in Staging for testing if needed.

1. Log in to the Magento Admin.
2. Navigate to **Stores** > **Configuration** > **Advanced** > **System** > **Fastly Configuration**.
3. Expand the **Edge dictionaries** section.
4. Click **Add container**. You need to create a container to hold up to 1,000 key-value pairs.
5. On the container, enter a Dictionary name. For this example, use the name `wordpress_urls`.
6. Select the checkbox for **Activate after the change** if you want to the dictionary after creating or editing the container.
7. Add key-value pairs in the new dictionary. For this example, enter the URLs for your blog that should be redirected to your WordPress backend. Enter a value of 1.

For more information on using Edge Dictionaries with your VCL snippets, see Fastly's [Creating and using Edge Dictionaries](https://docs.fastly.com/guides/edge-dictionaries/creating-and-using-dictionaries){:target="_blank"} and their example [自定义VCL代码片段](https://docs.fastly.com/guides/edge-dictionaries/creating-and-using-dictionaries#custom-vcl-examples){:target="_blank"}.

## Create wordpress.json {#vcl}
For this example, you may only want to run it against the Production server. You can also add it to Staging for testing.

Create an `wordpress.json` file with the following JSON content:

{% highlight json %}
{
  "name": "wordpress",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( req.url.path ~ \"^\\/?([^:\/\\s]+).*$\" ) { if ( table.lookup(wordpress_urls, re.group.1, \"NOTFOUND\") != \"NOTFOUND\" ) { set req.http.X-WP = \"1\"; } }"
}
{% endhighlight %}

Review the following values for the code to determine if you need to make changes:

* `name`: Name for the VCL snippet. For this example, we used the name `wordpress`.
* `priority`: Determines the order VCL snippets call. You want to set the priority to 5 to immediately run and check for URLs that should be redirected. This priority runs the snippet immediately and before any of the uploaded and default Magento VCL snippets (magentomodule) that have a priority of 50.
* `type`: For this VCL, we use `recv`, which places it in the vcl_recv subroutine by below the boilerplate VCL and above any objects.
* `content`: The code that runs. The code extracts the first part `mypath` of the path `/mypath/someotherpath`.  It then compares that path against the Edge Dictionary `wordpress_urls`. If a match is found, the visitor is redirected to the Wordpress backend.

<div class="bs-callout bs-callout-info" id="info" markdown="1">
The default VCL snippets you uploaded included a prepended name of `magentomodule_` with a priority of 50. For your 自定义VCL代码片段, **do not use the `magentomodule_` name**. Also consider the priority of your custom snippets if they should override the default snippets.
</div>

## Configure WordPress {#wordpress}
For this VCL snippet to work, you also need to attach a condition to the WordPress backend to handle this request:

	req.http.X-WP == “1”


## Finish adding the VCL {#complete}
When saved, continue creating other VCLs. You can then run the bash script, then validate and activate your VCLs to complete the process. For complete steps, see [快速定制VCL片段]({{ page.baseurl }}/cloud/configure/cloud-vcl-custom-snippets.html).
