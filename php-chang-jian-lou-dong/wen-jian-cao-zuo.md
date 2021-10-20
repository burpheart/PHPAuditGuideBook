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

[php的原生文件上传 ](https://www.php.net/manual/en/features.file-upload.post-method.php)收到POST表单->随机文件名写入临时目录->(执行PHP文件处理逻辑->移动临时文件到保存位置)->删除临时文件(如果临时文件没有被移动)

临时文件路径必须是php上传表单自动处理产生的 例如 $\_FILES\["pictures"]\["tmp\_name"]

"pictures"为表单中的name "tmp\_name"为固定变量名(临时文件名)

**注:**只要PHP收到POST上传文件表单 哪怕php页面一行代码没有 都会将上传文件保存到临时目录 在请求结束后如果临时文件没有被移走就会被自动删除 这里可能会有个条件竞争问题

### 文件解压

```
$zip = new \ZipArchive;
$zip->open('test_new.zip', \ZipArchive::CREATE) //打开一个zip文件
$zip->addFile('test.txt'); //添加压缩文件
$zip->addEmptyDir('newdir');//添加空目录
$zip->addFromString('new.txt', '文本');//从字符串添加文件到压缩包
$zip->extractTo('upload');//将压缩包文件解压到upload目录下
$zip->close();//关闭zip
```

注:ZipArchive扩展在windows平台 php版本>5.6时默认安装. linux及windows其他版本需要手动编译安装.

审计时重点查找 extractTo方法

判断解压目录是否在web目录下 是否检查压缩包内文件类型 如果不在web目录下也可以使用.. 进行目录穿越控制上传目录 到web目录下 或者在权限足够的情况下写入文件到系统关键目录 (自启动 定时任务 ssh公钥 覆盖shadow 等)



文件写入/上传

| 函数                                                               | 描述                                                                           | 例子                                                                                                     |
| ---------------------------------------------------------------- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| file\_put\_contents                                              | 将一个字符串写入文件                                                                   | file\_put\_contents("1.txt","6666");                                                                   |
| move\_uploaded\_file                                             | 将上传的临时文件移动到新的位置                                                              | move\_uploaded\_file($\_FILES\["pictures"]\["tmp\_name"],"1.php")                                      |
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

| 函数                                                       | 描述               | 例子                                                                                           |
| -------------------------------------------------------- | ---------------- | -------------------------------------------------------------------------------------------- |
| file\_get\_contents                                      | 读入文件返回字符串        | echo file\_get\_contents("flag.txt"); echo file\_get\_contents("https://www.bilibili.com/"); |
| readfile                                                 | 读取一个文件，并写入到输出缓冲  | 同file\_get\_contents                                                                         |
| fopen/fread/fgets/fgetss /fgetc/fgetcsv/fpassthru/fscanf | 打开文件或者 URL 读取文件流 | $file = fopen("test.txt","r"); echo fread($file,"1234"); fclose($file);                      |
| file                                                     | 把整个文件读入一个数组中     | echo implode('', file('https://www.bilibili.com/'));                                         |
| highlight\_file/show\_source                             | 语法高亮一个文件         | highlight\_file("1.php");                                                                    |
| parse\_ini\_file                                         | 读取并解析一个ini配置文件   | print\_r(parse\_ini\_file('1.ini'));                                                         |
| simplexml\_load\_file                                    | 读取文件作为XML文档解析    |                                                                                              |
