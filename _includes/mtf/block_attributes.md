<div markdown="1">

See the `block` node attributes details in the following table:

|`block` attribute | 描述 | Is required|Values| Example|
|---|---|---|---|---|
|`name`| Name of the block| Required|Unique in the page. The method to get the block class instance is generated using this value.|`widgetGrid`|
|`class`| Full name of the block class |必需| Class name |`Magento\Widget\Test\Block\Adminhtml\Widget\WidgetGrid` |
|`locator`| CSS selector or XPath locator of the block|必需|[CSS Selectors](http://www.w3.org/TR/selectors/), <a href="http://www.w3.org/TR/xpath-31/">XPath</a>|CSS: `#widgetInstanceGrid`, XPath: `//*[@id="widgetInstanceGrid"]`|
|`strategy` |Selector strategy| Required|`css selector`或`xpath`| `css selector`|

</div>