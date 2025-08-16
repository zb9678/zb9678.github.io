```
#Persistent
#SingleInstance ignore

; 设置15分钟自动刷新
SetTimer, dsh1, % ((1000*60*15) * 1)

; 初始化当前脚本的修改时间
FileGetTime, ScriptStartModTime, %A_ScriptFullPath%
SetTimer, CheckScriptUpdate, 1000  ; 每100毫秒检查一次脚本修改

; 初始化另一个脚本的路径和修改时间
OtherScriptPath := "D:\ahk1.0\CL3-1.106\cl3.ahk"  
FileGetTime, OtherScriptModTime, %OtherScriptPath%
SetTimer, CheckOtherScriptUpdate, 1000  ; 每100毫秒检查另一个脚本的修改

return

; 定时刷新当前脚本和另一个脚本
dsh1:
Reload  ; 重载当前脚本
; 检查并重载 cl3.ahk
if FileExist(OtherScriptPath) {
    Run, % "AutoHotkey.exe " . OtherScriptPath
}
return

; 检查当前脚本的修改
CheckScriptUpdate() {
    global ScriptStartModTime
    ; 获取当前的修改时间
    FileGetTime, curModTime, %A_ScriptFullPath%
    if (curModTime != ScriptStartModTime) {
        SetTimer, CheckScriptUpdate, Off  ; 关闭定时器，防止重复触发
        Reload
    }
}

; 检查 cl3.ahk 的修改
CheckOtherScriptUpdate() {
    global OtherScriptPath, OtherScriptModTime
    ; 获取另一个脚本的修改时间
    FileGetTime, curModTime, %OtherScriptPath%
    if (curModTime != OtherScriptModTime) {
        ; 更新修改时间并重载脚本
        OtherScriptModTime := curModTime
        Run, % "AutoHotkey.exe " . OtherScriptPath
    }
}

;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  保存后  自动刷新脚本  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01-45
```