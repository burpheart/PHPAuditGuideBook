# PHP弱类型

PHP是一种弱类型语言 在定义变量时无需定义变量值类型 PHP会根据变量内容自动转换类型

例如 整数与字符串松散比较时 字符串会转成整数 "0abcdefg"==0

PHP 的松散比较 (==) [https://www.php.net/manual/zh/types.comparisons.php](https://www.php.net/manual/zh/types.comparisons.php)



| 值1\值2       | **`true`**  | **`false`** | `1`         | `0`         | `-1`        | `"1"`       | `"0"`       | `"-1"`      | **`null`**  | `array()`   | `"php"`     | `""`        |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| **`true`**  | **`true`**  | **`false`** | **`true`**  | **`false`** | **`true`**  | **`true`**  | **`false`** | **`true`**  | **`false`** | **`false`** | **`true`**  | **`false`** |
| **`false`** | **`false`** | **`true`**  | **`false`** | **`true`**  | **`false`** | **`false`** | **`true`**  | **`false`** | **`true`**  | **`true`**  | **`false`** | **`true`**  |
| `1`         | **`true`**  | **`false`** | **`true`**  | **`false`** | **`false`** | **`true`**  | **`false`** | **`false`** | **`false`** | **`false`** | **`false`** | **`false`** |
| `0`         | **`false`** | **`true`**  | **`false`** | **`true`**  | **`false`** | **`false`** | **`true`**  | **`false`** | **`true`**  | **`false`** | **`true`**  | **`true`**  |
| `-1`        | **`true`**  | **`false`** | **`false`** | **`false`** | **`true`**  | **`false`** | **`false`** | **`true`**  | **`false`** | **`false`** | **`false`** | **`false`** |
| `"1"`       | **`true`**  | **`false`** | **`true`**  | **`false`** | **`false`** | **`true`**  | **`false`** | **`false`** | **`false`** | **`false`** | **`false`** | **`false`** |
| `"0"`       | **`false`** | **`true`**  | **`false`** | **`true`**  | **`false`** | **`false`** | **`true`**  | **`false`** | **`false`** | **`false`** | **`false`** | **`false`** |
| `"-1"`      | **`true`**  | **`false`** | **`false`** | **`false`** | **`true`**  | **`false`** | **`false`** | **`true`**  | **`false`** | **`false`** | **`false`** | **`false`** |
| **`null`**  | **`false`** | **`true`**  | **`false`** | **`true`**  | **`false`** | **`false`** | **`false`** | **`false`** | **`true`**  | **`true`**  | **`false`** | **`true`**  |
| `array()`   | **`false`** | **`true`**  | **`false`** | **`false`** | **`false`** | **`false`** | **`false`** | **`false`** | **`true`**  | **`true`**  | **`false`** | **`false`** |
| `"php"`     | **`true`**  | **`false`** | **`false`** | **`true`**  | **`false`** | **`false`** | **`false`** | **`false`** | **`false`** | **`false`** | **`true`**  | **`false`** |
| `""`        | **`false`** | **`true`**  | **`false`** | **`true`**  | **`false`** | **`false`** | **`false`** | **`false`** | **`true`**  | **`false`** | **`false`** | **`true`**  |
