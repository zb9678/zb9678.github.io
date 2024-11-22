## 脚本内容

```
F1 & a::
Text= ⭕       上传图片中     ⭕ 
btt(Text,600,0,,"Style4") 

    ; 启动截图程序
    Run, "D:\ahk1.0\Lib\0 tool\9金山截图王\kscrcap.exe"
    
    ; 延迟 2 秒后弹出确认对话框
    Sleep, 2000
    MsgBox, 4,, 请在完成截图和编辑后点击“是”确认上传图片。
    IfMsgBox, No
        return ; 如果选择“否”，则直接退出脚本

    ; 上传图片
	RunWait, cmd /c "picgo u",, hide
    return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & a  上传截图到github/img   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  000002-2000
```

## 图示（截图效果）

<p align='center'><img src="https://cdn.jsdelivr.net/gh/zcr07/img@main/im2/20241122164136.png" style='width:10px;'><br><br>

## 上传位置

- https://github.com/zcr07/img/tree/main/im2

## 配置文件 config.json 

- 注：如果失效 修改 pat = ""
- 位于 C:\Users\z\.picgo\config.json
- 注："raw.githubusercontent.com" = "cdn.jsdelivr.net/gh" 此条可删除，但得到的链接会被墙，有时显示不出。替换为https://cdn.jsdelivr.net/gh 
- 
- 具体如下图

<p align='center'><img src="https://cdn.jsdelivr.net/gh/zcr07/img@main/im2/20241122171454.png" style='width:400px;'><br><br>


```
rename = "cdn/B{month}.{day}:{hour}:{minute}:{second}{ext}"
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
pat = "ghp_PtTDpkdLFXwwn1M3z5dzS0In2QDu8v1LqQ4"
repo = "img"
username = "zb9678"
```

## 重新申请Tokens  即 pat = "   " 填写内容

- https://github.com/settings/tokens

## 具体填写内容及选项

<p align='center'><img src="https://cdn.jsdelivr.net/gh/zcr07/img@main/im2/20241122170036.png" style='width:400px;'><br><br>

## 复制出此 Tokens

<p align='center'><img src="https://cdn.jsdelivr.net/gh/zcr07/img@main/im2/20241122170215.png" style='width:400px;'><br><br>


