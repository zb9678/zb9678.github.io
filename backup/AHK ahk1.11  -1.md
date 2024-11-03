`
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ
#Requires AutoHotkey v1.1.36                             ; -----------------------------------V1版本
Menu, Tray, Icon, D:\ahk1.0\Lib\0\Library.ico       ;--------------------------------- 脚本图标
Menu , tray , tip , Ahk1.1                                       ;---------------------------- 鼠标悬浮提示
#NoEnv                                                                 ;--------------------------------- 改善性能
#SingleInstance Force        　                               ;------只允许单个该脚本运行,脚本强制替换
SendMode Input             ;-------Send,SendRaw,Click,MouseMove/Click/Drag到SendInput
#WinActivateForce                                               ;-------------------- 用强制的方法激活窗口
#Persistent                      ;----------- 使非热键类的脚本持久运行 直到用户关闭或遇到 ExitApp
#ClipboardTimeout -1                         ;首次访问剪贴板失败后脚本继续访问剪贴板的持续时间
                                        ; -1 表示持续访问剪贴板. 0 只访问1次. 无 使用 1000 ms 的超时时间
SetWorkingDir, %A_ScriptDir%                            ;----------- 脚本所在的文件夹作为工作目录
SetTitleMatchMode fast
SetBatchLines, -1                                               ; 脚本快速执行,减少 CPU 占用,  使用10ms -1
Process,priority, , high                                         ;------------------------脚本进程优先级为高
#HotkeyModifierTimeout 0  ;影响热键修饰符的行为：^!#+。设为 0 时则总是超时 (修饰键总是不会被推回到按下的状态).
DetectHiddenWindows, On
SetTitleMatchMode, 2 ; 设置标题匹配模式
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ

; 获取当前脚本的修改时间
FileGetTime, ScriptStartModTime, %A_ScriptFullPath%
SetTimer, CheckScriptUpdate, 100  ; 每100毫秒检查一次脚本修改

CheckScriptUpdate() {
    global ScriptStartModTime
    ; 获取当前的修改时间
    FileGetTime, curModTime, %A_ScriptFullPath%
    
    ; 如果当前修改时间和启动时不同，则重新加载脚本
    if (curModTime != ScriptStartModTime) {
        SetTimer, CheckScriptUpdate, Off  ; 关闭定时器，防止重复触发
        Reload
        ; 如果重载失败，给出提示
        if (ErrorLevel) {
            MsgBox, 0x2, %A_ScriptName%, 重载失败，是否重试？选择“忽略”将继续运行当前脚本。
            ifMsgBox, Retry
                SetTimer, CheckScriptUpdate, On  ; 重新启用定时器，继续检查修改
            else ifMsgBox, Abort
                ExitApp  ; 放弃则退出脚本
        }
    }
}
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  保存后  自动刷新脚本 ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ
#include *i %A_ScriptDir%\Lib\ImagePut.ahk%A_TrayMenu%.ahk
#Include *i %A_ScriptDir%\Lib\ImagePut.ahk
#Include *i %A_ScriptDir%\Lib\BTT.ahk
#Include *i %A_ScriptDir%\Lib\Gdip_All.ahk
#Include *i %A_ScriptDir%\Lib\NonNull.ahk
#Include *i %A_ScriptDir%\Lib\TrayIcon.ahk
#Include *i %A_ScriptDir%\Lib\StdOutToVar.ahk
#Include *i %A_ScriptDir%\Lib\ahk777.ahk

; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ

;🎫🎫🎫🎫🎫🎫🎫🎫🎫🎫    基本   设置   🎫🎫🎫🎫🎫🎫🎫🎫🎫🎫🎫

OnClipboardChange:
{
	SoundBeep, 10000, 1	
	btt(Clipboard,,,,"Style8")
	sleep, 700
	btt()​
;FileAppend, %clipboard% `n, c:\6           ;----------------  剪贴板历史记录保存
	return
}
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ     复制后通知    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 2

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    限制单进程运行   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00

;🎫🎫🎫🎫🎫🎫🎫🎫🎫🎫    基本   设置   🎫🎫🎫🎫🎫🎫🎫🎫🎫🎫🎫
;🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁    复制   粘贴   🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁

global MyClipData
global page
*>!q:: 批量复制粘贴工具()
	#IfWinExist, 批量复制粘贴工具 ahk_class AutoHotkeyGUI
$^c::
	Clipboard:=""
	Send ^c{Ctrl Up}
	ClipWait, 3
	s:=Clipboard
	if (s="")
	ToolTip,
else
	批量复制粘贴工具(s)
	return
1::
	nume:=1
	Gosub copytt(nume)
	return
2::
	nume:=2
	Gosub copytt(nume)
	return
3::
	nume:=3
	Gosub copytt(nume)
	return
4::
	nume:=4
	Gosub copytt(nume)
	return
5::
	nume:=5
	Gosub copytt(nume)
	return
6::
	nume:=6
	Gosub copytt(nume)
	return
7::
	nume:=7
	Gosub copytt(nume)
	return
8::
	nume:=8
	Gosub copytt(nume)
	return
9::
	nume:=9
	Gosub copytt(nume)
	return
copytt(nume):
{
	i:=nume
	Clipboard:=MyClipData[i:=(page-1)*10+i]
	Send ^v
	return
}
0::
	nume1:=0
	Gosub copytt(nume1)
	return
copytt(nume1):
{
	i:=nume1
	Clipboard:=MyClipData[i:=(page-1)*10+10+i]
	Send ^v
	return
}
	#IfWinExist

;-------- 下面是函数 --------
批量复制粘贴工具(s:="", Cmd:="")
{
static
  	if (Cmd="Move")
{
	if (A_GuiControl="")
	SendMessage, 0xA1, 2
	return
}
else if (Cmd="Click")
{
    	i:=SubStr(A_GuiControl, 3)
    	if (i>=1 and i<=10)
{
      	s:=MyClipData[i:=(page-1)*10+i]
      	if (s="")
        	return
      	if (!clear)
{
       	; Gui, MyClip: Hide
        	; Gui, MyClip: Show, NA
        	Clipboard:=s
        	Send ^v
        	Sleep, 200
        	return
}
      	MyClipData.RemoveAt(i)
      	if (MyClipData.length()<(page-1)*10+1)
        	page--
}
else if (i=11 and page>1)
	page--
else if (i=13 and MyClipData.length()>page*10)
	page++
else if (i=12)
      	clear:=!clear
}
else if (Cmd="" and s!="")
{
    	MyClipData.InsertAt(1,s), page:=1, clear:=0
}
 	 if !IsObject(MyClipData)
{
    MyClipData:=[], page:=1, clear:=0
    Run:=Func(A_ThisFunc).Bind("","Click")
    Gui, MyClip: Destroy
    Gui, MyClip: +AlwaysOnTop +ToolWindow +E0x08000000
    Gui, MyClip: Margin, 10, 10
    Gui, MyClip: Color, f39bdc8
    Gui, MyClip: Font, s11,c364f6b
    Loop, 13
{
      	i:=A_Index, v:=(i=11 ? "<<" : i=13 ? ">>" : "")
      	j:=(i=1 ? "w250 Left" : i=11 ? "xm w75"
       	 : i=12 ? "x+0 w100" : i=13 ? "x+0 w75" : "y+0 wp Left")
      	Gui, MyClip: Add, Button, %j% vbt%i% Hwndid -Wrap, %v%
      	GuiControl, MyClip: +g, %id%, % Run
}
    	Gui, MyClip: Show, NA, %A_ThisFunc%
    	OnMessage(0x201, Func(A_ThisFunc).Bind("","Move"))
    	v:=Func(A_ThisFunc).Bind("","")
    	Menu, Tray, Add
    	Menu, Tray, Add, %A_ThisFunc%, %v%
    	Menu, Tray, Default, %A_ThisFunc%
    	Menu, Tray, Click, 1
}
Loop, 10
{    
	Menu, Tray, Click, 1
    	i:=A_Index, v:=MyClipData[(page-1)*10+i]
    	v:=(v="" ? v : "[" StrLen(v) "] " SubStr(v,1,50))
    	v:=RegExReplace(v, "s+", " ")
    	GuiControl, MyClip: , bt%i%, %v%
}
  	GuiControl, MyClip: , bt12, % clear ? "点选条目":"+删除条目+"
  	Gui, MyClip: Show, NA
}
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ art+q 批量复制粘贴  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01

#Persistent
	Copy(clipboardID) 
{
	global ; All variables are global by default
	local oldClipboard := ClipboardAll ; Save the (real) clipboard

	Clipboard := "" ; Erase the clipboard first, or else ClipWait does nothing
	SendInput {Ctrl Down}c{Ctrl Up}
	ClipWait, 2, 1 ; Wait 1s until the clipboard contains any kind of data
if ErrorLevel 
{
	Clipboard := oldClipboard ; Restore old (real) clipboard
	return
}
	ClipboardData%clipboardID% := Clipboard
	Clipboard := oldClipboard ; Restore old (real) clipboard
}
Cut(clipboardID) 
{
	global ; All variables are global by default
	local oldClipboard := ClipboardAll ; Save the (real) clipboard
	Clipboard := "" ; Erase the clipboard first, or else ClipWait does nothing
	SendInput {Ctrl Down}x{Ctrl Up}
	ClipWait, 2, 1 ; Wait 1s until the clipboard contains any kind of data
if ErrorLevel 
{
	Clipboard := oldClipboard ; Restore old (real) clipboard
	return
}
	ClipboardData%clipboardID% := Clipboard
	Clipboard := oldClipboard ; Restore old (real) clipboard
}
Paste(clipboardID) 
{
	global
	local oldClipboard := ClipboardAll ; Save the (real) clipboard
	Clipboard := "" ; Erase the clipboard first, or else ClipWait does nothing
	Clipboard := ClipboardData%clipboardID%
	ClipWait, 2, 1 ; Wait 1s until the clipboard contains any kind of data
	SendRaw, % Clipboard ; Was having an issue with ^v
	Clipboard := oldClipboard ; Restore old (real) clipboard
}
	return
;---------------------------------------------------------------------------   copy
 >!2::Copy(1)
 >!3::Copy(2)
 >!4::Copy(3)
 >!5::Copy(4)
 >!s::Copy(5)
 >!d::Copy(6)
 >!f::Copy(7)
 ;---------------------------------------------------------------------------   paste
 >!w::Paste(1)
 >!e::Paste(2)
 >!r::Paste(3)
 >!t::Paste(4)
 >!x::Paste(5)
 >!c::Paste(6)
 >!v::Paste(7)
;-----------------------------------------------------------------------------   cut
 >!g::Cut(1)
 >!h::Cut(2)
 >!j::Cut(3)
 >!k::Cut(4)
;---------------------------------------------------------------------------   paste
 >!b::Paste(1)                                 ;-------------->! g 剪切    >! b 粘贴
 >!n::Paste(2)
 >!m::Paste(3)
 >!,::Paste(4)
;-----------------------------------------------------------------------------------
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ >! 2345sdf复制  wertxcv 粘贴   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 02

 >^c::                                              
	clipboard :=GetFilename(GetPath())   ;---------获取带后缀名的文件名
	sleep,1000
	send, {f2}^c                    ;---------------------再一次获取无后缀文件名
	return
;-----------剪贴板中现在有２个文件名，有后缀和无后缀
 >^x::                                                
	clipboard :=GetPath()         ;----------------------------------获取路径
	return

GetFolder(txt)
{
	SplitPath, txt,, o
	return o
}
GetFilename(txt)
{
	SplitPath, txt, o
	return o
}
;在当前资源管理器窗口中，获取选中文件路径
GetPath(hwnd="")
{
	ComObjError(false)
WinGet, process, processName, % "ahk_id" hwnd := hwnd? hwnd:WinExist("A")
        	WinGetClass class, ahk_id %hwnd%
        	if (process != "explorer.exe")
	return
        	if (class ~= "Progman|WorkerW") {
ControlGet, files, List, Selected Col1, SysListView321, ahk_class %class%
	Loop, Parse, files, `n, `r
	ToReturn .= A_Desktop "\" A_LoopField "`n"
}
        	else if (class ~= "(Cabinet|Explore)WClass")
{
	for window in ComObjCreate("Shell.Application").Windows
{
	if (window.hwnd==hwnd)
	sel := window.Document.SelectedItems
}
	for item in sel
	ToReturn .= item.path "`n"
}
        	return Trim(ToReturn,"`n")
}
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  >^c 复制文件名 >^x 获取路径   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 03

 >^v::
	send, {F2}
	sleep, 200
	send, {ctrl down}v{ctrl up}{enter}
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  >^v 对文件夹文件粘贴文件名   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 04

;🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁    复制   操作   🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁
;🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆    截图   操作   🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆

;ImagePutFile(Image)             ; 将图片存为文件
;ImagePutClipboard(Image)   ; 将图片存入剪贴板
;ImagePutWindow(Image)     ; 将图片显示出来
;ImageShow(Image)               ; 将图片显示出来（无标题栏）
;ImagePutDesktop(Image)     ; 将图片放在桌面壁纸前、桌面图标后的位置

Appskey & 1::
Run, nircmd  savescreenshot "C:\oneD\OneDrive\desktop\~$currdate.yyyyMMdd$-~$currtime.HHmmss$.png"  
return                                                                   ;-----------------------截全屏
;ImagePutClipboard(ImagePutFile("A", "C:\oneD\OneDrive\desktop\"))        ;-- 只截窗口 存剪
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  全屏截存桌面选格式 Appskey & 1   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 001

Appskey & 6::
Imageshow("a")                                                                      ;------------------截图并贴图
ImagePutFile(Image)                                           ;----------- 将图片存入剪贴板
ImagePutClipboard(ImagePutFile("A", "C:\oneD\OneDrive\desktop"))     ; 存desktop
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 当前窗口 截图并贴图 Appskey & 6  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 009

Appskey & 2::
	Run "D:\ahk1.0\Lib\0 tool\窗口隐藏工具\窗口隐藏工具.exe"
	Run c:\3\4\Gif123.exe
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  Appskey & 2  录屏gif   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 002

Appskey & 3::
	Run "D:\ahk1.0\Lib\0 tool\窗口隐藏工具\窗口隐藏工具.exe"
	Run c:\3\9ZDSoftScnRec\ScnRecPortable.exe
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  Appskey & 3 录屏MP4   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 003
Appskey & 4::
file := ImagePutFile(clip, "C:\oneD\OneDrive\desktop\" )
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞ  剪贴板中截图保存于desktop  Appskey & 4   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 004

#SingleInstance force
isRunning := false                                                ;---- 用于跟踪脚本是否在运行
timerRunning := false                                          ;-- 用于跟踪定时器是否在运行

F5 & v::                                             
    	Process, Exist, FSCapture.exe                  ; --------检查程序是否在运行
    	if (ErrorLevel) 
{
        	Process, Close, FSCapture.exe                ;---- 如果程序在运行则关闭它
        	isRunning := false                                   ;----------- 更新状态为未运行
        	SetTimer, AutoCloseFSCapture, Off       ;------------------ 关闭定时器
        	timerRunning := false                             ;------------- 更新定时器状态
}
else 
{
        	Run, c:\3\9 FSCapture97\FSCapture.exe , , min ;--- 如果程序没运行则启动它
        	Sleep, 30
	click                                                　　  ;------------- 这个点击动作可以在截图时不显示输入法指示
        	Sleep, 1200
        	SendInput, !+z                                        ;--------------截图快捷键 !+z
       	isRunning := true                                    ;-------- 更新状态为正在运行

        	if (!timerRunning)                                   ;----------- 如果定时器未运行
       {                                          
            	SetTimer, AutoCloseFSCapture, -3000000  ; --------------------------设置一个50分钟的单次定时器
            	timerRunning := true                               ;--- 更新定时器状态为运行中
       }
}
return
;----------------------------------------------------------------------------定时器
AutoCloseFSCapture:
    	Process, Close, FSCapture.exe                ;----------- 自动关闭截图软件
    	isRunning := false                                   ;----------- 更新状态为未运行
    	timerRunning := false                             ;---- 更新定时器状态为未运行
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F5 & v  FSCapture.exe  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 005

Appskey & 5::                                ;---- 后台截图　6000 为间隔6秒  共运行5 次 
run, nircmd  loop 5 6000 savescreenshot "C:\oneD\OneDrive\desktop\~$currtime.HHmm_ss$ ~$loopcount$.png"
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  后台间隔截图 全屏 Appskey & 5  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 006m

;  shift+alt+a      框选画中画       Mouselnc
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  框选画中画 shift+alt+a ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 007m

;  win+Esc           框选OCR         Mouselnc
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  框选OCR win+Esc ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 008

$+#s::                                        ;-------------------系统自带加了一个保存在桌面
	clipboard =
	clipboard = clipboardALL
	Send, {PrintScreen}
sleep,5000
	file := ImagePutFile(clip, "C:\oneD\OneDrive\desktop\" )
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  截图  剪贴板 desktop  +#s  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 010

<!esc::                                     ;------------------------------------ OCR 或截图
    	send, !j                        ;---------------------------------- 暂时关闭 VPN
    	run "D:\ahk1.0\Lib\0 tool\SGScreencapture\screencapture.exe"
    	SetTimer, ReEnableVPN, -14000            ;----------------------------- 设置一个14秒的单次定时器
	return

	ReEnableVPN:
    	send, !u                       ;---------------------------------- 重新启用 VPN
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  截图 OCR <!esc ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 012

;#SingleInstance Force
;#NoEnv
displayNum := 0
visibleState := true

F9 & 9::
	pasteToScreen(){
	if DllCall("IsClipboardFormatAvailable", "UInt", 1)
	displayText(Clipboard)
	If DllCall("IsClipboardFormatAvailable", "UInt", 2)
{
	if DllCall("OpenClipboard", "uint", 0) 
{
	hBitmap := DllCall("GetClipboardData", "uint", 2)
	DllCall("CloseClipboard")
}
	displayImg(hBitmap)
}
	if DllCall("IsClipboardFormatAvailable", "UInt", 15){
	imgFile := Clipboard
	if(hBitmap := LoadPicture(imgFile))
	displayImg(hBitmap)
}
}
	displayText(text)
{
	global
Gui, New, +hwndpasteText%displayNum% -Caption +AlwaysOnTop +ToolWindow -DPIScale
	local textHnd := pasteText%displayNum%
	Gui, Margin, 10, 10
	Gui, Font, s16
	Gui, Add, Text,, % text
	OnMessage(0x201, "move_Win")
	OnMessage(0x203, "close_Win")
	Gui, Show,, pasteToScreen_text
	transparency%textHnd% := 100
	displayNum++
}
	displayImg(hBitmap)
{
	global
Gui, New, +hwndpasteImg%displayNum% -Caption +AlwaysOnTop +ToolWindow -DPIScale
	local imgHnd := pasteImg%displayNum%
	Gui, Margin, 0, 0
	Gui, Add, Picture, Hwndimg%imgHnd%, % "HBITMAP:*" hBitmap
	OnMessage(0x201, "move_Win")
	OnMessage(0x203, "close_Win")
	Gui, Show,, pasteToScreen_img
	local img := img%imgHnd%
ControlGetPos,,, width%imgHnd%, height%imgHnd%,, ahk_id %img%
	scale%imgHnd% := 100
	transparency%imgHnd% := 100
	displayNum++
}
	move_Win()
{
	PostMessage, 0xA1, 2
}
	close_Win()
{
	id := WinExist("A")
	transparency%id% := ""
	scale%id% := ""
	width%id% := ""
	height%id% := ""
	Gui, Destroy
}
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F9+9 贴图  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 013
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    Shift+鼠标滚动   改变粘贴的透明度  ΞΞΞΞΞΞΞΞΞΞ
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    鼠标滚轮改变贴图大小 双击关闭  ΞΞΞΞΞΞΞΞΞΞΞΞΞ

F9 & 0::
	toggleVisibleState()
{
	global visibleState
	if(visibleState){
	WinGet, id, List, pasteToScreen
	Loop, %id%
{
	this_id := id%A_Index%
	WinHide, ahk_id %this_id%
}
	visibleState := false
} 
	else 
{
	DetectHiddenWindows, On
	WinGet, id, List, pasteToScreen
	Loop, %id%
{
	this_id := id%A_Index%
	WinShow, ahk_id %this_id%
}
	DetectHiddenWindows, Off
	visibleState := true
}
}
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F9+0 隐藏或显示所有粘贴   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 014

F9 & -::
	destroyAllPaste()
{
	WinGet, id, List, pasteToScreen
	Loop, %id%
{
	this_id := id%A_Index%
	SendMessage, 0x203,,,, ahk_id %this_id%
}
}
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F9+- 关闭贴图   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 015

F9 & =::
	FileSelectFile, imgFile, 3, C:\oneD\OneDrive\desktop\
	hBitmap := LoadPicture(imgFile)
	displayImg(hBitmap)
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F9+= 打开图并设置为贴图  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 016

F9 & 8::
	Imageshow({image: %clipboardAll%, scale: ["auto", 600]})  ;长自动，宽600
	;Imageshow({image: %clipboardAll%, scale: 2.25})   ; 放大到2.25倍
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    剪贴板内容贴在桌面 放大到1.25倍    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 017

;🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆    截图   操作   🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆
;🎟🎟🎟🎟🎟🎟🎟🎟🎟🎟    显隐   操作   🎟🎟🎟🎟🎟🎟🎟🎟🎟🎟🎟

F1 & y::
send,<!{Enter}
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F1 & y 右键属性   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0001

F5 & 1::
	HideShowTaskbar()
{
   	static SW_HIDE := 0, SW_SHOWNA := 8, SPI_SETWORKAREA := 0x2F
   	DetectHiddenWindows, On
   	hTB := WinExist("ahk_class Shell_TrayWnd")
   	WinGetPos,,,, H
hBT := WinExist("ahk_class Button ahk_exe Explorer.EXE")  ; for Windows 7
   	b := DllCall("IsWindowVisible", "Ptr", hTB)
   	for k, v in [hTB, hBT]
( v && DllCall("ShowWindow", "Ptr", v, "Int", b ? SW_HIDE : SW_SHOWNA) )
   	VarSetCapacity(RECT, 16, 0)
   	NumPut(A_ScreenWidth, RECT, 8)
   	NumPut(A_ScreenHeight - !b*H, RECT, 12, "UInt")
DllCall("SystemParametersInfo", "UInt", SPI_SETWORKAREA, "UInt", 0, "Ptr", &RECT, "UInt", 0)
   	WinGet, List, List
	Loop % List
{
	WinGet, res, MinMax, % "ahk_id" . List%A_Index%
	if (res = 1)
WinMove, % "ahk_id" . List%A_Index%,, 0, 0, A_ScreenWidth, A_ScreenHeight - !b*H
}
}
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F5 & 1  隐藏任务栏   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  0002

F5 & 2::
	ControlGet, q, Hwnd,, SysListView321, ahk_class Progman
If q =
	ControlGet, q, Hwnd,, SysListView321, ahk_class WorkerW
If DllCall("IsWindowVisible", UInt, q)
	WinHide, ahk_id %q%
Else
	WinShow, ahk_id %q%
Return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F5 & 2  隐藏桌面图标    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0003

toggle := false           ; ---------------------定义一个变量来跟踪状态

F5 & -::
if (toggle)             ;检查当前状态，如果为 true，则显示；如果为 false，则隐藏。
{
        	run, nircmd.exe win show class progman                    ; 显示桌面图标
} 
	else 
{
        	run, nircmd.exe win hide class progman                      ; 隐藏桌面图标
}

toggle := !toggle              ;---切换状态使得下次按下 F5.. 时能够执行相反的操作。
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F5 & -  隐.显桌面   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0004

F5 & x::          ;;显示文件
RegRead,value,HKEY_CURRENT_USER,Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\, Hidden
	If(value=1)
	value = 2
	Else
	value = 1
RegWrite, REG_DWORD, HKEY_CURRENT_USER,Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\, Hidden, %Value%
RegWrite, REG_DWORD, HKEY_CURRENT_USER,Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\, ShowSuperHidden, %Value%-1
	PostMessage,0x111,0x7103,0,SHELLDLL_DefView1,A
	return

F5 & k::           ;;显示文件扩展名
RegRead,Value,HKEY_CURRENT_USER,Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\,HideFileExt
	If(value=0)
	value = 1
	Else
	value = 0
RegWrite, REG_DWORD,HKEY_CURRENT_USER,Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\,HideFileExt, %Value%
	PostMessage,0x111,0x7103,0,SHELLDLL_DefView1,A
	return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F5 & k 显示扩展名 F5 & x 显隐文件   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0005

F5 & r::
; 设置注册表路径和值名称
regPath := "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced"
valueName := "IconsOnly"

; 读取当前的 IconsOnly 值
RegRead, currentValue, %regPath%, %valueName%

; 如果读取失败（值不存在），则将值初始化为 0
if (ErrorLevel)
    currentValue := 0

; 切换值：如果当前值是 0 则设置为 1，否则设置为 0
newValue := (currentValue = 0) ? 1 : 0

; 写入新值到注册表
RegWrite, REG_DWORD, %regPath%, %valueName%, %newValue%

 ; 刷新资源管理器以应用更改
;send, ^r
; 使用 COM 对象刷新桌面和文件资源管理器窗口
for window in ComObjCreate("Shell.Application").Windows
{
    if (window.FullName != "")  ; 检查是否是有效的资源管理器窗口
        window.Refresh()
}
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F5 & r  缩略图   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0006

F5 & t::
Send, <!p
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  显示预览窗格   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0007

F5 & 6::
	WinGetActiveTitle, Title
	Title := StrReplace(Title, "Ξ置顶 Ξ")
	ID := WinExist("A")
	WinGet, ExStyle, ExStyle, ahk_id %ID%
	If (ExStyle & 0x8)
{
	WinSet,TopMost,,A
	WinSetTitle, , ,Ξ OFF Ξ
 	SoundPlay, D:\ahk1.0\Lib\0\y2253.mp3
}
	Else
{
	WinSet,TopMost,,A
	WinSetTitle, , ,Ξ 置顶 Ξ
   	SoundPlay, D:\ahk1.0\Lib\0\2.mp3
}
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F5 & 6  窗口置顶   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0008

;🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁    显隐   操作   🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁
;🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆    打开   操作   🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆

F5 & e::
clipboard := ""
    Send {ctrl down}c{ctrl up}
Run, D:\ahk1.0\Lib\0\0000000                 AutoHotkey.chm
sleep, 600
SendInput {alt down}s{alt up}
sleep, 50
SendInput {ctrl down}v{ctrl up}{Enter}
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F5 & e  帮助文档   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00001

F5 & 9::
	Imageshow("D:\ahk1.0\1\1.png")
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F5 & 9  快捷键目录  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00002

F5 & 0::
	Imageshow("D:\ahk1.0\1\2.png")
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F5 & 0  快捷键目录  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00003
 
F1 & k::
{
; 保存当前剪贴板内容
   	clipboardBackup := ClipboardAll
	Clipboard := ""  ; 清空剪贴板
; 复制选中的快捷方式路径
    	Send, ^c
    	ClipWait, 1
if ErrorLevel 
{
        	MsgBox, 未能复制到剪贴板。
        	Clipboard := clipboardBackup  ; 还原剪贴板内容
        	return
}
; 获取快捷方式的目标路径
    	FileGetShortcut, %Clipboard%, shortcutPath
if (shortcutPath != "") {
; 使用资源管理器打开并选中目标文件
        	Run, explorer.exe /select`, %shortcutPath%
;select`：是用于资源管理器中打开包含指定文件的文件夹并选中该文件的参数。
;  , :         逗号用于分隔命令和参数。在这里，它将 select 命令与后面的参数分开。
} 
	else 
{
        	MsgBox, 当前剪贴板内容不是有效的快捷方式。
}
	; 还原剪贴板内容
    	Clipboard := clipboardBackup
    	return
}
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F1 & k 打开快捷方式的文件夹   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00004

^+z:: 
	WinGet, processID, PID, A                      ;--获取当前活动窗口的进程ID
WinGet, exePath, ProcessPath, ahk_pid %processID%    ; 获取可执行文件路径 
	SplitPath, exePath, , fileDir            ; 提取文件夹路径
	Run, %fileDir%            ; 打开文件夹
 	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   打开当前活动窗口的文件夹位置  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00005

F5 & 8::
o=C:\0　　tool\EmEditor\EmEditor.exe
1=D:\ahk1.0\Lib\ahk777.ahk
2=D:\ahk1.0\Ahk1.1.ahk
;3=D:\ahk1.0\Lib\ahk2.ahk

Run,%o% "%1%" "%2%" "%3%"
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F5 & 8   EmEditor打开3文件   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00006

#SingleInstance force                                                          ; 强制加载新的脚本
isRunning := false                  ; 状态变量: isRunning 用于跟踪脚本是否正在运行
Rctrl & 5::
    Process, Exist, v2rayN.exe                                      ; 检查程序是否已经在运行
    if (ErrorLevel)                 ;根据 ErrorLevel 的值来决定是关闭程序还是启动程序
    {
                                                                            ; 如果程序正在运行，则关闭它
        Process, Close, v2rayN.exe
        isRunning := false                                                        ; 更新状态为未运行
    } 
    else 
    {
                                                                        ; 如果程序没有在运行，则启动它
        Run, C:\3\v2rayN-With-Core\v2rayN.exe , , min 
        isRunning := true                                                     ; 更新状态为正在运行
    }
return

;Rctrl & 5::
if (u := !u)
	{
	Process,close,v2rayN.exe
	}
else
	{
    	Run, C:\3\v2rayN-With-Core\v2rayN.exe , , min 
keywait, 5
}
Return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    Rctrl & 5 打开 v2rayN   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00007

Rctrl & t::
TrayIcon_Button("v2rayN.exe", "L")
sleep, 100
send, !l
return 
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    Rctrl & t 打开托盘 v2rayN  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00008

DetectHiddenWindows, On                                 ;------ 启用对隐藏窗口的检测
SetTitleMatchMode, 2                                         ;----------- 设置标题匹配模式

F9 & [::
	Run, "D:\ahk1.0\Lib\SnoMouse.ahk"
     Loop
{
	Sleep, 120000 ; 等待120秒
                                                                             ;----------------------------- 显示确认对话框
	MsgBox, 4,, 关闭 SnoMouse.ahk 请点是
    IfMsgBox, Yes
	{
       	WinClose, SnoMouse.ahk ahk_class AutoHotkey
	}
	break ; 退出循环                                      ;-- 如果选择“否”，则继续循环
}
	return
;-----------------------------------------------------------------------------------
F9 & ]::
       	WinClose, SnoMouse.ahk ahk_class AutoHotkey
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F1 & [ 启动 F1 & ] 退出 SnoMouse  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00009

#SingleInstance force      ; 强制加载新的脚本
isRunning := false         ; 状态变量: isRunning 用于跟踪脚本是否正在运行。
F5 & b::
    Process, Exist, ZoomIt64.exe       ; 检查程序是否已经在运行
    if (ErrorLevel)      ;根据 ErrorLevel 的值来决定是关闭程序还是启动程序，而不再依赖于 isRunning 状态变量。这可以避免因状态更新不及时而导致的需要按两次热键的问题。
    {
                                                                          ; 如果程序正在运行，则关闭它
        Process, Close, ZoomIt64.exe
        isRunning := false     ; 更新状态为未运行
    } 
    else 
    {
                                                                      ; 如果程序没有在运行，则启动它
        Run, D:\ahk1.0\Lib\0 tool\ZoomIt64\ZoomIt64.exe
sleep, 1000
send, ^2
        isRunning := true      ; 更新状态为正在运行
    }
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F5 & b 启动 / 关闭ZoomIt64.exe  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00010

#WinActivateForce
Rctrl & 1::
    ; 获取当前鼠标位置
    MouseGetPos, originalX, originalY

    ; 执行鼠标点击
    SendEvent {click, 1250, 0}
    IfWinNotExist ahk_exe chrome.exe
    {
	;Run "C:\Users\D\AppData\Local\Google\Chrome\Application\chrome.exe", ,max
	Run "C:\Program Files\Google\Chrome\Application\chrome.exe", ,max
        WinActivate
;keywait, Rctrl
    }
    Else IfWinNotActive ahk_exe chrome.exe
    {
       WinActivate
;keywait, Rctrl
;sleep,1000
;Run, nircmd  savescreenshot "C:\Users\D\Desktop\~$currdate.yyyyMMdd$-~$currtime.HHmmss$.png"
    }
    Else
    {
        WinMinimize
;keywait, Rctrl
    }
    ; 将鼠标移动回原来的位置
    MouseMove, originalX, originalY
Return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  打开 chrome  Rctrl & 1 ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00011

Rctrl & 2::
    ; 获取当前鼠标位置
    MouseGetPos, originalX, originalY

    ; 执行鼠标点击
    SendEvent {click, 1250, 0}

    ; 检查 EmEditor 是否存在
    IfWinNotExist ahk_exe EmEditor.exe
    {
        Run "C:\0　　tool\EmEditor\EmEditor.exe", , max
        WinActivate
        KeyWait, Rctrl
    }
    Else IfWinNotActive ahk_exe EmEditor.exe
    {
        WinActivate
        ; KeyWait, Rctrl
    }
    Else
    {
        WinMinimize
        ; KeyWait, Rctrl
    }

    ; 将鼠标移动回原来的位置
    MouseMove, originalX, originalY
Return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   打开 EmEditor  Rctrl & 2 ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00012

Rctrl & 3::
    ; 获取当前鼠标位置
    MouseGetPos, originalX, originalY

    ; 执行鼠标点击
    SendEvent {click, 1250, 0}
    IfWinNotExist ahk_class CabinetWClass
    {
        Run "C:\Windows\explorer.exe"
        WinActivate
;keywait, Rctrl
    }
    Else IfWinNotActive ahk_class CabinetWClass
    {
       WinActivate
;keywait, Rctrl
    }
    Else
    {
        WinMinimize
;keywait, Rctrl
    }
    ; 将鼠标移动回原来的位置
    MouseMove, originalX, originalY
Return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  打开 资源处理器  Rctrl & 3  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00013

CoordMode, Mouse, Window
Rctrl & 4::
WeChat:="ahk_class WeChatMainWndForPC"
WeChat_path:="C:\Program Files\Tencent\WeChat\WeChat.exe" ，max

if ProcessExist("WeChat.exe")=0
{
	Run, %WeChat_path%
WinWait, ahk_class WeChatLoginWndForPC
click, 180, 350
sleep, 4000
click, 180, 350
sleep, 4000
click, 180, 350
}
else
{
	WinGet,wxhwnd,ID,%WeChat%
	if strlen(wxhwnd)=0
	{
		winshow,%WeChat%
		winactivate,%WeChat%
	}
	else
	{
		winhide,%WeChat%
	}
}
return

ProcessExist(exe){		   ;一个自定义函数,根据自定义函数的返回值作为#if成立依据原GetPID
	Process, Exist,% exe
	return ErrorLevel
}
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  打开 微信  Rctrl & 4   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00014

F5 & /::
Run, "C:\Users\kev07\AppData\Local\Programs\Microsoft VS Code\Code.exe"  , , max
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F5 & /  VS Code  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00015

;🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆    打开   操作   🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆🎆
; 💢⭐💢⭐💢⭐💢⭐💢⭐💢⭐    杂类   操作   ⭐💢⭐💢⭐💢⭐💢⭐💢⭐💢⭐💢

F5 & 5::AltTab
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ     F5 & 5  AltTab     ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000001

F6 & d::
	Clip(Format("{:" GetNextCaseFormat() "}", Clip()), true)
	GetNextCaseFormat()
{
   	static i := 0, Formats := ["U", "L", "T"]
   	return Formats[++i > 3 ? i := 1 : i]
}
	Clip(Text="", Reselect="")
{
	Static BackUpClip, Stored, LastClip
If (A_ThisLabel = A_ThisFunc) 
{
	If (Clipboard == LastClip)
	Clipboard := BackUpClip
	BackUpClip := LastClip := Stored := ""
} 
	Else 
{
If !Stored {
	Stored := True
	BackUpClip := ClipboardAll ; ClipboardAll must be on its own line
} 
	Else
	SetTimer, %A_ThisFunc%, Off
	LongCopy := A_TickCount, Clipboard := "", LongCopy -= A_TickCount ; LongCopy gauges the amount of time it takes to empty the clipboard which can predict how long the subsequent clipwait will need
	If (Text = "") 
{
	SendInput, ^c
	ClipWait, LongCopy ? 0.6 : 0.2, True
} 
	Else 
{
	Clipboard := LastClip := Text
	ClipWait, 10
	SendInput, ^v
}
	SetTimer, %A_ThisFunc%, -700
Sleep 20 ; Short sleep in case Clip() is followed by more keystrokes such as {Enter}
If (Text = "")
	Return LastClip := Clipboard
	Else If ReSelect and ((ReSelect = True) or (StrLen(Text) < 3000))
	SendInput, % "{Shift Down}{Left " StrLen(StrReplace(Text, "`r")) "}{Shift Up}"
}
	Return
	Clip:
	Return Clip()
}
	return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F6 & d 大小写 首字母大写  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000002

F5 & ,::
run D:\ahk1.0\Lib\diskeys.ahk
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   锁键盘鼠标 F5 & ,   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000003

~Shift & Wheelup::
; 透明度调整，增加。
WinGet, Transparent, Transparent,A
If (Transparent="")
    Transparent=255
    Transparent_New:=Transparent+15    ;透明度增加速度。
    If (Transparent_New > 254)
                    Transparent_New =255
    WinSet,Transparent,%Transparent_New%,A

    tooltip now: ▲%Transparent_New%`nmae: __%Transparent%  ;查看当前透明度（操作之后的）。
    ;sleep 1500
    SetTimer, RemoveToolTip_transparent_Lwin__2016.09.20, 1500  ;设置统一的这个格式，label在最后。
return

~Shift & WheelDown::
;透明度调整，减少。
WinGet, Transparent, Transparent,A
If (Transparent="")
    Transparent=255
    Transparent_New:=Transparent-15  ;透明度减少速度。
    ;msgbox,Transparent_New=%Transparent_New%
            If (Transparent_New < 30)    ;最小透明度限制。
                    Transparent_New = 30
    WinSet,Transparent,%Transparent_New%,A
    tooltip now: ▲%Transparent_New%`nmae: __%Transparent%  ;查看当前透明度（操作之后的）。
    ;sleep 1500
    SetTimer, RemoveToolTip_transparent_Lwin__2016.09.20, 1500  ;设置统一的这个格式，label在最后。
return
;设置shift &Mbutton直接恢复透明度到255。

shift & Mbutton::
WinGet, Transparent, Transparent,A
WinSet,Transparent,255,A
tooltip ▲Restored ;查看当前透明度（操作之后的）。
;sleep 1500
SetTimer, RemoveToolTip_transparent_Lwin__2016.09.20, 1500  ;设置统一的这个格式，label在最后。
return

removetooltip_transparent_Lwin__2016.09.20:     ;LABEL
tooltip
SetTimer, RemoveToolTip_transparent_Lwin__2016.09.20, Off
return
;---------------shift+滚轮down +10透明度
;--------------------------------shift+滚轮up -10透明度
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  shift+中键按下 复原   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000003

NumpadEnter::reload
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   重启脚本 ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000006

+appskey::
send {Tab}
loop,4
SoundBeep, 12000, 20
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  +appskey   Tab  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000007

<^!z::
send, ^y
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  <^!z   撤消    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000008

;#NoEnv
   ;SendMode Input
   ;SetWorkingDir %A_ScriptDir%
	MoveCycle(Add)
{
	static StepsInCycle = 2                        ;--------------在2种状态间切换
	static SizeCycle = 0
	SizeCycle := Mod(SizeCycle + Add, StepsInCycle)
	if (SizeCycle < 0)
	{
		SizeCycle := SizeCycle + StepsInCycle
	}
	if (Add = 111) {
		SizeCycle = 1
	}
	else if (Add = 222) {
		SizeCycle = 2
	}
	else if (Add = 333) {
		SizeCycle = 3
	}

	if (SizeCycle = 0) {
		MoveWindow(50, 50)
	}
	else if (SizeCycle = 1) {
		MoveWindow(0, 50)
	}
	else if (SizeCycle = 2) {
		MoveWindow(0, 100)
	}
	else if (SizeCycle = 3) {
		MoveWindow(15, 70)

	}
	else if (SizeCycle = 4) {
		MoveWindow(20, 80)
	}
else if (SizeCycle = 5)
	{
		MoveWindow(10, 80)
	}
}

MoveWindow(XP, WP)
{
	; Get current Window
	WinGetActiveTitle, WinTitle
	WinGetPos, X, Y, WinWidth, WinHeight, %WinTitle%

	; Get Taskbar height
	WinGetPos,,, tbW, tbH, ahk_class Shell_TrayWnd

	; Calculate new position and size
	XNew := (A_ScreenWidth * XP / 100)
	WNew := (A_ScreenWidth * WP / 100)
	HNew := (A_ScreenHeight - tbH)
	TopNew := 2

	; MsgBox, %XNew% - %WNew% ; DEBUG
	WinRestore, %WinTitle%
	WinMove, %WinTitle%,, %XNew%, %TopNew%, %WNew%, %HNew%
}

<!z::
	MoveCycle(-1)
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  窗口左半，右半切换 <!z   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000004

;#NoEnv
  ; SendMode Input
  ; SetWorkingDir %A_ScriptDir%
	MoveCycle2(Add)
{
	static StepsInCycle2 = 2                        ;--------------------------------------在2种状态间切换
	static SizeCycle2 = 0
	SizeCycle2 := Mod(SizeCycle2 + Add, StepsInCycle2)
	if (SizeCycle2 < 0)
	{
		SizeCycle2 := SizeCycle2 + StepsInCycle2
	}
	if (Add = 111) {
		SizeCycle2 = 1
	}
	else if (Add = 222) {
		SizeCycle2 = 2
	}
	else if (Add = 333) {
		SizeCycle2 = 3
	}

	if (SizeCycle2 = 0) {
		MoveWindow2(0, 100)
	}
	else if (SizeCycle2 = 1) {
		MoveWindow2(15, 70)
	}
	else if (SizeCycle2 = 2) {
		MoveWindow2(0, 100)
	}
	else if (SizeCycle2 = 3) {
		MoveWindow2(15, 70)

	}
	else if (SizeCycle2 = 4) {
		MoveWindow2(10, 80)
	}
else if (SizeCycle2 = 5) {
		MoveWindow2(0, 80)
	}
}

MoveWindow2(XP, WP)
{
	; Get current Window2
	WinGetActiveTitle, WinTitle
	WinGetPos, X, Y, WinWidth, WinHeight, %WinTitle%

	; Get Taskbar height
	WinGetPos,,, tbW, tbH, ahk_class Shell_TrayWnd

	; Calculate new position and size
	XNew := (A_ScreenWidth * XP / 100)
	WNew := (A_ScreenWidth * WP / 100)
	HNew := (A_ScreenHeight - tbH  / 1.3)
	TopNew := 1

	; MsgBox, %XNew% - %WNew% ; DEBUG
	WinRestore, %WinTitle%
	WinMove, %WinTitle%,, %XNew%, %TopNew%, %WNew%, %HNew%
}

	<!x::
	MoveCycle2(-1)
	return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  < !x  切换窗口  70%·····100%    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000010

if !A_IsAdmin && !RegExMatch(_:=DllCall("GetCommandLineW", "Str"), " /restart(?!\S)")
    RunWait % "*RunAs " RegExReplace(_, "^\"".*?\""\K|^\S*\K", " /restart")
F5 & 7::
send, ^c
sleep, 800
run D:\ahk1.0\Lib\二维码.ahk
sleep, 400
click 122,233
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  二维码  F5 & 7  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000011

!LButton::    ;-- 【Win+鼠标左键】任意移动窗口位置
#LButton::    ;-- 【Win+鼠标右键】任意调整窗口大小
Critical
CoordMode, Mouse
MouseGetPos, x1, y1, id
IfWinNotExist, ahk_id %id%
  return
WinGet, flag, MinMax    ;-- 不操作最大化的窗口
if flag=1
  return
SetWinDelay, 20
WinGetPos, x2, y2, w2, h2
While GetKeyState(SubStr(A_ThisLabel,2),"P")
{
  MouseGetPos, x3, y3
  if A_ThisLabel = !LButton
    WinMove, x3-x1+x2, y3-y1+y2
  else
    WinMove,,,,, x3-x1+w2, y3-y1+h2
}
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  !+左键 移窗口 #+左键 调窗口大小   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000012

    ; Windows messages to monitor
    msg_WM_WTSSESSION_CHANGE = 0x2b1
    msg_WM_POWERBROADCAST    = 0x218

    ; Registry key and value to store the state of the mouse buttons
    reg_KeyName = HKEY_CURRENT_USER\SessionInformation
    reg_ValueName = LeftHandedMouse

    ; Set taskbar tray icon
    Menu, Tray, Icon, shell32.dll, 44 ; Gold star icon
    Menu, Tray, Tip, Swap Mouse Buttons

    ; Initialize
    ; Create an invisile window which is registered to receive WTSRegisterSessionNotification notifications (for lock and unlock messages)
    ; and RegisterPowerSettingNotification notifications (for suspend and wake-up messages)
    Gui,+LastFound
    hwnd:=WinExist()

    ; Register the window for WTSRegisterSessionNotification notifications in order to receive the WM_WTSSESSION_CHANGE messages
    DllCall("Wtsapi32.dll\WTSRegisterSessionNotification","UInt",hwnd,"UInt",0)

    ; Register the window for RegisterPowerSettingNotification notification in order to receive the WM_POWERBROADCAST messages
    ; hHandle is set to the hidden window
    ; PowerSettingGuid is set to GUID_SYSTEM_AWAYMODE
    ; Flags is 0 (DEVICE_NOTIFY_WINDOW_HANDLE) to register for notifications sent using WM_POWERBROADCAST messages
    DllCall("User32.dll\RegisterPowerSettingNotification",hwnd,"98a7f580-01f7-48aa-9c0f-44352c29e5C0",0)

    ; Register function to recieive the WM_WTSSESSION_CHANGE messages
    OnMessage(msg_WM_WTSSESSION_CHANGE,"f_WM_Monitor")

    ; Register functino to receive the WM_POWERBROADCAST messages
    OnMessage(msg_WM_POWERBROADCAST,"f_WM_Monitor")

    ; Set the mouse to the last known state
    RegRead, buttonState, %reg_KeyName%, %reg_ValueName%
    if (ErrorLevel) ; Reistry value not found
    {
        buttonState := DllCall("user32.dll\SwapMouseButton", "UInt", 1) ; Set left-handed mouse
        if buttonState <> 0 ; If the result is non-zero, the mouse was set to left-handed before the above DLL call
        {
            buttonState := 1
        }
        RegWrite, REG_DWORD, %reg_KeyName%, %reg_ValueName%, %buttonState%
    }
    tmpInt := DllCall("user32.dll\SwapMouseButton", "UInt", buttonState)

Return

F5 & .::
    buttonState := DllCall("user32.dll\SwapMouseButton", "UInt", 1) ; Set left-handed mouse
    if buttonState <> 0 ; If the result is non-zero, the mouse was set to left-handed before the above DLL call
    {
        buttonState := 0
        tmpInt := DllCall("user32.dll\SwapMouseButton", "UInt", 0) ; Set right-handed mouse
        ToolTip, Right Handed
    }
    else
    {
        buttonState := 1
        ToolTip, Left Handed
    }
    RegWrite, REG_DWORD, %reg_KeyName%, %reg_ValueName%, %buttonState%

    SetTimer, tRemoveToolTip, -3000 ; Whith negative period, the timer will run only once
Return


; Function to monitor the WM_WTSSESSION_CHANGE and WM_POWERBROADCAST messages
f_WM_Monitor(wParam, lParam, msg)
{

Global reg_KeyName, reg_ValueName
Global msg_WM_WTSSESSION_CHANGE, msg_WM_POWERBROADCAST

    ; Lock or Suspend
    if ((msg = msg_WM_WTSSESSION_CHANGE and wParam = 7) or (msg = msg_WM_POWERBROADCAST and wParam = 4))
    {
        ; Get mouse buttons' state and store it in the registry. Required if the mouse buttons were swapped using the
        ; Control Panel and not by using the script
        buttonState := DllCall("user32.dll\SwapMouseButton", "UInt", 1) ; Note: Sets left-handed mouse
        if buttonState <> 0 ; If the result is non-zero, the mouse was set to left-handed before the above DLL call
            RegWrite, REG_DWORD, %reg_KeyName%, %reg_ValueName%, 1
        else
            RegWrite, REG_DWORD, %reg_KeyName%, %reg_ValueName%, 0
    }

    ; Unlock
    if ((msg = msg_WM_WTSSESSION_CHANGE and wParam = 8) or (msg = msg_WM_POWERBROADCAST and wParam = 7))
    {
        ; Synaptics driver and Windows 10 issues might reset the mouse buttons to right-handed mouse after unlock/wake-up
        ; The timer is to make sure that the state of the mouse buttons is set to what it was before the computer was locked/suspended
        SetTimer, tSetMouseButtons, -1000 ; With negarive period, the timer will run only once
    }
}
; Timers
tRemoveToolTip:
    ToolTip
Return
tSetMouseButtons:
    RegRead, buttonState, %reg_KeyName%, %reg_ValueName%
    tmpInt := DllCall("user32.dll\SwapMouseButton", "UInt", buttonState)
Return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F5 & . 切换鼠标左右键   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000013
 >^b::
if wincc_presses > 0 ; SetTimer 已经启动, 所以我们记录键击.
{
    wincc_presses += 1
    return
}
; 否则, 这是新开始系列中的首次按下. 把次数设为 1 并启动
; 计时器：
wincc_presses = 1
SetTimer, Keywincc, 300 ; 在 400 毫秒内等待更多的键击.
return

Keywincc:
SetTimer, Keywincc, off
if wincc_presses = 1 ; 此键按下了一次.
{
   Click right
sleep,200
Send, wf
Clipboard= %Clipboard%
sleep,200
send,{ctrl down}v{ctrl up}
ClipWait
send, {enter}
}
else if wincc_presses = 2 ; 此键按下了两次.
{
   Click right
sleep,200
Send, w{up 2}{enter}
Clipboard= %Clipboard%
sleep,200
send,{ctrl down}v{ctrl up}
ClipWait
send, {enter}
}
wincc_presses = 0
return
; ΞΞΞΞΞΞΞΞΞΞΞΞ   >^b  单 新建文件夹 双 TxT文件  名为剪贴板   ΞΞΞΞΞΞΞΞΞΞΞΞΞ 000005
F5 & u::
Clipboard =
Send, ^c
Run  "D:\ahk1.0\Lib\0 tool\bat\新建htm覆盖不提示.vbs"
sleep, 900
FileAppend, %clipboard% `n, C:\oneD\OneDrive\desktop\q.htm

 	IfWinNotExist ahk_exe AudioRecorder.exe
{
	Run "C:\3\0\语音合成\录音\录音.exe"  , , max
	WinActivate
}
	Else IfWinNotActive ahk_exe AudioRecorder.exe
{
	WinActivate
}
sleep, 4000
runwait C:\oneD\OneDrive\desktop\q.htm
sleep, 3000
send ^+u
sleep, 300
send ^+{space}
return
; 耳机,扬声器状态都能录，但中途不要切换音频设备。开Vpn也没关系。如失败，不要操作别的，再按一次F5 & u就可以了。
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F5 & u  文字转语音   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000006


`