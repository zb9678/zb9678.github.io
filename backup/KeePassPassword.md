## 打开系统属性/高级/环境变量/系统变量

- 运行 control.exe sysdm.cpl

## 新建系统变量 KeePassPassword

![image](https://github.com/user-attachments/assets/8a9f592a-9170-41b6-8084-9d2f64546abe)

## AHK脚本

```
; 定义全局标志变量
Global ClipboardLock := false

Rctrl & s::
    ClipboardLock := true  ; 设置标志为 true，锁定剪贴板监控
    clipboard := "o0o0o0"  ; 修改剪贴板内容以迷惑监控程序
    
    ; 启动目标程序
    Run, "D:\ahk1.0\Lib\0 tool\9KeePass-2.52\KeePass.exe"
    Sleep, 100
    
    ; 等待释放按键
    KeyWait, s , D
    
    ; 获取密码（假设从环境变量中获取）
    EnvGet, password, KeePassPassword
    
    ; 直接发送密码而不使用剪贴板
    SendInput, %password%{Enter}
return
```

## 说明

迷惑剪贴板监控程序：
在脚本中设置 clipboard := "o0o0o0" 是为了迷惑监控程序

避免剪贴板暴露密码：
替代 clipboard := password 然后 ^v 粘贴，使用 SendInput，直接将密码键入，避免在剪贴板中留下痕迹。

## KeePassPassword命名规范

仅使用字母、数字和下划线（_）。
名称应以字母或下划线开头（例如 _MyVar 或 App_Var）。
避免使用特殊字符或空格。

一般来说，设置环境变量后不需要重启电脑，但可能需要重启相关程序或会话。如果某些程序仍未识别变量，试试关闭并重新打开它，或者刷新环境变量。

可通过 PowerShell 或 CMD 刷新环境变量
打开命令提示符或 PowerShell。
输入以下命令刷新环境变量：
cmd
复制代码
`setx KeePassPassword "1234"`
