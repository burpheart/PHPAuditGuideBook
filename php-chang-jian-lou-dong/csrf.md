---
description: 跨站请求伪造
---

# CSRF

### 表单请求

**攻击者使被害者的浏览器在用户不知情的情况下发起目标网站表单请求 **这些表单常常带有目标网站的用户cookies 可以以用户在目标网站的身份进行操作 (攻击者不能获取cookies)

**检查鉴权后的操作是否添加token/Referrer校验 拒绝空Referrer**

### JSONP请求

除了表单常见的还有jsonp请求 服务器返回一段带有函数调用的json 浏览器把jsonp页面当做js加载执行 调用回调函数将数据传入函数 用于浏览器从服务器动态获取信息 由于js等静态资源调用浏览器默认放行 造成了风险

(get表单也可以使用这种方式发起请求 但是无法获取服务器返回的内容)

可获取用户登陆后才能获取的信息  比如登陆用户个人资料 账户余额 等

**检查Referrer 拒绝空Referrer**

### AJAX请求

**一种使用js动态加载数据的技术**

浏览器会先发送一个HEAD请求 获取HTTP头 检查Access-Control-Allow-Origin等Access-Control安全策略

这会决定是否发起带有目标域浏览器cookies的请求 如果没有头或不符合策略则拒绝请求

**审计时检查 HTTP是否错误地添加"Access-Control-Allow-Origin:\*" 头**

### 防护方法

添加随机token 在表单/jsonp请求时附加token(非常有效)

服务端检测 Referrer (<mark style="color:red;">**一定要拒绝空Referrer**</mark>** **html表单可以发起空referrer)(表单/静态资源引用/jsonp请求)

如果使用正则匹配一定要检查正则是否可以被绕过

服务器返回Access-Control-Allow-Origin 头 (表单/静态资源引用/jsonp请求无效 仅AJAX请求)(<mark style="color:red;">一定不要设置成 \*</mark>)







###



