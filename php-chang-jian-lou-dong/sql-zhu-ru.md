# SQL注入

将处理不当的用户输入拼接到数据库将要执行的SQL语句中 导致攻击者可以修改原有执行的SQL语句

### 例子

```

<?php
include('conn.php');//数据库连接省略
$sql = "SELECT id, name FROM users WHERE id=$_GET['id']";
$result = $mysqli->query($sql);
if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        echo "id: " . $row["id"]. " - Name: " . $row["name"];
    }
} else {
    echo "没有查询到结果";
}
?>

```

正常请求 ?id=123

执行SQL 

```
SELECT id, name FROM users WHERE id=123;
```

攻击者构造请求: ?id=**123 UNION SELECT name,password FROM users;**

**执行SQL**

```
SELECT id, name FROM users WHERE id=123 UNION SELECT name,password FROM users;
```

攻击者改变了原有的SQL语句逻辑



### 常见过滤/防护

**addslashes **_在单引号（'）、双引号（"）、反斜线（\）与 NUL前加上反斜线_ **可用于防止SQL注入**

**mysqli::real_escape_string mysqli::escape_string mysqli_real_escape_string mysql_real_escape_string SQLite3::escapeString **

**以上函数会在\x00(NULL), \n, \r, , ', " 和 \x1a (CTRL-Z)**_**前加上反斜线**_**  并考虑了当前数据库连接字符集进行处理**

注意: <mark style="color:red;"></mark><mark style="color:red;">**经过以上函数处理后的字符串不可直接用于sql查询拼接 需要使用引号包裹后拼接到sql语句中 否则仍可导致sql注入 **</mark>

<mark style="color:red;">**例如 上文中的例子 攻击者输入并没有使用到引号反斜线 逗号可使用其他方法绕过 仍可构成SQL注入**</mark>

```

<?php
/*强制类型转换*/
$id=intval($_GET['id']); //因查询ID为整数 所以可以强制转换为整数
/*转义特殊字符 加上引号 (字符串类型)*/
$id=$pdo->quote($_GET['name']);
/*预处理语句*/
$stmt =$pdo->prepare("SELECT id, name FROM users WHERE id=?;");
$stmt->execute([$_GET['id']]);//简单的预处理 完整使用方法见PHP手册
?>


```

**PDO::quote 转义特殊字符 并添加引号**

**PDO::prepare 预处理SQL语句 有效防止SQL注入 (推荐)**

**intval($input) floatval() floatval() floor() (int)$input num+0** 

将输入强制转换为整数/浮点 用于整数/浮点类型的输入参数处理 可防止SQL注入



#### 一些执行SQL语句的函数

| 函数/方法                                                                                                                                                              | 备注  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --- |
| mysql_query                                                                                                                                                        |     |
| odbc_exec                                                                                                                                                          |     |
| mysqli_query                                                                                                                                                       |     |
| mysql_db_query                                                                                                                                                     |     |
| mysql_unbuffered_query                                                                                                                                             |     |
| <p>mysqli::query</p><p>用法</p><p>$mysqli = new mysqli("localhost", "my_user", "my_password", "world");</p><p>$mysqli->query();</p>                                  |     |
| pg_query                                                                                                                                                           |     |
| pg_query_params                                                                                                                                                    |     |
| pg_send_query                                                                                                                                                      |     |
| pg_send_query_params                                                                                                                                               |     |
| sqlsrv_query                                                                                                                                                       |     |
| <p>pdo::query</p><p>$pdo=new PDO("mysql:host=localhost;dbname=phpdemo","root","1234"); $pdo->query($sql);</p>                                                      | PDO |
| <p>SQLite3::query</p><p>SQLite3::exec</p><p>$db = new SQLite3('mysqlitedb.db'); $db->query('SELECT bar FROM foo'); $db->exec('CREATE TABLE bar (bar STRING)');</p> |     |
