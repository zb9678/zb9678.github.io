## config.toml 上传截图

"raw.githubusercontent.com/zcr07/img/main" = "ing.w07.us.kg"  
困扰很久的问题解决了。


```
rename = "images/{month}.{day}:{hour}:{minute}:{second}{ext}"
default_uploader = "github"
[replacements]
"raw.githubusercontent.com/zcr07/img/main" = "ing.w07.us.kg"


[output_formats]
"bbcode" = "[img]{url}[/img]"
"html" = '<img src="{url}" />'
"markdown" = "![]({url})"
"ccc" = '<p align="center"><img src="{url}" style="width:400px;"></p>'

[uploaders.github]
# 保存文件的分支，例如 master 或 main
branch = "main"
pat = "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"
repo = "img"
username = "zcr07"


```