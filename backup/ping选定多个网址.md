## ping选定多个网址

```
^F9::
    clipboard := ""  ; 清空剪贴板
    Send, ^c  ; 复制选中的文本到剪贴板
    ClipWait  ; 等待剪贴板中有数据
    urls := clipboard  ; 将剪贴板内容存储到变量中

    ; 创建一个临时批处理文件
    FileDelete, ping_commands.bat  ; 删除旧的文件（如果存在）
    FileAppend, @echo off`n, ping_commands.bat  ; 创建新的批处理文件并添加开头

    Loop, parse, urls, `n  ; 遍历每一行（网址）
    {
        FileAppend, ping %A_LoopField%`n, ping_commands.bat  ; 将每个 ping 命令写入批处理文件
    }

    Run, cmd.exe /k ping_commands.bat  ; 在一个窗口中运行批处理文件
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  ^F9  ping选定多个网址  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 012-516
```