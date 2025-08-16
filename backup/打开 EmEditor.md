## 打开 EmEditor

```
#Persistent                     ;确保脚本常驻：保证脚本不因长时间未使用而自动退出。
Rctrl & 2::
    KeyWait, Rctrl, D  ; 确保释放 Rctrl 键后再执行操作

    ; 检查 EmEditor.exe 是否已存在
    IfWinNotExist, ahk_exe EmEditor.exe
    {
        Run "C:\0　　tool\EmEditor\EmEditor.exe"
        WinWait, ahk_exe EmEditor.exe, , 5  ; 最多等待 5 秒
    }
    Else IfWinNotActive, ahk_exe EmEditor.exe
    {
        WinActivate  ; 激活窗口
    }
    Else
    {
        ; 检查窗口是否已最小化
        IfWinExist, ahk_exe EmEditor.exe
        {
            WinGet, MinimizedState, MinMax, ahk_exe EmEditor.exe
            if (MinimizedState = -1)  ; 如果窗口已最小化
                WinRestore  ; 还原窗口
            else
                WinMinimize  ; 否则最小化窗口
        }
    }
Return

;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  Rctrl & 2   打开 EmEditor  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00012-999
```