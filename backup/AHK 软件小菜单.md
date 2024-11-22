<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/cdn/B11.22:22:52:39.png" style="width:400px;"></p>

## choice1.vbs

```
Set zz = CreateObject("WScript.Shell")
zz.Run "choice1.bat", 0, False
```

## choice1.bat

```
@echo off
chcp 65001
choice1.ahk
echo ErrorLevel=%ErrorLevel%

if "%ErrorLevel%"=="1" (
    echo Word
) else if "%ErrorLevel%"=="2" (
    echo EXCEL
) else if "%ErrorLevel%"=="3" (
    echo POWERPNT
) else (
    echo 未知的选择
)
pause
```

## ControlColor.ahk

```
; http://www.autohotkey.com/board/topic/104539-controlcol-set-background-and-text-color-gui-controls/

ControlColor(Control, Window, bc := "", tc := "", Redraw := True) {
    Local a := {}
    a["c"]  := Control
    a["g"]  := Window
    a["bc"] := (bc == "") ? "" : (((bc & 255) << 16) + (((bc >> 8) & 255) << 8) + (bc >> 16))
    a["tc"] := (tc == "") ? "" : (((tc & 255) << 16) + (((tc >> 8) & 255) << 8) + (tc >> 16))

    CC_WindowProc("Set", a, "", "")

    If (Redraw) {
        WinSet Redraw,, ahk_id %Control%
    }
}

CC_WindowProc(hWnd, uMsg, wParam, lParam) {
    Local tc, bc, a
    Static Win := {}
    ; Critical

    If uMsg Between 0x132 And 0x138 ; WM_CTLCOLOR(MSGBOX|EDIT|LISTBOX|BTN|DLG|SCROLLBAR|STATIC)
    If (Win[hWnd].HasKey(lParam)) {
        If (tc := Win[hWnd, lParam, "tc"]) {
            DllCall("gdi32.dll\SetTextColor", "Ptr", wParam, "UInt", tc)
        }

        If (bc := Win[hWnd, lParam, "bc"]) {
            DllCall("gdi32.dll\SetBkColor",   "Ptr", wParam, "UInt", bc)
        }

        Return Win[hWnd, lParam, "Brush"] ; Return the HBRUSH to notify the OS that we altered the HDC.
    }

    If (hWnd == "Set") {
        a := uMsg
        Win[a.g, a.c] := a

        If ((Win[a.g, a.c, "tc"] == "") && (Win[a.g, a.c, "bc"] == "")) {
            Win[a.g].Remove(a.c, "")            
        }

        If (!Win[a.g, "WindowProcOld"]) {
            Win[a.g,"WindowProcOld"] := DllCall("SetWindowLong" . (A_PtrSize == 8 ? "Ptr" : "")
            , "Ptr", a.g, "Int", -4, "Ptr", RegisterCallback("CC_WindowProc", "", 4), "UPtr")
        }

        If (Win[a.g, a.c, "bc"] != "") {
            Win[a.g, a.c, "Brush"] := DllCall("gdi32.dll\CreateSolidBrush", "UInt", a.bc, "UPtr")
        }

        Return
    }

    Return DllCall("CallWindowProc", "Ptr", Win[hWnd, "WindowProcOld"], "Ptr", hWnd, "UInt", uMsg, "Ptr", wParam, "Ptr", lParam, "Ptr")
}

```


## choice1.ahk

```

#SingleInstance Force
#NoEnv
SetWorkingDir %A_ScriptDir%
SetBatchLines -1

#Include %A_ScriptDir%\ControlColor.ahk

Gui +hWndhMainWnd
Gui Font, s9, Segoe UI
Gui Color, 0xFF8000
;Gui Add, Text, hWndhTxt x102 y49 w132 h71 +0x200, 选择要启动的软件
ControlColor(hTxt, hMainWnd, 0xFF8080, 0x800040)

Gui Add, Button, gdd x29 y177 w80 h23, Word
Gui Add, Button, gee x130 y177 w80 h23, EXCEL
Gui Add, Button, gff x234 y177 w80 h23, POWERPNT

Gui Add, Button, gaa x29 y137 w80 h23, 11Manager
Gui Add, Button, gbb x130 y137 w80 h23, 右键设置
Gui Add, Button, gcc x234 y137 w80 h23, 任务管理器

Gui Add, Button, ggg x29 y97 w80 h23, 键盘可视化
Gui Add, Button, ghh x130 y97 w80 h23, 重复文件
Gui Add, Button, gii x234 y97 w80 h23, 磁盘碎片

Gui Add, Button, gr x29 y57 w80 h23, 文件对比
Gui Add, Button, gs x130 y57 w80 h23, Joplin
Gui Add, Button, gt x234 y57 w80 h23, 输入法管理

Gui Add, Button, gu x29 y17 w80 h23, CorelDRW
Gui Add, Button, gv x130 y17 w80 h23, PDFXEdit
Gui Add, Button, gw x234 y17 w80 h23, RegWork

Gui Add, Button, gx x29 y217 w80 h23, 批量重命名
Gui Add, Button, gy x130 y217 w80 h23, KeePass
Gui Add, Button, gz x234 y217 w80 h23, WindTerm

Gui Show, w340 h260, 选择要启动的软件
Return

gg:
run C:\3\5\键盘可视化Keyviz\keyviz.exe
ExitApp 7  ; 设置返回码为 7
Return

hh:
run C:\3\6 Duplicate Cleaner v4.1.1 Portable\DuplicateCleanerProPortable.exe
ExitApp 8  ; 设置返回码为 8
Return

ii:
run C:\3\7 SmartDefrag\SmartDefrag.exe
ExitApp 9  ; 设置返回码为 9
Return

dd:
run C:\0　　tool\0\9 Office\9                Office2016\Office16\WINWORD.EXE
ExitApp 1  ; 设置返回码为 1
Return

ee:
run D:\ahk1.0\1\2\00   快捷键目录.xlsx
ExitApp 2  ; 设置返回码为 2
Return

ff:
run C:\0　　tool\0\9 Office\9                Office2016\Office16\POWERPNT.EXE
ExitApp 3  ; 设置返回码为 3
Return

aa:
run C:\3\Windows11Manager\Windows11Manager.exe
ExitApp 4  ; 设置返回码为 4
Return

bb:
run C:\3\Windows11Manager\App\ContextMenuManager.exe
ExitApp 5  ; 设置返回码为 5
Return

cc:
run C:\3\Windows11Manager\App\MyTask.exe
ExitApp 6  ; 设置返回码为 6
Return

r:
run C:\3\9BCompare\BCompare.exe
ExitApp 10  ; 设置返回码为 10
Return

s:
run C:\3\9 JoplinPortable2\Joplin.exe
ExitApp 11  ; 设置返回码为 11
Return

t:
run C:\3\9 imetl3输入法\输入法管理器.exe
ExitApp 12  ; 设置返回码为 12
Return

u:
run C:\3\9 CorelDRAW Graphics Suite X4\Programs\CorelDRW.exe
ExitApp 13  ; 设置返回码为 13
Return

v:
run C:\3\PDFXEdit10_Portable_x64\PDFXEdit.exe
ExitApp 14  ; 设置返回码为 14
Return

w:
run C:\3\Registry Workshop\RegWorkshopX64.exe
ExitApp 15  ; 设置返回码为 15
Return

x:
run C:\3\9 ReNamer\ReNamer.exe
ExitApp 16  ; 设置返回码为 16
Return

y:
run C:\3\9KeePass-2.52\KeePass.exe
ExitApp 17  ; 设置返回码为 17
Return

z:
run C:\3\WindTerm_2.6.1\WindTerm.exe
ExitApp 18  ; 设置返回码为 18
Return

GuiEscape:
GuiClose:
    ExitApp
```