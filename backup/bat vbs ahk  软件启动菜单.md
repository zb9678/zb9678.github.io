<p align='center'><img src="https://raw.githubusercontent.com/zcr07/img/refs/heads/main/images/L11.13_13_27_06.png" style='width:400px;'><br><br>

<p align='center'><img src="https://raw.githubusercontent.com/zcr07/img/refs/heads/main/images/L11.13_13_40_07.png" style='width:400px;'><br><br>

## choice1.vbs

Set WshShell = CreateObject("WScript.Shell")
WshShell.Run "choice1.bat", 0, False

## choice1.bat

@echo off
chcp 65001
choice1.ahk
echo ErrorLevel=%ErrorLevel%

if "%ErrorLevel%"=="1" (
    echo 批量共享
) else if "%ErrorLevel%"=="2" (
    echo 照片去底
) else if "%ErrorLevel%"=="3" (
    echo SuperF4
) else (
    echo 未知的选择
)
pause

## choice1.ahk

#SingleInstance Force
#NoEnv
SetWorkingDir %A_ScriptDir%
SetBatchLines -1

#Include %A_ScriptDir%\ControlColor.ahk

Gui +hWndhMainWnd
Gui Font, s9, Segoe UI
Gui Color, 0xFF8000
Gui Add, Text, hWndhTxt x102 y49 w132 h71 +0x200, 选择要启动的软件
ControlColor(hTxt, hMainWnd, 0xFF8080, 0x800040)
Gui Add, Button, gplgx x29 y177 w80 h23, &1 批量共享
Gui Add, Button, gqd x130 y175 w80 h23, &2 照片去底
Gui Add, Button, gStopup x234 y177 w80 h23, &3 SuperF4

Gui Show, w340 h235, Window
Return

plgx:
run C:\3\局域网共享\批量共享.exe
ExitApp 1  ; 设置返回码为 1
Return

qd:
run C:\3\拍照试卷去底工具\照片去底色免费版.exe
ExitApp 2  ; 设置返回码为 2
Return

Stopup:
run C:\3\SuperF4\SuperF4.exe
ExitApp 3  ; 设置返回码为 3
Return

GuiEscape:
GuiClose:
    ExitApp

