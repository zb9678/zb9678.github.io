## 设置新环境变量

打开命令提示符 CMD

输入以下命令完成 环境变量的设置：

```
setx zf8 "@zb8"
setx zf7 "Zb8"
setx zf6 "@Zb8"
setx zf5 "0712"
```

注意：  `设置环境变量后 需要重启电脑。`


<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img9@main/im2/08.17:11:33:41.png" style="width:400px;"></p><br>

----------------------------------------------------------------------------------------

或者  如下操作

## 打开系统属性/高级/环境变量/系统变量


- 运行 control.exe sysdm.cpl

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img9@main/im2/08.17:11:36:10.png" style="width:400px;"></p><br>



## 新建z的用户变量 KeePassPassword

![image](https://github.com/user-attachments/assets/8a9f592a-9170-41b6-8084-9d2f64546abe)

-----------------------------------------------------------------------------------------


## AHK脚本

```
    Global ClipboardLock := false                         ; 定义全局标志变量

F1 & r::
    ClipboardLock := true                                      ; 设置标志为 true，锁定剪贴板监控
    clipboard := "."                                     ; 修改剪贴板内容以迷惑监控程序

    Run, "D:\ahk1.0\Lib\0 tool\9KeePass-2.52\KeePass.exe"
    Sleep, 100
    KeyWait, r , D       			        ; 等待释放按键
    EnvGet, password, zf5             ; 获取密码（从环境变量中获取）
    SendInput, %password%{Enter}                      ; 直接发送密码而不使用剪贴板
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F1 & r  Keebass.exe   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 26-499

F1 & F6::
    	EnvGet, password, zf6                    ; 环境变量设置后需重启电脑  

    	; 切换到英文输入法
    	Send, {Shift} ; 根据你的设置可能需要调整，不设置会输出乱码

    	; 使用 SendInput 发送密码
    	SendInput, %password%{Shift}
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & F6 获取系统变量中密码   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 29--538

F1 & F7::
    	EnvGet, password, zf7                   ; 环境变量设置后需重启电脑  

    	; 切换到英文输入法
    	Send, {Shift} ; 根据你的设置可能需要调整

    	; 使用 SendInput 发送密码
    	SendInput, %password%{Shift}
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & F7 获取系统变量中密码   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 29--538

F1 & F8::
	EnvGet, password, zf8                 ; 环境变量设置后需重启电脑

   	; 切换到英文输入法
    	Send, #{Shift} ; 根据你的设置可能需要调整

    	; 使用 SendInput 发送密码
    	SendInput, %password%{Shift}
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & F8 获取系统变量中密码   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 28-527
```

## 说明

迷惑剪贴板监控程序：
在脚本中设置 clipboard := "." 是为了迷惑监控程序

避免剪贴板暴露密码：
替代 clipboard := password 然后 ^v 粘贴，使用 SendInput，直接将密码键入，避免在剪贴板中留下痕迹。

## KeePassPassword命名规范

仅使用字母、数字和下划线（_）。
名称应以字母或下划线开头（例如 _MyVar 或 App_Var）。
避免使用特殊字符或空格。

                                                                  











