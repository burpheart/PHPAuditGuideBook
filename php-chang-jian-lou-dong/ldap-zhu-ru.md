# LDAP注入

ldap的注入是ldap搜索过滤器的注入

审计时可以搜索ldap\_search 函数判断第三个参数是否可控

检查是否正确转义了特殊符号

```
 '" \/ \\ 空格  # <> , ; + * () \x00(null)
```

将以上字符转换成ascii码值 在其前面加上反斜线

只转义以下这6个字符就足以防止常见的ldap注入

```
* \ ( ) \x00
```

```
function ldapspecialchars($string) {
    $sanitized=array('\\' => '\5c',
                     '*' => '\2a',
                     '(' => '\28',
                     ')' => '\29',
                     "\x00" => '\00');
    return str_replace(array_keys($sanitized),array_values($sanitized),$string);
}
```

ldap过滤函数代码来自 [Pino\_HD【LDAP】LDAP注入漏洞与防御 \[2017.09.27\]](https://www.jianshu.com/p/d94673be9ed0)

如果想要详细了解利用及原理可以参考文章 [ldap注入入门学习](https://damit5.com/2019/08/05/LDAP%E6%B3%A8%E5%85%A5%E5%85%A5%E9%97%A8%E5%AD%A6%E4%B9%A0/)

```

ldap_bind($ds, "cn=".$username.",".$ldap, $passwd);//绑定ldap区域(相当于登陆ldap服务器)
$ds=ldap_connect($ldapSrv,$port);//建立ldap连接
if($ds) {
    $r=ldap_bind($ds, "cn=".$username.",".$dn, $passwd);/绑定ldap区域(相当于登陆ldap服务器)
    if($r) {
        $sr=ldap_search($ds, $dn, "(|(cn=".$_GET["user"].")(mail=".$_GET["user"]."))");//在ldap中使用过滤器搜索
        $info = ldap_get_entries($ds, $sr);
        if($info["count"]==0){
        	die('用户不存在');
        }
        if($info[0]["userpassword"][0]==$_GET["pass"]){
        die('登陆成功');
        }else{
        die('密码错误');
        }
        ldap_close($ds);
        } else {
            echo "Unable to connect to LDAP server.";
        }        
    }
```

ldap过滤器结构表

```
    Fileter = (filtercomp)
    Filtercomp = and / or / not / item
    And = & filterlist
    Or = | filterlist
    Not = ! filter
    Filterlist = 1*filter
    Item = simple / present / substring
    Simple = “=” / “~=” / ”>=” / “<=”
    Present = attr =*
    Substring = attr “=” [initial]*[final]
    Initial = assertion value
    Final = assertion value
```
