---
description: 让用户浏览器执行到攻击者指定的JS脚本代码
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

浏览器渲染纯文本 Hello cz! 

```
攻击者输入: ?name=<script type="text/javascript">alert('XSS!');</script>
服务器返回 Hello <script type="text/javascript">alert('XSS!');</script>!
浏览器渲染 Hello !  script被作为html标签解析 执行其中的代码 弹出警告框XSS!
```

此种漏洞比较明显 很容易分析问题的存在

**审计时注意 PHP常使用 htmlspecialchars 和 htmlentities函数 转义用户的输入作为防护 **

### 储存型XSS

将服务器储存的处理不当的用户输入输出到网页 导致用户浏览器执行恶意代码

攻击者输入->服务器储存 攻击者得到一个返回储存值的页面

被害者请求页面->服务器调用储存并输出->XSS

常见于评论 留言 文章 等

该漏洞需要同时联合查看储存与输出 有时业务复杂 多写入点 多输出点 不易发现

比如 发布评论 攻击者发布带有恶意代码的评论 被害者访问评论展示页面 触发XSS 后台管理员审核评论时 触发XSS

再比如 用户系统设置昵称时 攻击者将昵称写入数据库 在评论显示时读取数据库值输出用户昵称



#### DOM型 XSS

####  DOM型 XSS 只与浏览器前端DOM渲染有关 不做赘述



