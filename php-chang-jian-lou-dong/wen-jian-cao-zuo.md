# 文件操作

文件操作相关关键参数用户可控 导致文件/目录 删除/移动/写入(上传)/读取等

### 文件/目录删除

```
unlink(文件路径)//删除文件
rmdir(文件夹路径)//删除目录
```

**攻击者常见用法**

删除lock文件(解除重复程序安装保护等安全限制)

删除网站关键文件(导致网站拒绝服务 数据丢失)

### 文件写入/上传

```
文件写入
file_put_contents(路径,写入字符串);//直接将字符串写入文件(不存在会自动创建)

$fp = fopen(文件路径, "w");//以写入模式打开一个文件 返回文件指针(不存在会自动创建)
fwrite($fp,写入字符串);//写入数据
fclose($fp);//关闭文件
文件上传
move_uploaded_file(临时上传文件路径,目标文件路径);//移动临时上传文件
```

[php的原生文件上传 ](https://www.php.net/manual/en/features.file-upload.post-method.php)收到POST表单->随机文件名写入临时目录->执行PHP文件处理逻辑->移动临时文件到保存位置->自动删除临时文件(如果临时文件没有被移动)

临时文件路径必须是php上传表单自动处理产生的 例如 $\_FILES\["pictures"]\["tmp_name"]

"pictures"为表单中的name "tmp_name"为固定变量名(临时文件名)

**注:**只要PHP收到POST上传文件表单 哪怕php页面一行代码没有 都会将上传文件保存到临时目录 在请求结束后如果临时文件没有被移走就会被自动删除





文件写入/上传

| 函数                                                               | 描述                                                                           | 例子                                                                                                     |
| ---------------------------------------------------------------- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| file_put_contents                                                | 将一个字符串写入文件                                                                   | file_put_contents("1.txt","6666");                                                                     |
| move_uploaded_file                                               | 将上传的临时文件移动到新的位置                                                              | move_uploaded_file($\_FILES\["pictures"]\["tmp_name"],"1.php")                                         |
| rename                                                           | 重命名文件/目录                                                                     | rename($oldname, $newname);                                                                            |
| rmdir                                                            | 删除目录                                                                         |                                                                                                        |
| mkdir                                                            | 创建目录                                                                         |                                                                                                        |
| unlink                                                           | 删除文件                                                                         |                                                                                                        |
| copy                                                             | 复制文件                                                                         | copy($file, $newfile);                                                                                 |
| fopen/fputs/fwrite                                               | 打开文件或者 URL                                                                   | [https://www.php.net/manual/zh/function.fwrite.php](https://www.php.net/manual/zh/function.fwrite.php) |
| link                                                             | 创建文件硬链接                                                                      | link($target, $link);                                                                                  |
| symlink                                                          | 创建符号链接(软链接)                                                                  | symlink($target, $link);                                                                               |
| tmpfile                                                          | 创建一个临时文件 (在临时目录存放 随机文件名 返回句柄)                                                | $temp = tmpfile(); fwrite($temp, "123456"); fclose($temp);                                             |
| <p>request()->file()->move()</p><p>request()->file()->file()</p> | ****[**Thinkphp 文件上传**](https://www.kancloud.cn/manual/thinkphp5/155159)**** | <p>$file = request()->file($name);</p><p>$file->move($filepath);</p>                                   |



### 文件读取

| 函数                                                       | 描述               | 例子                                                                                       |
| -------------------------------------------------------- | ---------------- | ---------------------------------------------------------------------------------------- |
| file_get_contents                                        | 读入文件返回字符串        | echo file_get_contents("flag.txt"); echo file_get_contents("https://www.bilibili.com/"); |
| readfile                                                 | 读取一个文件，并写入到输出缓冲  | 同file_get_contents                                                                       |
| fopen/fread/fgets/fgetss /fgetc/fgetcsv/fpassthru/fscanf | 打开文件或者 URL 读取文件流 | $file = fopen("test.txt","r"); echo fread($file,"1234"); fclose($file);                  |
| file                                                     | 把整个文件读入一个数组中     | echo implode('', file('https://www.bilibili.com/'));                                     |
| highlight_file/show_source                               | 语法高亮一个文件         | highlight_file("1.php");                                                                 |
| parse_ini_file                                           | 读取并解析一个ini配置文件   | print_r(parse_ini_file('1.ini'));                                                        |
| simplexml_load_file                                      | 读取文件作为XML文档解析    |                                                                                          |
