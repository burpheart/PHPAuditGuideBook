---
description: 将远程/本地作为PHP文件包含入当前执行的PHP源码并作为PHP代码执行
---

# 文件包含

## 例子

开发人员希望自己写的页面实现更加灵活的加载



```
<?php
$file = $_GET['page']; 
include(“pages/$file”);
?>
```

正常输入 ?page=login.php

服务器包含并执行pages目录下的login.php

攻击者输入 ?page=../image/123.jpg

服务器包含并执行pages的上层目录image目录下的123.jpg

该漏洞通常需要参数后半部分可控或者参数完全可控才存在

注意:当代码运行环境 php版本小于5.3.4且 php的magic_quotes_gpc为OFF状态时 参数在中间拼接也可利用  (CVE-2006-7243)(这是个PHP本身的问题 不是代码的问题 解决方法: 升级PHP)

参数在中间拼接时 如果用户仍可向拼接出的文件进行写入则可以利用

如 include(“pages/$file.tpl”);  

架设用户不能上传php文件 但可上传tpl文件

可以上传一个tpl文件 构造路径包含tpl文件 执行php代码

##

| 函数/语法结构      | 描述                               | 例子                                |
| ------------ | -------------------------------- | --------------------------------- |
| include      | 包含并运行指定文件 执行出错会抛出错误              | include 'vars.php'; (括号可有可无)      |
| require      | 同include 执行出错会抛出警告               | require('somefile.php'); (括号可有可无) |
| require_once | 同require 但会检查之前是否已经包含该文件 确保不重复包含 |                                   |
| include_once | 同include 但会检查之前是否已经包含该文件 确保不重复包含 |                                   |

