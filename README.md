# PHP代码审计入门指南
https://www.yuque.com/burpheart/phpaudit

### 作者

白帽酱 (橙子酱)(i@rce.moe)

### 简介

这本指南包含了我在学习过程中整理出的一些技巧和对漏洞的一些理解

这本指南仍在在编写完善中

如果发现有遗漏或者是错误的地方 欢迎大家提issue


## 目录:
* [PHP代码审计入门指南](https://www.yuque.com/burpheart/phpaudit/readme)
* [序言](https://www.yuque.com/burpheart/phpaudit/xu-yan)
* PHP审计基础
  * [⚒ 工具准备](https://www.yuque.com/burpheart/phpaudit/php-shen-ji-ji-chu_gong-ju-zhun-bei)
  * [PHP代码审计思路](https://www.yuque.com/burpheart/phpaudit/php-shen-ji-ji-chu_php-shen-ji-liu-cheng)
  * [VS CODE 常用快捷键](https://www.yuque.com/burpheart/phpaudit/php-shen-ji-ji-chu_vs-code-shen-ji-ji-qiao)
  * [💉 PHP用户可控输入速查表](https://www.yuque.com/burpheart/phpaudit/php-shen-ji-ji-chu_yong-hu-ke-kong-shu-ru-su-cha-biao)
  * [🧬 PHP敏感函数速查表](https://www.yuque.com/burpheart/phpaudit/php-shen-ji-ji-chu_cui-ruo-han-shu-su-cha-biao)
  * [🩹 PHP原生过滤方法](https://www.yuque.com/burpheart/phpaudit/php-shen-ji-ji-chu_php-yuan-sheng-guo-lv-han-shu)
  * [PHP动态调试-Xdebug安装配置](https://www.yuque.com/burpheart/phpaudit/php-shen-ji-ji-chu_php-dong-tai-tiao-shi-xdebug-an-zhuang-pei-zhi)
* PHP常见漏洞
  * [命令注入](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_page-11)
  * [代码注入](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_dai-ma-zhu-ru)
  * [文件包含](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_wen-jian-bao-han)
  * [SQL注入](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_sql-zhu-ru)
  * [文件操作](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_wen-jian-cao-zuo)
  * [XSS](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_xss)
  * [SSRF](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_ssrf)
  * [CSRF](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_csrf)
  * [XXE](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_xxe)
  * [反序列化](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_fan-xu-lie-hua)
  * [LDAP注入](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_ldap-zhu-ru)
  * [其他漏洞](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-lou-dong_qi-ta-lou-dong)
* PHP常见框架
  * [TODO]
  * [Thinkphp](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-kuang-jia_page-2)
  * [Laravel](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-kuang-jia_laravel)
  * [Codeigniter](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-kuang-jia_codeigniter)
  * [Yii](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-kuang-jia_yii)
  * [Cakephp](https://www.yuque.com/burpheart/phpaudit/php-chang-jian-kuang-jia_cakephp)
* PHP审计实例
  * [TODO]
* PHP特性利用
  * [TODO]
* PHP审计扩展
  * [PHP商业源码提取](https://www.yuque.com/burpheart/phpaudit/kau3lk)
  * [浅谈PHP源代码保护方案&受保护PHP代码の解密还原](https://www.yuque.com/burpheart/phpaudit/mzbi3y)

* 附录
  * [changelog](https://www.yuque.com/burpheart/phpaudit/tbdum5)
  * [PHP弱类型](https://www.yuque.com/burpheart/phpaudit/fu-lu_php-ruo-lei-xing)

  * [扩展阅读](https://www.yuque.com/burpheart/phpaudit/xg1xrk)
  * [🎉 总结](https://www.yuque.com/burpheart/phpaudit/zong-jie)
  * [🔗 参考](https://www.yuque.com/burpheart/phpaudit/can-kao)


# changelog
## 2021-12-12 
1. 弃用gitbook 改用语雀
2. 补充 其他漏洞 页面  小幅度修整页面格式

## 2021-12-20
1. 文件操作 函数补充
2. 增加扩展阅读页面
3. 增加PHP源码解密

## 2021-12-28
PHP源码解密页面完成

## 2022-03-10
补充其他漏洞
