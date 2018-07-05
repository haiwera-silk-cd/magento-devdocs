---
group: b2b
subgroup: 10_REST
title: 与NegotiableQuote模块集成
menu_title: 与NegotiableQuote模块集成
menu_order: 31
version: 2.2
ee_only: True
level3_menu_node: level3child
level3_subgroup: nq
github_link: b2b/negotiable-quote.md
functional_areas:
  - B2B
  - Integration
---

议价是一种允许公司用户(购买者)在发起订单前和销售者(管理员用户)商议产品和物流价格的一种机制，它的功能只对公司有效。

议价的生命周期包含几个阶段，如下图所示

![议价工作流程]({{ page.baseurl }}/b2b/images/quote-workflow.jpg)

议价处理自身可以是一个持续的过程，过程中有几个流程可重复，一直到接受为止。

* 购买者创建并提交议价
* 销售者浏览并修改或拒绝此报价。
* 购买者查看销售者给的实际折扣
* 经同意，购买者开始结算过程并且系统将议价转换为订单

<div class="bs-callout bs-callout-info" id="info" markdown="1">
你不能商议自身产品项的价格。
</div>

## 报价状态

报价的生命周期由报价的状态管理，报价接口允许销售者和购买者管理管理报价中的产品项(添加、删除、修改数量)以及给定产品项及物流的可卖价(或可买价)

被商议的价格设置在议价中，是准确的价格，在结算、订单生成和发票生成期间它将作为报价

<table>
<tr>
<th>状态</th><th>描述</th><th>销售者可用的动作</th></tr>
<tr>
<td>已创建</td>
<td><p>购买者提交了一个报价，但销售者还没有打开它，购买者仍能修改</p>
<p>系统创建一条他的报价记录</p>
 </td>
<td>查看</td>
</tr>

<tr>
<td>Open </td>
<td>购买者已经打开了提交的报价，并审查/修改了它，此时销售者能修改，但购买者不能	 </td>
<td><p>浏览、提交、拒绝，保存为草案</p>
<p>修改过期日期，产品项的数量，添加/移除产品项，输入一个想要的价格，添加物流方式和物流价格及添加评论。</p> </td>
</tr>

<tr>
<td>已提交<td>
<td>销售者已经审查了报价并将其发送回给了购买者。此时销售者不能修改。</td>
<td>查看</td>
</tr>

<tr>
<td>客户已查看 </td>
<td>购买者已经打开了销售者提交报价，并正在修改它，修改项或添加物流地址。此时销售者不能修改此报价 </td>
<td>查看</td>
</tr>

<tr>
<td>已更新<td>
<td>购买者重新提交报价到销售者，此时销售者可以修改，但购买者不能</td>
<td><p>浏览、提交、拒绝，保存为草案</p>
<p>修改过期日期，产品项的数量，添加/移除产品项，输入一个想要的价格，添加物流方式和物流价格及添加评论。</p></td>
</tr>

<tr>
<td>已下单</td>
<td>购买者已经购买了报价，并且Magento将此报价转换为了订单 </td>
<td>查看</td>
</tr>

<tr>
<td>已关闭</td>
<td><p>购买者取消了报价且他们停止了商议过程，此时双方者不能再修改此报价。</p><p>购买者在报价详情页点击 <b>Close</b> 按钮(不能用Web API) </p></td>
<td>查看</td>
</tr>

<tr>
<td>已拒绝</td>
<td>销售者拒绝了报价，所有的客户出价从报价中移除。在管理面板，报价被编辑锁锁定 </td>
<td>查看</td>
</tr>

<tr>
<td>已过期</td>
<td>报价处在购买者方，并且报价超过了过期时间</td>
<td>查看</td>
</tr>
</table>

下面的表格映射了Magento系统的内部状态和前台与管理面板显示状态的对应关系

系统状态 |购买者状态 | 销售者状态
--- | --- | ---
已创建 | 已提交 | New
客户处理中 | 已打开 | 客户已查看
管理员处理中 | Pending | 已打开
客户已提交 | 已提交 | 已更新
管理员已提交 | 已更新 | 已提交
已下单 | 已下单 | Ordered
已过期 | 已过期 | 已过期 
已拒绝 | 已拒绝 | 已拒绝
已关闭 | 已关闭 | 已关闭

下面的图从状态的角度展示了议价的生命周期

![议价状态]({{ page.baseurl }}/b2b/images/quote-statuses.png)

## 相关信息

* [管理协商报价]({{ page.baseurl }}/b2b/negotiable-manage.html)
* [更新协商报价]({{ page.baseurl }}/b2b/negotiable-update.html)
* [协商报价结算]({{ page.baseurl }}/b2b/negotiable-checkout.html)
* [生成协商报价订单]({{ page.baseurl }}/b2b/negotiable-order-workflow.html)
