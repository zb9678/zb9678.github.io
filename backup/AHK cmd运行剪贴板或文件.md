^F9   
ping  www.my69777.com
my69777.com
^F10
cmd/k 选定文字
^F11
cmd/k 选定文字  管理员身份   如   ipconfig
^F12
cmd/k 选定文件  管理员身份　如   1.bat
^+F12
cmd/k 选定文件  普通身份

`^F9::
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

^F10::
    clipboard = 
    send, ^c
    clipboard = %clipboard%
    Sleep, 100  ; 等待剪切操作完成
    ClipWait  ; 等待剪贴板中有数据
Run, %A_ComSpec% /k %clipboard%
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  ^F10  cmd/k 选定文字   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 012-516

^F11::
    clipboard = 
    send, ^c
    clipboard = %clipboard%
    Sleep, 100  ; 等待剪切操作完成
    ClipWait  ; 等待剪贴板中有数据
Run, %A_ComSpec% /k %clipboard%, , RunAs
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ ^F11  cmd/k 选定文字 以管理员运行   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 012-516

^F12::
    Send, >^x
    Sleep, 100  ; 等待剪切操作完成
    ; 获取剪贴板内容（假设剪贴板中存储的是批处理文件的路径）
    ClipWait  ; 等待剪贴板内容
    batchFilePath := Clipboard  ; 将剪贴板内容赋值给变量

    ; 确保路径是有效的
    if FileExist(batchFilePath) {
        ; 使用 RunAs 命令以管理员身份运行批处理文件
        Run, % "cmd.exe /c """ batchFilePath """", , RunAs
    } else {
        MsgBox, 批处理文件不存在: %batchFilePath%
    }
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  ^F12  cmd/c 选定文件 管理员运行    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 012-517

^+F12::
    Send, >^x      ; 获取批处理文件的路径快捷键
    Sleep, 100  ; 等待剪切操作完成
    ; 获取剪贴板内容（假设剪贴板中存储的是批处理文件的路径）
    ClipWait  ; 等待剪贴板内容
    batchFilePath := Clipboard  ; 将剪贴板内容赋值给变量

    ; 确保路径是有效的
    if FileExist(batchFilePath) {
        ; 非管理员身份　运行批处理文件
        Run, % "cmd.exe /c """ batchFilePath """"
    } else {
        MsgBox, 批处理文件不存在: %batchFilePath%
    }
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  ^F12  cmd/c 选定文件 管理员运行    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 012-517`