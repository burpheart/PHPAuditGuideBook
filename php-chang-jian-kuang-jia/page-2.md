# Thinkphp

### 模型 视图 控制器

THINKPHP 是一个MVC PHP框架

所谓MVC 是Model View Controller(模型 视图 控制器)的缩写&#x20;

简单理解

**模型主要负责数据处理 (数据库交互 为控制器提供数据 ) **

**视图 负责渲染输出展示给客户端的HTML页面**

**控制器  接收用户请求 与客户端发生交互  处理基本的业务逻辑 决定要输出的视图 **

**使用THINKPHP框架开发的项目 主要审计模型和控制器文件**

### 目录结构

```
project  应用部署目录
├─application           应用目录（可设置）
│  ├─common             公共模块目录（可更改）
│  ├─index              模块目录(可更改)
│  │  ├─config.php      模块配置文件
│  │  ├─common.php      模块函数文件
│  │  ├─controller      控制器目录
│  │  ├─model           模型目录
│  │  ├─view            视图目录
│  │  └─ ...            更多类库目录
│  ├─command.php        命令行工具配置文件
│  ├─common.php         应用公共（函数）文件
│  ├─config.php         应用（公共）配置文件
│  ├─database.php       数据库配置文件
│  ├─tags.php           应用行为扩展定义文件
│  └─route.php          路由配置文件
├─extend                扩展类库目录（可定义）
├─public                WEB 部署目录（对外访问目录）
│  ├─static             静态资源存放目录(css,js,image)
│  ├─index.php          应用入口文件
│  ├─router.php         快速测试文件
│  └─.htaccess          用于 apache 的重写
├─runtime               应用的运行时目录（可写，可设置）
├─vendor                第三方类库目录（Composer）
├─thinkphp              框架系统目录
│  ├─lang               语言包目录
│  ├─library            框架核心类库目录
│  │  ├─think           Think 类库包目录
│  │  └─traits          系统 Traits 目录
│  ├─tpl                系统模板目录
│  ├─.htaccess          用于 apache 的重写
│  ├─.travis.yml        CI 定义文件
│  ├─base.php           基础定义文件
│  ├─composer.json      composer 定义文件
│  ├─console.php        控制台入口文件
│  ├─convention.php     惯例配置文件
│  ├─helper.php         助手函数文件（可选）
│  ├─LICENSE.txt        授权说明文件
│  ├─phpunit.xml        单元测试配置文件
│  ├─README.md          README 文件
│  └─start.php          框架引导文件
├─build.php             自动生成定义文件（参考）
├─composer.json         composer 定义文件
├─LICENSE.txt           授权说明文件
├─README.md             README 文件
├─think                 命令行入口文件
```

./application/xxx/controller/xxxx.php 控制器文件默认位置

./application/xxx/model/xxxx.php 模型文件默认位置

application 目录名可以修改 (某些版本为app  可以在配置文件中自定义)

thinkphp问题大多都出在控制器 初学者建议重点审计控制器文件&#x20;

对框架有一定了解后可以深入审计 不要太局限于控制器

<mark style="color:red;">未完待续</mark>

