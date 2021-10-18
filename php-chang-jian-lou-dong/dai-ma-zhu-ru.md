# 代码注入

将用户输入拼接到PHP代码中执行 导致的任意代码执行问题

### 例子

有些特殊业务使用了eval等代码执行函数

```
<?php eval( 'echo ('.$_GET['a'].');'); //计算器?>
```

正常输入: ?a=9\*9

服务器执行 echo (9\*9);

输出:81

攻击者输入?a=system('whoami')

服务器执行echo (system('whoami'));

成功调用system函数执行命令

实际业务中要尽量避免使用eval这种动态执行代码方法 必要使用时做好过滤



| 函数/语法结构              | 描述                                             | 例子                                                             |
| -------------------- | ---------------------------------------------- | -------------------------------------------------------------- |
| eval                 | 将传入的参数内容作为PHP代码执行 eval 不是函数 是一种语法结构 不能当做函数动态调用 | eval('phpinfo();');                                            |
| assert               | 将传入的参数内容作为PHP代码执行 版本在PHP7以下是函数 PHP7及以上为语法结构    | assert('phpinfo();');                                          |
| preg_replace         | 当preg_replace使用/e修饰符且原字符串可控时时 有可能执行php代码       | echo preg_replace("/e","{${PHPINFO()}}","123");                |
| call_user_func       | 把第一个参数作为回调函数调用 需要两个参数都完全可控才可利用 只能传入一个参数调用      | call_user_func('assert', 'phpinfo();');                        |
| call_user_func_array | 同call_user_func 可传入一个数组带入多个参数调用函数              | call_user_func_array ('file_put_contents', \['1.txt','6666']); |
| create_function      | 根据传递的参数创建匿名函数，并为其返回唯一名称 利用需要第二个参数可控 且创建的函数被执行  | $f = create_function('','system($\_GET\[123]);'); $f();        |

