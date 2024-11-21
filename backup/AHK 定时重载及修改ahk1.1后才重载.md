
```
#Persistent
#SingleInstance ignore

; 设置8分钟自动刷新当前脚本
SetTimer, ReloadCurrentScript, % ((1000 * 60 * 8) * 1)

; 设置8分钟自动刷新 cl3.ahk
SetTimer, ReloadCl3Script, % ((1000 * 60 * 8) * 1)

; 初始化当前脚本的修改时间
FileGetTime, ScriptStartModTime, %A_ScriptFullPath%
SetTimer, CheckScriptUpdate, 100  ; 每100毫秒检查一次脚本修改

; 定义 cl3.ahk 的路径
Cl3ScriptPath := "C:\Path\To\cl3.ahk"  ; 替换为 cl3.ahk 的实际路径

return

; 定时刷新当前脚本
ReloadCurrentScript:
Reload
return

; 定时刷新 cl3.ahk
ReloadCl3Script:
if FileExist(Cl3ScriptPath) {
    Run, % "AutoHotkey.exe " . Cl3ScriptPath
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
```