# dailynews
get today's hot news from all big news website
# 新闻 Markdown 生成器使用说明

## 一、程序功能

本程序根据 `template.txt` 模板批量生成 Markdown 新闻文件。

程序启动后，点击“开始”，输入需要生成的文件数量。例如输入 `5`，程序会生成 5 个 `.md` 文件。

每个输出文件会完成以下处理：

- 将日期和时间占位符替换为当前时间
- 按循环次数输出 `{loop}` 和 `{/loop}` 之间的内容
- 从 `link.txt` 按顺序读取 `{link}`
- 从 `title.txt` 中随机读取 `{title}`
- 使用随机字母生成文件名
- 将生成的文件名追加保存到 `log.txt`

## 二、目录文件

以下文件需要放在同一个目录中：

| 文件 | 用途 |
| --- | --- |
| `NewsBuilder.ps1` | PowerShell 主程序 |
| `启动新闻生成器.bat` | 推荐的启动文件 |
| `template.txt` | Markdown 模板 |
| `link.txt` | 链接数据，每行一条 |
| `title.txt` | 标题数据，每行一条 |
| `log.txt` | 程序自动生成，用于记录输出文件名 |

## 三、模板占位符

### 日期和时间

模板支持以下占位符：

```text
{年}  {月}  {日}  {时}  {分}  {秒}
```

示例：

```text
更新时间：{年}年{月}月{日}日 {时}时{分}分{秒}秒
```

### 标题和链接

```text
{title}
{link}
```

- `{title}` 每次循环随机读取 `title.txt` 中的一行
- `{link}` 每次循环读取 `link.txt` 中的下一行
- 读取到 `link.txt` 最后一行后，会重新从第一行开始

### 循环输出

推荐写法：

```text
{loop row="100"}
### {title}

来源：{link}
{/loop}
```

其中 `row="100"` 表示循环输出 100 次。

也支持以下写法：

```text
{loop row=100}
内容
{/loop}
```

或：

```text
{loop}
row=100
内容
{/loop}
```

## 四、运行方法

### 推荐方式

双击：

```text
启动新闻生成器.bat
```

该方式不需要管理员权限。

### PowerShell 方式

在当前目录打开 PowerShell，执行：

```powershell
powershell.exe -ExecutionPolicy Bypass -File .\NewsBuilder.ps1
```

## 五、输出文件

输出文件保存在程序所在目录，文件名格式为：

```text
年月news-5个随机小写字母.md
```

例如：

```text
202611news-wgxgw.md
```

程序会检查文件名是否已经存在。如果重复，会自动重新生成随机字母，避免覆盖原文件。

## 六、日志文件

每生成一个 Markdown 文件，程序会把文件名追加到 `log.txt`，每行一个：

```text
202611news-wgxgw.md
202611news-qkpta.md
202611news-hzmxr.md
```

已有日志不会被覆盖，后续生成的文件名会继续追加到文件末尾。

## 七、注意事项

- `template.txt`、`link.txt` 和 `title.txt` 必须存在
- `link.txt` 至少需要有一条非空内容
- `title.txt` 至少需要有一条非空内容
- 每条链接和标题建议单独占一行
- 请使用 UTF-8 保存模板和数据文件
