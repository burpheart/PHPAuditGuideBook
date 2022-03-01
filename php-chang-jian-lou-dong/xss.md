---
description: 跨站脚本(攻击) 让用户浏览器执行到攻击者指定的JS脚本代码
---

# XSS

### 反射型XSS

反射型XSS是服务器后端处理时把处理不当的用户输入输出到网页 导致用户浏览器执行恶意代码

```
<?php
echo 'Hello '.$_GET['name'].'!';
```

正常输入: ?name=cz

服务器返回 Hello cz!

浏览器渲染纯文本 Hello cz!&#x20;

```
攻击者输入: ?name=<script type="text/javascript">alert('XSS!');</script>
服务器返回 Hello <script type="text/javascript">alert('XSS!');</script>!
浏览器渲染 Hello !  script被作为html标签解析 执行其中的代码 弹出警告框XSS!
```

此种漏洞比较明显 很容易分析问题的存在

**审计时注意 PHP常使用 htmlspecialchars 和 htmlentities函数 转义用户的输入作为防护**&#x20;

### 储存型XSS

将服务器储存的处理不当的用户输入输出到网页 导致用户浏览器执行恶意代码

攻击者输入->服务器储存 攻击者得到一个返回储存值的页面

被害者请求页面->服务器调用储存并输出->XSS

常见于评论 留言 文章 等

该漏洞需要同时联合查看储存与输出 有时业务复杂 多写入点 多输出点 不易发现

比如 发布评论 攻击者发布带有恶意代码的评论 被害者访问评论展示页面 触发XSS 后台管理员审核评论时 触发XSS

再比如 用户系统设置昵称时 攻击者将昵称写入数据库 在评论显示时读取数据库值输出用户昵称



#### DOM型 XSS

纯dom

储存(反射)dom

#### &#x20;DOM型 XSS 只与浏览器前端DOM渲染有关 不做赘述

### 前端外部文件引用

攻击者修改前端引用的文件链接 引用外部网站文件

常见于用户头像 文章/评论图片等

被害者访问到攻击者个人页面 文章 评论 聊天内容时会访问远程图片文件

这可能会使攻击者获取到访问者的ip 浏览器 系统等信息

也可以绕过内容审查 在审查通过后动态替换文件内容(hsbc广告等信息)

解决方法:正则匹配限制url域名

### 防护

后端过滤

服务端返回HTTP头 添加内容安全策略 [content-security-policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Security-Policy) 头

正确设置安全策略可以有效减少**未知XSS/html外部文件引用**漏洞产生的危害

COOKIES添加Httponly属性 防止使用js读取用户cookies (js发起表单仍可携带cookies)



