---
description: 服务端请求伪造
---

# SSRF

让服务器发起攻击者指定的请求(HTTP/HTTPS/TCP/UDP 等)

攻击者通常用来访问/攻击内网服务 获取内网信息 绕过ip限制

SSRF的函数几乎和文件读取操作一样 php中绝大多数文件读取/写入操作函数都支持多种协议(包括HTTP/S FTP 伪协议 等)

| 函数                                                       | 描述                        | 例子                                                                                                           |
| -------------------------------------------------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------ |
| file_get_contents                                        | 读入文件返回字符串                 | echo file_get_contents("https://www.bilibili.com/");                                                         |
| fsockopen                                                | 打开一个套接字连接(远程 tcp/udp raw) | [https://www.php.net/manual/zh/function.fsockopen.php](https://www.php.net/manual/zh/function.fsockopen.php) |
| readfile                                                 | 读取一个文件，并写入到输出缓冲           | 同file_get_contents                                                                                           |
| fopen/fread/fgets/fgetss /fgetc/fgetcsv/fpassthru/fscanf | 打开文件或者 URL 读取文件流          | $file = fopen("test.txt","r"); echo fread($file,"1234"); fclose($file);                                      |
| file                                                     | 把整个文件读入一个数组中              | echo implode('', file('https://www.bilibili.com/'));                                                         |
| highlight_file/show_source                               | 语法高亮一个文件                  | highlight_file("1.php");                                                                                     |
| parse_ini_file                                           | 读取并解析一个ini配置文件            | print_r(parse_ini_file('1.ini'));                                                                            |
| simplexml_load_file                                      | 读取文件作为XML文档解析             |                                                                                                              |
