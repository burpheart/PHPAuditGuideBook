---
description: 来自用户可控的输入
---

# 用户可控输入速查表

|                变量/常量/函数/等                | 描述                                                                                                           |
| :--------------------------------------: | ------------------------------------------------------------------------------------------------------------ |
|                 $\_SERVER                | <p>包含 服务器信息 环境变量 用户传入的htt</p><p>p头和uri路径等信息</p>                                                              |
|           $\_GET $HTTP_GET_VARS          | 包含 用户传入的URL参数                                                                                                |
|          $\_POST $HTTP_POST_VARS         | 包含 用户传入的POST BODY的参数 (当 HTTP头中Content-Type 值为 application/x-www-form-urlencoded 或 multipart/form-data时才会被传入) |
|         $\_FILES $HTTP_POST_FILES        | 包含 用户上传文件信息 文件内容 原文件名 临时文件名 大小 等信息                                                                           |
|        $\_COOKIE $HTTP_COOKIE_VARS       | 包含 用户传入的HTTP头中的Cookies kv值                                                                                   |
|                $\_REQUEST                | 同时包含 $\_GET $\_POST $\_COOKIE                                                                                |
|      php://input $HTTP_RAW_POST_DATA     | 包含 用户POST请求中BODY 的完整数据 常见用法 file_get_contents('php://input');                                                |
| apache_request_headers() getallheaders() | 包含 用户传入的http头 (Apache ONLY)                                                                                  |





####
