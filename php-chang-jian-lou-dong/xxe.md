---
description: XML外部实体(注入) 攻击者利用xml的性质可以获取本地/远程文件内容 (不同于其他语言 PHP中xml实体可以使用PHP伪协议)
---

# XXE

XML外部实体是XML的一个特性 XML可以使用外部实体引用来包含和解析其他文档

当然XML还有其他实体 详细内容可以参考[这个DTD教程](https://www.yiibai.com/dtd/dtd\_entities.html)

这里就不详细将利用技巧了

审计时如果发现使用了文末列表的函数 就要检查是否禁用了外部实体

<mark style="color:red;">**libxml\_disable\_entity\_loader(true);  //禁用外部实体使用到的函数 参数为true时禁用**</mark>

<mark style="color:red;">**注意: **</mark>php环境中libxml 版本>=2.9.0时外部实体默认禁用 (<mark style="color:red;">**PHP版本 >=8.0时 就开始使用>=2.9.0版本的libxml **</mark>且<mark style="color:red;">**libxml\_disable\_entity\_loader函数被完全废弃 使用该函数会抛出错误**</mark>)

漏洞常见处: 支付等回调api

| 函数                                 | 描述            |                                                                                                                                                                             |
| ---------------------------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>DOMDocument::</p><p>loadXML</p> | 加载解析XML       | <p>&#x3C;?php $xml=file_get_contents('php://input');</p><p>$dom=new DOMDocument(); $dom->loadXML($xml); $xml=simplexml_import_dom($dom); $xxe=$xml->xxe; echo $xxe; ?> </p> |
| simplexml\_load\_string            | 加载解析XML字符串    | $xml=simplexml\_load\_string($\_REQUEST\['xml']); print\_r($xml);                                                                                                           |
| simplexml\_load\_file              | 读取文件作为XML文档解析 | simplexml\_load\_file("1.xml")                                                                                                                                              |
