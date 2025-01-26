## 任务栏透明度

WinSet, Transparent, 210, ahk_class Shell_TrayWnd			        ; 210  0-255 任务栏透明度


## 更新 github_hosts

Run, "C:\Program Files\Git\git-bash.exe" --hide "D:\ahk1.0\fetch_github_hosts", , Hide


### fetch_github_hosts 文件

```
_hosts=$(mktemp /tmp/hostsXXX)
hosts=/c/Windows/System32/drivers/etc/hosts
remote=https://raw.hellogithub.com/hosts
reg='/# GitHub520 Host Start/,/# Github520 Host End/d'

sed "$reg" $hosts > "$_hosts"
curl "$remote" >> "$_hosts"
cat "$_hosts" > "$hosts"

rm "$_hosts"
```

### Git 下载

- https://git-scm.com/downloads


## ahk1.0 前设置

```
#Requires AutoHotkey v1.1.36                            ; -----------------------------------V1版本
Menu, Tray, Icon, D:\ahk1.0\Lib\0\Library.ico      ;--------------------------------- 脚本图标
Menu , tray , tip , Ahk1.1                                      ;---------------------------- 鼠标悬浮提示
#NoEnv                                                                 ;--------------------------------- 改善性能
#SingleInstance Force        　                               ;------只允许单个该脚本运行,脚本强制替换
SendMode Input             ;-------Send,SendRaw,Click,MouseMove/Click/Drag到SendInput
#WinActivateForce                                               ;-------------------- 用强制的方法激活窗口
#ClipboardTimeout -1                         ;首次访问剪贴板失败后脚本继续访问剪贴板的持续时间
                                        ; -1 表示持续访问剪贴板. 0 只访问1次. 无 使用 1000 ms 的超时时间
SetWorkingDir, %A_ScriptDir%                            ;----------- 脚本所在的文件夹作为工作目录
SetTitleMatchMode fast
SetBatchLines, -1                                                 ; 脚本快速执行,减少 CPU 占用,  使用10ms -1
Process,priority, , high                                         ;------------------------脚本进程优先级为高
#HotkeyModifierTimeout 0  ;影响热键修饰符的行为：^!#+。设为 0 时则总是超时 (修饰键总是不会被推回到按下的状态)
;DetectHiddenWindows, On
;SetTitleMatchMode, 2                                        ; 2 窗口标题部分匹配. 3 要求标题必须准确匹配
;#Persistent                      ; 使非热键类的脚本持久运行 直到用户关闭或遇到 ExitApp 如果脚本包含此指令，即使在 return 后没有其他代码，脚本依然会保持运行。
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 1-19

WinSet, Transparent, 210, ahk_class Shell_TrayWnd			        ; 210  0-255 任务栏透明度
Run, "C:\Program Files\Git\git-bash.exe" --hide "D:\ahk1.0\fetch_github_hosts", , Hide
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 2-29

#include *i %A_ScriptDir%\Lib\ImagePut.ahk%A_TrayMenu%.ahk
#Include *i %A_ScriptDir%\Lib\ImagePut.ahk
#Include *i %A_ScriptDir%\Lib\BTT.ahk
#Include *i %A_ScriptDir%\Lib\Gdip_All.ahk
#Include *i %A_ScriptDir%\Lib\NonNull.ahk
#Include *i %A_ScriptDir%\Lib\TrayIcon.ahk
#Include *i %A_ScriptDir%\Lib\StdOutToVar.ahk
#Include *i %A_ScriptDir%\Lib\ahk777.ahk
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 2-29

#SingleInstance Off
;MsgBox, 4096,, % A_Now
return

	OnlyOne(flag="") 
  {
  	static init:=OnlyOne("001")
  	DetectHiddenWindows, % (bak:=A_DetectHiddenWindows) ? "On":"On"
  	mypid:=DllCall("GetCurrentProcessId")
  	flag:="Ahk_OnlyOne_Ahk<<" . flag . ">>"
  	Gui, Ahk_OnlyOne_Ahk: Show, Hide, %flag%
  	WinGet, list, List, %flag% ahk_class AutoHotkeyGUI
  	Loop, % list
  	IfWinExist, % "ahk_id " . list%A_Index%
  {
    	WinGet, pid, PID
    	IfEqual, pid, %mypid%, Continue
   	 WinClose, ahk_pid %pid% ahk_class AutoHotkey,, 3
    	IfWinNotExist,,, Continue
    	Process, Close, %pid%
    	WinWaitClose
  }

  	WinGet, list, List, %flag% ahk_class AutoHotkeyGUI
  	IfNotEqual, list, 1, ExitApp
  	DetectHiddenWindows, %bak%
  }

;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   限制单进程运行    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 3-64
```