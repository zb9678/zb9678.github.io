## config.toml 上传截图 cdn.jsdelivr.net/gh

```
rename = "up1/{month}.{day}:{hour}:{minute}:{second}{ext}"
default_uploader = "github"
[replacements]
"raw.githubusercontent.com" = "cdn.jsdelivr.net/gh"
"/main" = "@main"

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
username = "zb9678"


```

## config.toml 上传截图 ing.w07.us.kg

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

## F1 & a  上传截图到github/img

```
F1 & a::
    ; 启动截图程序
    Run, "D:\ahk1.0\Lib\0 tool\9金山截图王\kscrcap.exe"
    
    ; 延迟 2 秒后弹出确认对话框
    Sleep, 2000
    MsgBox, 4,, 请在完成截图和编辑后点击“是”确认上传图片。
    IfMsgBox, No
        return ; 如果选择“否”，则直接退出脚本
    
    ; 上传图片
    Run, D:\ahk1.0\Lib\0 tool\picgo-croe\upgit.exe :clipboard -o clipboard -f ccc, , hide
    return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & a  上传截图到github/img   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  000001-1984
```

### 使用说明

https://github.com/pluveto/upgit/blob/main/docs/README.zh-CN.md

```
--output-type           如 --output-type clipboard
-o                              如 -o clipboard

upgit :clipboard -o clipboard -f ccc    
"ccc" = '<p align="center"><img src="{url}" style="width:400px;"></p>'
```


<!-- ##{"timestamp":1734343161}## -->


                         