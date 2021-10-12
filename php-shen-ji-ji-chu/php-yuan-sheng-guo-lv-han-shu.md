# PHP原生过滤方法

### **过滤函数**

**escapeshellarg** 传入参数添加单引号并转义原有单引号 **用于防止命令注入**

例 传入 ' id # 处理后 '\\' id #' 处理后的字符串可安全的添加到命令执行参数

**escapeshellcmd** 转义字符串中的特殊符号 **用于防止命令注入**

反斜线（\）会在以下字符之前插入： \&#;\`|\*?\~<>^()\[]{}$\\, \x0A 和 \xFF。 ' 和 " 仅在不配对儿的时候被转义

_来自 <_[_https://www.php.net/manual/zh/function.escapeshellcmd.php_](https://www.php.net/manual/zh/function.escapeshellcmd.php)_>_

**addslashes** _在单引号（'）、双引号（"）、反斜线（\）与 NUL前加上反斜线_ **可用于防止SQL注入**

注意: **经过addslashes 处理后的字符串不可直接用于sql查询拼接 需要使用引号包裹后拼接到sql语句中 否则仍可导致sql注入**

**htmlspecialchars 和 htmlentities** 将特殊字符转义成html实体 可用于防止XSS

**intval($input) floatval() floatval() floor() (int)$input num+0** 将输入强制转换为整数/浮点 常见于防止SQL注入

### 防护配置项
