```
#Persistent
#SingleInstance ignore

; 设置定时器
SetTimer, ReloadCurrentScript, % ((1000 * 60 * 15) * 1)  ; 15分钟自动重载当前脚本
SetTimer, ReloadCl3Script, % ((1000 * 60 * 10) * 1)  ; 10分钟自动重载 cl3.ahk

; 定义 cl3.ahk 的路径
Cl3ScriptPath := "D:\ahk1.0\CL3-1.106\cl3.ahk"  ; 替换为 cl3.ahk 的实际路径
AutoHotkeyPath := "C:\Program Files\AutoHotkey\AutoHotkey.exe"  ; 替换为 AutoHotkey.exe 的完整路径

; 初始化当前脚本的修改时间
FileGetTime, ScriptStartModTime, %A_ScriptFullPath%
SetTimer, CheckScriptUpdate, 500  ; 每500毫秒检查一次当前脚本的修改时间

return

; 定时刷新当前脚本
ReloadCurrentScript:
Reload
return

; 定时刷新 cl3.ahk
ReloadCl3Script:
if FileExist(Cl3ScriptPath) {
    Run, % AutoHotkeyPath . " " . Cl3ScriptPath
} else {
    MsgBox, 找不到 cl3.ahk 文件，请检查路径。
}
return

; 检查当前脚本是否已修改
CheckScriptUpdate() {
    global ScriptStartModTime
    ; 获取当前的修改时间
    FileGetTime, curModTime, %A_ScriptFullPath%
    if (curModTime != ScriptStartModTime) {
        ; 如果检测到修改，重载脚本
        SetTimer, CheckScriptUpdate, Off  ; 关闭定时器，防止重复触发
        Reload
    }
}

;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  保存后  自动刷新脚本  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01-45
```