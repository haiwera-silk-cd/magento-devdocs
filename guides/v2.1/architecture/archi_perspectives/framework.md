---
group: arch-guide
subgroup: Logical View
title: Magento框架
menu_title: Magento框架
menu_order: 4
version: 2.1
github_link: architecture/archi_perspectives/framework.md
redirect_from: /guides/v1.0/architecture/archi_perspectives/framework.html
---

## 概述

Magento框架控制应用程序组件如何交互，包括请求流程，路由，索引，缓存和{% glossarytooltip 53da11f1-d0b8-4a7e-b078-1e099462b409 %}exception{% endglossarytooltip %}处理。它提供了为创建包含业务逻辑的模块减少努力的服务。贡献了使Magento代码更加模块化以及减少依赖的目标。

主要的{% glossarytooltip bf703ab1-ca4b-48f9-b2b7-16a81fd46e02 %}PHP{% endglossarytooltip %}软件组件被组织成叫作<i>库</i>逻辑组，所有的模块都可以调用。多数框架代码放置于{% glossarytooltip 41aee03b-a5d5-49c2-8839-894090ef4e86 %}领域{% endglossarytooltip %}层，或围住表示层、服务层及领域层。框架不包含业务逻辑。
虽然Magento框架不包含资源模型，但它包含一个代码{% glossarytooltip 08968dbb-2eeb-45c7-ae95-ffca228a7575 %}库{% endglossarytooltip %}来帮助实现资源模型。

<div class="bs-callout bs-callout-info" id="info">
  <p>不要混淆Magento框架和承载Magento的Zend应用框架</p>
</div>

你不应该修改框架的文件，虽然如果你正在扩展Magento,你必须知道如何调用Magento的库，典型地，你创建的模块将从框架目录中定义的类和接口继承。

## 职责

Magento框架提供帮助你减少创建包含业务逻辑的模块努力的库。

框架对潜在所有的模块有用的操作进行响应，包括：

* 处理HTTP协议

* 数据库和文件系统的交互

* 渲染内容

## 组织

这是Magento的文件结构：

<pre>
vendor/
    ../magento
        ../framework
lib/
    ../internal
        ../LinLibertineFont
    ../web
 </pre>

* `/vendor/magento/framework`目录仅包含PHP代码。它们是代码库加上路由请求到模块(依次调用框架库)的应用程序入口点。例如，框架库帮助实现一个资源模型(基类和接口从这里继承)，但不是资源模型本身。某些库也支持{% glossarytooltip 6c5cb4e9-9197-46f2-ba79-6147d9bfe66d %}CSS{% endglossarytooltip %}渲染。

* `/lib/internal` 包含一些非PHP及PHP组件。非PHP框架库包含{% glossarytooltip 312b4baf-15f7-4968-944e-c814d53de218 %}JavaScript{% endglossarytooltip %}和LESS/CSS

* `/lib/web` 包含JavaScript和CSS/LESS文件。这些文件存在在`web`而不是`internal`，因为它们是web浏览器可访问的。而`internal`下的PHP代码则可以。(任何浏览器需要访问的代码都应放在`web`下，而其它的放到`internal`下)

<div class="bs-callout bs-callout-info" id="info">
  <p><code>vendor/magento/framework</code>目录映射<code>Magento\Framework</code> {% glossarytooltip 621ef86b-7314-4fbc-a80d-ab7fa45a27cb %}命名空间{% endglossarytooltip %}.</p>
</div>

## Magento框架的亮点

Magento框架(`lib/internal/Magento/Framework/`)提供了一系列稳健的功能。如果你是一个{% glossarytooltip 55774db9-bf9d-40f3-83db-b10cc5ae3b68 %}扩展{% endglossarytooltip %}开发者，你可能对这个框架的命名空间子集感兴趣。

<table>
   <tbody>
      <tr style="background-color: lightgray">
         <th>命名空间</th>
         <th>目的</th>
      </tr>
      <tr>
         <td><code>Magento\Framework\DataObject</code>
         </td>
         <td>提供存储和通过魔术方法接收数据的标准功能。</td>
      </tr><tr>
         <td><code>Magento\Framework\DataObject\Model</code>
         </td>
         <td>包含几乎所有Magento模型类要继承的基础模型类</td>
      </tr><tr>
         <td><code>Magento\Framework\DataObject\AbstractModel</code>
         </td>
         <td></td>
      </tr>
      <tr>
         <td><code>Magento\Framework\DataObject\AbstractResource</code></td>
         <td></td>
      </tr>
      <tr>
         <td><code>Magento\Framework\DataObject\Controller</code></td>
         <td>包含帮助返回不同类型结果集的所有类（例如，JSON或直接返回）</td>
      </tr>
      <tr>
         <td><code>Magento\Framework\DataObject\View</code></td>
         <td>包含渲染页面和布局的代码</td>
      </tr><tr>
         <td><code>Magento\Framework\DataObject\Data</code></td>
         <td>包含处理表单的额外类</td>
      </tr><tr>
         <td><code>Magento\Framework\DataObject\URL</code></td>
         <td>包含查找Magento其它页的代码</td>
      </tr>
   </tbody>
</table>

其它在`Magento\Framework`下的命名空间将引起扩展开发者的兴趣：

<table>
    <tbody>
        <tr style="background-color: lightgray">
            <th>命名空间</th>
            <th>目的</th>
        </tr>
      <tr>
         <td><code>Magento\Framework\ObjectManager</code>
         </td>
         <td>被用于提供<i>依赖注入</i> </td>
      </tr>
	  <tr>
         <td><code>Magento\Framework\App</code>
         </td>
         <td>包含知道Magento应用程序信息的框架代码。此代码引导应用程序且读取初始化配置。它也包含命令行工具、网页应用程序、定时任务的入口点。最终，它提供布署上下文环境(诸如读取数据库、语言、缓存系统的配置)路由请求。
</td>
</tr>
<tr>
	<td>
		<code>Magento\Framework\Api</code>
	</td>
	<td>包含通过系统可扩展的对象的高级功能的基类(即，对象可以通过Magento市场的扩展扩展添加新数据的)</td>
</tr>
<tr>
	<td>
		<code>Magento\Framework\Config</code>
	</td>
	<td>包含一般配置读取器，每个配置文件有自己特定的从这些类继承的读取器。</td>
</tr>
<tr>
	<td>
		<code>Magento\Framework\Filesystem</code>
	</td>
	<td>包含处理读取和写入文件系统的类</td>
</tr>
	<tr>
		<td>
			<code>Magento\Framework\HTTP\PhpEnvironment</code>
		</td>
		<td/>
	</tr>
	<tr>
		<td>
			<code>Magento\Framework\Session</code>
		</td>
		<td/>
	</tr>
	<tr>
		<td>
			<code>Magento\Framework\Stdlib\Cookie</code>
		</td>
		<td>处理HTTP请求/响应以及SESSION/COOKIE的代码</td>
	</tr>
	<tr>
		<td>
			<code>Magento\Framework\Exception</code>
		</td>
		<td>Contains the basic exceptions that are thrown throughout the Magento codebase.</td>
	</tr>
	<tr>
		<td>
			<code>Magento\Framework\Event</code>
		</td>
		<td>Contains the code that publishes synchronous events and that handles observers for any Magento event is handled here.
		</td>
	</tr>
		<tr>
			<td>
				<code>Magento\Framework\Validator</code>
			</td>
			<td>包含验证数据(货币校验，非空校验)的代码及处理任何Magento的事件观察者的代码。
			</td>
		</tr>
	</tbody>
</table>
