# 文件包含

将远程/本地文件 包含入当前页面的PHP代码并执行 详细加载执行原理见[PHP7内核剖析](https://www.kancloud.cn/nickbai/php7/363301)

## 例子

开发人员希望自己写的页面实现更加灵活的加载

```
<?php
$file = $_GET['page']; 
include(“pages/$file”);
?>
```

正常输入 ?page=login.php

```
<?php
$file = $_GET['page']; 
/*
pages/login.php 文件代码被包含执行
*/
?>
```

服务器包含并执行pages目录下的login.php

攻击者输入 ?page=../image/123.jpg

服务器包含并执行pages的上层目录image目录下的123.jpg

该漏洞通常需要参数后半部分可控或者参数完全可控才存在

注意:当代码运行环境 php版本小于5.3.4且 php的magic\_quotes\_gpc为OFF状态时 参数在中间拼接也可利用  (**CVE-2006-7243**)(这是个PHP本身的问题 不是代码的问题 解决方法: 升级PHP)

参数在中间拼接时 如果用户仍可向拼接出的文件进行写入则可以利用

如 include(“pages/$file.tpl”); &#x20;

假设用户不能上传php文件 但可上传tpl文件

可以上传一个tpl文件 构造路径包含tpl文件 执行php代码

### 文件包含利用方法

**包含上传文件** (上传头像图片等)

**包含 data:// php://filter 或 php://input 伪协议** (php.ini allow\_url\_include 设置为 on)

**包含日志** Apache nginx 等web服务器访问日志 SSH FTP 等登陆错误日志 PHP框架日志&#x20;

**包含 /proc/self/environ** (必须是有proc伪文件系统的操作系统 比如LINUX) 当前进程的环境变量(PHP会将HTTP头 请求URI等信息写入当前进程环境变量)

**包含 session文件 ** (通常在临时目录下 (linux /tmp/ ) sess\_会话ID文件)

**PHP间接或直接创建的其他文件 **比如数据库文件 缓存文件 应用日志等

| 函数/语法结构       | 描述                               | 例子                                |
| ------------- | -------------------------------- | --------------------------------- |
| include       | 包含并运行指定文件 执行出错会抛出错误              | include 'vars.php'; (括号可有可无)      |
| require       | 同include 执行出错会抛出警告               | require('somefile.php'); (括号可有可无) |
| require\_once | 同require 但会检查之前是否已经包含该文件 确保不重复包含 |                                   |
| include\_once | 同include 但会检查之前是否已经包含该文件 确保不重复包含 |                                   |

