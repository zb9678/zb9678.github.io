`b105(timeout = 400)
{
	tout := timeout/1000
	key := RegExReplace(A_ThisHotKey,"[\*\~\$\#\+\!\^]")
	Loop
	{
     	 t := A_TickCount
      	KeyWait %key%
      	Pattern .= A_TickCount-t > timeout
      	KeyWait %key%,DT%tout%
      	If (ErrorLevel)
	Return Pattern
	}
}
;-----------------------------------------------------------------------------------
+F12::
   p := b105()

          If (p = "0")
	Run ms-settings:network-proxy            ;------------------------- 代理 1

   Else If (p = "00")
	Run control.exe sysdm.cpl`,`,3               ;---------------------环境变量 2

   Else If (p = "000")
	Run compMgmtLauncher                      ;------------------ 计算机管理 3

   Else If (p = "0000")
	run devmgmt.msc                                  ;------------------ 设备管理器 4
		
   Else If (p = "1")　
Run mmc            

   Else
{
	Run dcomcnfg                                     ;------------------------组件服务 6  次数5次以上
}
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F12  代理 变量 管理 控制台 组件服务   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000007
+F11::
   p := b105()

          If (p = "0")
	Run control                                            ;---------------------控制面板 1

   Else If (p = "00")
Run, %A_ComSpec% /k ipconfig  ; 打开 CMD 并直接运行 ipconfig   ; ipconfig 2
		
   Else If (p = "000")　　
	Run gpedit.msc                                      ;-----------------------组策略 3

   Else If (p = "0000")
	Run ncpa.cpl                                          ;---------------------网络连接 4

   Else If (p = "1")　　
{
	Run shrpubw
	Run fsmgmt.msc                                    ;-------------------共享文件夹 5  长按
}
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ F11 控制面板 IP 组策略 网络连接 共享 ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000008

#Persistent
SetWorkingDir %A_ScriptDir%

~CapsLock::
if (A_PriorHotkey != "CapsLock" or A_TimeSincePriorHotkey > 400)
     {
    ; 这是第一次点击
    KeyWait, CapsLock
    KeyWait, CapsLock, D T0.4   ;等待400毫秒看是否会有第二次点击
    if (ErrorLevel)
{
        Send, !p                                                        ;------------------------- 单击
        Sleep, 100
        Send, s
}
    else
	{
        ; 可能是双击或三击 双击后有轻微的延迟，等1小段时间来确定是否有第3次点击
        KeyWait, CapsLock
        KeyWait, CapsLock, D T0.4
        if (ErrorLevel)
{
            Send, !p                                                    ;------------------------- 双击
            Sleep, 100
            Send, 9
}
        else
{
            KeyWait, CapsLock                                  ;------------------------- 三击
            Send, !p
            Sleep, 100
            Send, 0
}
	}
     }
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  浏览器  1全局 2auto 3直连  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000009

 >^q::
ControlGetFocus, control, A
SendMessage, 0x115, 2, , %control%, A
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  >^q 上一页  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000010

 >^e::
ControlGetFocus, control, A
SendMessage, 0x115, 3, , %control%, A
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  >^e 下一页  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000011
F4 & 0::
loop,10
{
var := 0
InputBox, time, KevZ:计时器 请输入一个时间__分钟
time := time*60000
Sleep,%time%
loop,26
{
var += 180
SoundBeep, var, 900
;SoundPlay, %A_WinDir%\Media\Ring10.wav
}
msgbox 时间到！！！! ! ! ! ! ! !
return
}
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  计时器 F4 & 0  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000011

#IfWinActive ahk_class WindowsForms10.Window.8.app.0.2bf8098_r7_ad1
:*b:++::610712一2550800一122一018{Bs 13}{left 2}{Bs}{left 4}{Bs 4}{Enter}   ;BS 回退13，left 左移 Enter确认 输入+2成功替换
#IfWinActive
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   keepast   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01 

; 💢⭐💢⭐💢⭐💢⭐💢⭐💢⭐    杂类   操作   ⭐💢⭐💢⭐💢⭐💢⭐💢⭐💢⭐💢
; ➰➰➰➰➰➰➰➰➰➰   选行   选段   ➰➰➰➰➰➰➰➰➰➰➰

<!1::
send, {home}{shiftdown}{end}{shiftup}^c
Return
<!q::
Send +{Home}^c
Return
<!a::
Send {shift down}{End down}{End up}{shift up}^c
Return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  <!1 复整行　<!q 到行首  <!a 到行尾   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0000001

<!2::
send, {home}{shiftdown}{end}{shiftup}^v
Return
<!w::
Send +{Home}^v
Return
<!s::
Send {shift down}{End down}{End up}{shift up}^v
Return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  <!2 粘整行  <!w 光标前 <!s 光标后     ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0000002

<!3::
send, {home}{shiftdown}{end}{shiftup}^x
Return
<!e::
Send +{Home}^x
Return
<!d::
Send {shift down}{End down}{End up}{shift up}^x
Return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  <!3 剪整行  <!e 光标前   <!d 光标后    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0000003

<#1::
send, {home}{shift down}{end}{shift up}
Return
<#q::
Send +{Home}
Return
<#a::
Send {shift down}{End down}{End up}{shift up}
Return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  <#1选整行　<#q到行首 <#a到行尾    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0000004

<#2::
send !{End}+!{home}
Return
<#w::
Send ^+{home}
Return
<#s::
Send ^+{End}
Return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  <#2 选整段  <#w光标前 <#s光标后    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0000005

<#3::
send, {home}{shiftdown}{end}{shiftup}{delete}
Return
#If (WinActive("ahk_class XLMAIN") or WinActive("ahk_class OpusApp") or WinActive("ahk_exe Notepad3.exe") or WinActive("ahk_exe EmEditor.exe") or WinActive("ahk_class Chrome_WidgetWin_1"))
<#e::
Send +{Home}{delete}
Return
#IfWinActive
<#d::
Send {shift down}{End down}{End up}{shift up}{delete}
Return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  <#3 删整行 <#e 光标前 <#d 光标后   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0000006

; ➰➰➰➰➰➰➰➰➰➰   选行   选段   ➰➰➰➰➰➰➰➰➰➰➰
; 🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵   滚动   速度   🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵

#If ( WinActive("ahk_exe chrome.exe")  or WinActive("ahk_exe WeChatAppEx.exe")  or WinActive("ahk_exe Typora.exe") or WinActive("ahk_exe Notepad3.exe") or WinActive("ahk_exe EmEditor.exe") or WinActive("ahk_exe Joplin.exe"))
www=0
F2 & F1::
{
www:=!www
If(www=0)
{
SetTimer, aaaa, Off
SetTimer, bba, Off

}
ELSE
	{
	SetTimer, aaaa, 50	 ;滚动速度
	}
}
Return
	aaaa:
	{
	ControlGetFocus, control, A
	SendMessage, 0x115, 0, 0, %control%, A
	;SendMessage, 0x115, 2, , %control%, A
	}
Return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F2 & F1 快速向上滚动   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000001

F2 & F3::
{
	www:=!www
	If(www=0)
	{
	SetTimer, bba, Off
	SetTimer, aaaa, Off
	}
ELSE
	{
	SetTimer, bba, 50	;滚动速度
	}
}
Return
	bba:
	{
	ControlGetFocus, control, A
	SendMessage, 0x115, 1, 0, %control%, A
	;SendMessage, 0x115, 3, , %control%, A
	}
Return
#IfWinActive
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F2 & F3 快速向下滚动   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000002

F2 & Esc::
{
www:=!www
If(www=0)
{
SetTimer, aaa, Off
SetTimer, bb, Off
}
ELSE
	{
	SetTimer, aaa, 1000	 ;滚动速度
	}
}
Return
	aaa:
	{
	ControlGetFocus, fcontrol, A
	Loop 1                                                          ; 行数
	SendMessage, 0x115, 0, 0, %fcontrol%, A
	}
Return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F2 & Esc 缓慢向上滚动   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000003

#ifwinactive
www=0

F2 & F4::
{
	www:=!www
	If(www=0)
	{
	SetTimer, bb, Off
	SetTimer, aaa, Off
	}
ELSE
	{
	SetTimer, bb, 1000	;滚动速度
	}
}
Return
	bb:
	{
	ControlGetFocus, fcontrol, A
	Loop 1                                     ; 行数
	SendMessage, 0x115, 1, 0, %fcontrol%, A
}
Return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F2 & F4 缓慢向下滚动   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000004

; 🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵   滚动   速度   🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵
;🎵🎵🎵🎵🎵🎵🎵🎵🎵🎵    颜色   坐标   🎵🎵🎵🎵🎵🎵🎵🎵🎵🎵🎵

F5 & o::
	MouseGetPos, mouseX, mouseY
PixelGetColor, color, %mouseX%, %mouseY%, RGB ; 调用 PixelGetColor 函数，获得 RGB 值，并赋值给 color                     
StringRight color,color,6    ; 截取 color（第二个 color）右边的6个字符，因为获得的值是这样的：0x8700FF，一般我们只需要 8700FF 部分。把截取到的值再赋给 color（第一个 color）。

	clipboard = #%color%        ;--------------------------------- 添加了 #
	tooltip, %clipboard%          ;--------------- 把 color 的值发送到剪贴板
	sleep 2000
	tooltip,
	return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F5 & o 获得 RGB 值   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000000001

F5 & P::  
    	ClipSaved := ClipboardAll        ; ------------------保存当前剪贴板内容
    	Clipboard := ""                         ;-- 清空剪贴板以确保后续操作的准确性
	Send ^c  
    	ClipWait                                    ; ------------------等待剪贴板内容更新
	color := Clipboard                    ;------------------ 获取剪贴板中的色值
    	;Clipboard := ClipSaved           ;----------------------- 恢复剪贴板内容

    ; 检查颜色格式并转换为 RGB
    if (SubStr(color, 1, 1) = "#") {
        color := SubStr(color, 2)  ; 去掉 "#"
    }
    
    if (StrLen(color) = 6) {
        ; 使用 AutoHotkey 内置的十六进制转换
        r := "0x" SubStr(color, 1, 2)
        g := "0x" SubStr(color, 3, 2)
        b := "0x" SubStr(color, 5, 2)

Gui, New, +Escape +AlwaysOnTop, Color Preview          ; 创建 GUI 窗口以显示颜色，并启用 Esc 关闭功能
        	Gui, Color, % "0x" color  ; 设置背景颜色为获取的颜色        

        	Gui, Add, Text, Center, #%color%）
        	Gui, Font, s14 Bold  ; 设置字体大小和样式
Gui, Show, w200 h200, Color Preview    ; 设置窗口大小为正方形 200x200 像素
} 
	else 
{
        	MsgBox, Invalid color format. Please use #RRGGBB.
}
	return
	GuiClose:
	GuiEscape:
	Gui, Destroy
	return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F5 & p 显示颜色  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000000002

	autostart:=1
	autostartLnk:=A_StartupCommon . "D:\ahk1.0\Lib\se.ahk"
F5 & [::

	if(autostart)
{
    	IfExist, % autostartLnk
{
        	FileGetShortcut, %autostartLnk%, lnkTarget
        	if(lnkTarget!=A_ScriptFullPath)
FileCreateShortcut, %A_ScriptFullPath%, %autostartLnk%, %A_WorkingDir%
}
	else
{
FileCreateShortcut, %A_ScriptFullPath%, %autostartLnk%, %A_WorkingDir%
}
}
	else
{
    	IfExist, % autostartLnk
{
       	FileDelete, %autostartLnk%
}
}
;----------------------------------------------------------------------------------
WinMoveZ(hWnd, C, X, Y, W, H, Redraw:=0) 
{ ;  WinMoveZ v0.5 by SKAN on D35V/D361 @ tiny.cc/winmovez
Local V:=VarSetCapacity(R,48,0), A:=&R+16, S:=&R+24, E:=&R, NR:=&R+32, TPM_WORKAREA:=0x10000
C:=( C:=Abs(C) ) ? DllCall("SetRect", "Ptr",&R, "Int",X-C, "Int",Y-C, "Int",X+C, "Int",Y+C) : 0
DllCall("SetRect", "Ptr",&R+16, "Int",X, "Int",Y, "Int",W, "Int",H)
DllCall("CalculatePopupWindowPosition", "Ptr",A, "Ptr",S, "UInt",TPM_WORKAREA, "Ptr",E, "Ptr",NR)
X:=NumGet(NR+0,"Int"),  Y:=NumGet(NR+4,"Int")
Return DllCall("MoveWindow", "Ptr",hWnd, "Int",X, "Int",Y, "Int",W, "Int",H, "Int",Redraw)
}
;----------------------------------------------------------------------------------
	#NoEnv
	#SingleInstance, Force
	CoordMode, Mouse, Screen
	CoordMode, Pixel, Screen

Gui New, -Caption  +Escape +Border +hWndhWnd +Disabled +AlwaysOnTop
	Gui, Margin, 15, 70         ; ----------------------------------宽度与高度
Gui, Add, Edit, w50 Center  yellow   ;文字左右居中 Center, yellow  加上逗号则上下居中
	Gui, Show
	WinGetPos, X, Y, W, H, ahk_id %hWnd%
	PX:=X, PY:=Y
	Loop
{
  	MouseGetPos, X, Y
  	If ! (X=PX and Y=PY)
{
      	WinMoveZ(hWnd, 96, X, Y, W, H), PX:=X, PY:=Y
      	PixelGetColor, C, %X%, %Y%, RGB
      	Gui, Color, % PC:=C
      	GuiControl,,Edit1, % Format("{:06X}",C)
}
  	Sleep 50
}
	return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F5 & [  颜色值 鼠标跟随  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000000003

F5 & ]::
	MouseGetPos, xpos, ypos
	clipboard = %xpos%,%ypos%
	a = %xpos%_%ypos% 	;-------------------------a = 鼠标位置`(X,Y`)
	tooltip, %a%
	return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   获取当前鼠标指针的坐标   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000000004

;🎵🎵🎵🎵🎵🎵🎵🎵🎵🎵    颜色   坐标   🎵🎵🎵🎵🎵🎵🎵🎵🎵🎵🎵
; 🚧 🚧 🚧 🚧 🚧 🚧 🚧 🚧🚧    上传   图库   🚧 🚧 🚧 🚧 🚧 🚧 🚧 🚧🚧   

F1 & z::
    ; 显示上传中提示
    Text := "⭕ 上传图片中 ⭕"
    btt(Text, 600, 0, , "Style4")
    ; 运行 upgit 上传命令，将 URL 复制到剪贴板
    Run "C:\3\picgo-croe\upgit.exe" :clipboard -o clipboard,, hide      ; -f markdown
    ; 等待上传完成
    Sleep, 5000
    ; 关闭上传提示
    btt()
    ; 获取上传后的剪贴板内容
    Clip := Clipboard
    ; 确保剪贴板不为空
    if (Clip != "") {
        ; 删除第 22 到 27 位的子字符串
        StringReplace, Clip, Clip, % SubStr(Clip, 22, 6), , All
        ; 将修改后的内容格式化为 HTML 并更新到剪贴板
        Clipboard := "<p align='center'><img src=""" Clip """ style='width:400px;'><br><br>"
    }
    return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & z  上传截图到github/img  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  000001

F1 & x::
Text= ⭕       上传图片中     ⭕ 
btt(Text,600,0,,"Style4") 
RunWait, cmd /c "picgo u",, hide
Sleep, 9000
btt()
; 获取上传后的剪贴板内容并删除换行符
Clip := StrReplace(Clipboard, "`n", "")                  ;没有这２步剪贴板中的html分换行成２段．
Clip := StrReplace(Clip, "`r", "")
; 确保剪贴板不为空
if (Clip != "") 
    ; 将修改后的内容格式化为 HTML 并更新到剪贴板
    Clipboard := "<p align='center'><img src=""" Clip """ style='width:400px;'><br><br>"
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & x  上传截图到github/img  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  000002

F1 & c::       
         run, https://picx.xpoet.cn/#/upload    ;需要先在浏览器上将窗口设为67%
         sleep, 4000
click, 1400, 255
	sleep, 1000
	send, ^v
    	Sleep, 100
	send, ^s
    	Sleep, 3000
clipboard = <p align = "center"><img src="%clipboard%" style="width:400px;"><br><br>
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & c  上传截图到图库   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  000003

F1 & v::       
	run, https://tuku.zbb07.us.kg
	;run, https://tuku.zcr07.us.kg
    	;run, https://tu.k07.us.kg         ;需要先在浏览器上将窗口设为67%
	;run, https://tu.w07.us.kg
	;run, https://tu.n06.us.kg
	;run, https://tu.z07.us.kg
	sleep, 7000
Click, 320, 370, 1, 6, ahk_class Chrome_WidgetWin_1  ; 点击左键
    	Sleep, 1000
send, ^v
    	Sleep, 1000  
    	ControlClick, x1160 y505, ahk_class Chrome_WidgetWin_1
    	Sleep, 9500

    ; 使用 ControlClick 模拟鼠标点击特定位置
    ControlClick, x480 y609, ahk_class Chrome_WidgetWin_1
    Sleep, 100

clipboard = <p align = "center"><img src="%clipboard%" style="width:600px; height:400px;">

return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & v  上传截图到图库    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  000004

F1 & b::
Text= ⭕       上传图片中     ⭕ 
btt(Text,600,0,,"Style4") 
send ^c
sleep, 2000
RunWait, cmd /c "picgo u"
,, hide
return
sleep, 9000
btt()​
clipboard = <p align = "center"><img src="%clipboard%" style="width:400px;"><br><br>
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & b  上传剪贴板中的文件  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  000005

F1 & n::                                                                  ;---------------------文件上传
	clipboard = youapig
	send, {F2}
sleep, 100           ;------------------因为文件名不能带中文所以先改名为youapig
	send, {ctrl down}v{ctrl up}{enter}
sleep, 100
	Send, {ctrl down}c{ctrl up}
sleep, 100
	RunWait, "upgit.exe" :clipboard-files
	, ,hide
sleep, 100
	send, ^z
;Run, cmd /c C:\3\picgo-croe\upgit.exe :clipboard-files
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & n  上传剪贴板中的文件  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  000006

; 🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧  上传   图库    🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧
; 🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞  光标   操作    🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞

AppsKey & w::Send {Up}
	AppsKey & s::Send {Down}
		AppsKey & a::Send {Left}
			AppsKey & d::Send {Right}
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    adws 上 下 左 右  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0000001

AppsKey & q:: Send, {Bs}
	AppsKey & e:: Send, {delete}
		AppsKey & f:: Send, {Enter}
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    q 退格 e 删除 f 回车   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0000002

AppsKey & g::
	Send {End}
	Send {Enter}
	Return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    AppsKey & g 任意位置回   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 0000004



; 🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞  光标 鼠标  🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞
; 🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞 快捷  搜索  🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞

F1 & 1::
send,{ctrl down}c{ctrl up}
sleep,200
ClipWait

  	Run, "C:\3\Everything-1.5.0.1356a.x64\Everything64.exe"  -s "%clipboard%"

return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F1 & 1 用Evething搜索选中的文字   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000001

/*
#IfWinActive ahk_exe chrome.exe or ahk_exe EmEditor.exe     ;只对chrome  EmEditor 起作用
F1::return                                         ; 覆盖单独按下 F1 的功能，不执行任何操作
F1 & 2::                                            ; 打开谷歌翻译，回车激活切换中英
Click, 1400,170  , Right
	Click Right
	Send {T}{enter}
Click, 1400,170
return
#IfWinActive                                     ; 结束限制
*/
;-----------------------------------------------------------------------------------

#If (WinActive("ahk_exe chrome.exe") or WinActive("ahk_exe EmEditor.exe"))
F1::return  ; 禁用 F1 的单独功能
F1 & 2:: 
Click, 1400,170  , Right
	Click Right
	Send {T}{enter}
Click, 1400,170
return
#If  ; 结束限制
;如果你的条件比较简单且仅仅是检查窗口，#IfWinActive 完全可以满足需求。
;如果你需要更复杂的条件判断，下面这种  #If 更加灵活且强大。
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  谷歌翻译 F1 & 2  中/ 英  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000002 

F1 & 3::
; 复制当前选中的文本
send, ^c
sleep, 100

; 启动 Mobipocket Reader，如果已经运行则激活窗口
if WinExist("ahk_class MobiDesktopReader")
{
    WinActivate
}
else
{
    run, "C:\3\4\9 MobipocketReader_6.2.exe"
}

; 等待 Mobipocket Reader 窗口存在，最多等待10秒
WinWait, ahk_class MobiDesktopReader, , 10000
if ErrorLevel
{
    MsgBox, 程序未能在10秒内启动。
    return
}

; 等待窗口激活
WinWaitActive, ahk_class MobiDesktopReader, , 1000
if ErrorLevel
{
    MsgBox, 窗口未能在1秒内激活。
    return
}

; 将焦点设置到搜索框控件
ControlFocus, Edit1, ahk_class MobiDesktopReader
sleep, 100  ; 等待焦点设置生效

; 模拟鼠标点击搜索框
ControlClick, Edit1, ahk_class MobiDesktopReader
sleep, 100  ; 等待点击生效

; 清空搜索框内容
ControlSetText, Edit1,, ahk_class MobiDesktopReader
sleep, 100  ; 等待清空生效

; 确保剪贴板内容是干净的
clipboard := Trim(clipboard)

; 使用 ControlSend 粘贴剪贴板内容并发送 Enter 按键
ControlSend, Edit1, ^v, ahk_class MobiDesktopReader
sleep, 100  ; 等待粘贴生效

; 发送 Enter 按键进行搜索
ControlSend, Edit1, {Enter}, ahk_class MobiDesktopReader
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & 3 Mobi   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000003

F1 & 4::
	Send, {ctrl down}c{ctrl up}
	KeyWait F1
	Run https://www.baidu.com/s?ie=UTF-8&wd=%clipboard%
	return
 ; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F1 & 4 用百度搜索选中的文字  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000004

F1 & 5::
  	Send, {ctrl down}c{ctrl up}
	KeyWait F1
	Run http://www.google.com.tw/search?hl=zh-TW&q=%Clipboard%
	return
 ; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F1 & 5 用谷歌搜索选中的文字  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000005

F1 & 6::
	send, ^c
	sleep,100
	run, "C:\3\4\9 MobipocketReader_6.2.exe"
	WinWait, ahk_class MobiDesktopReader, , 15000   ; 等待 Mobipocket Reader 窗口存在，最多等待15秒
if ErrorLevel
{
    MsgBox, 程序未能在15秒内启动。
    return
}
	send, {NumpadUp}
	WinWaitActive, ahk_class MobiDesktopReader, , 4000     ; 等待窗口激活
if ErrorLevel
{
    MsgBox, 窗口未能在1秒内激活。
    return
}
	send, {enter}
	sleep, 100
	send, ^v{enter}
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & 6 Mobi   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000006

F1 & 7::
	Send, {ctrl down}c{ctrl up}
 	 Runwait https://transmart.qq.com/zh-CN/index?sourcelang=en&targetlang=zh&source=%clipboard%
	WinWait, ahk_class Chrome_WidgetWin_1, , 15000  
	return
 ; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F1 & 7 腾讯翻译   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000007

F1 & 8::
	Send, {ctrl down}c{ctrl up}
	KeyWait F1
	sleep,20
  	Run  http://youtube.com/results?q=%clipboard%
	return
 ; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F1 & 8  youtube  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000008

F1 & 0::
	Send, {ctrl down}c{ctrl up}
 	Runwait https://fanyi.baidu.com/mtpe-individual/multimodal?aldtype=23#/en/zh/%clipboard%
	WinWait, ahk_class Chrome_WidgetWin_1, , 15000  
	return
 ; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F1 & 0 百度翻译     ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000009

F1 & =:: 
	Send, {ctrl down}c{ctrl up}   
sleep, 400
	KeyWait F1                         
 	 Runwait https://transmart.qq.com/zh-CN/index
	sleep, 3000
	Send, {ctrl down}v{ctrl up}                                                               
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F1 & = 腾讯翻译     ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000009

F1 & 9::
	Send, {ctrl down}c{ctrl up}
		KeyWait F1
	sleep,20
  	Run  https://zh.wikipedia.org/wiki/Special:Search/%clipboard%
	  	return
 ; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & 9  wiki   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000010

F1 & -::      
	Send, {ctrl down}c{ctrl up}
	send, #!/     
	KeyWait F1
	;sleep,2000                        
  	Run https://www.deepl.com/translator?q=Adds%20shortcuts%20to%20increase%2Fdecrease%20font%20size#en/zh/%clipboard%  
	sleep,16000
	send, #!/  
  	return
 ; 🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁🍁      F1 & 0  DeepL翻译 需全局

; 🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞 快捷  搜索  🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞🎞
; 🎼🎼🎼🎼🎼🎼🎼🎼🎼🎼 关机  重启  🎼🎼🎼🎼🎼🎼🎼🎼🎼🎼🎼🎼

F4 & z::
Run, nircmd speak text "确定注销，请点是" 0 90
Run, nircmd.exe cmdwait 100 qboxcom ".............注  销............." "  注意：保存文件" exitwin logoff
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F4 & z 注销    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000000001
F4 & c::
Run, nircmd speak text "确定重启 请点是" 0 90
Run, nircmd.exe  cmdwait 100 qboxcom ".............重  启............." "  注意：保存文件" exitwin reboot
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F4 & c 重启    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000000002

F4 & g::
Run, nircmd speak text "确定关机 请点是" 0 90
Run, nircmd.exe cmdwait 100 qboxcom ".............关  机............." "  注意：保存文件" exitwin poweroffr
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F4 & g 关机   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000000003

F4 & d::
Run, nircmd speak text "进入待机 请点是" 0 90
Run, nircmd.exe cmdwait 100 qboxcom ".............待　机............" "  睡眠：注意保存文件" standby
sleep, 5000
send, y
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F4 & d 待机   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000000004

F4 & x::
Run, nircmd speak text "确定休眠 请点是" 0 90
Run, nircmd.exe cmdwait 100 qboxcom ".............休　眠............." "  注意：保存文件" hibernate
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F4 & q 重启资源管理器   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000000005

F4 & q::
Run, nircmd speak text "重启资源管理器" 0 90
sleep, 2000
process,close,explorer.exe
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F4 & q 重启资源管理器   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000000006

F4 & p::
Run, nircmd speak text "关屏" 0 90
Run, nircmd.exe cmdwait 2000 monitor off
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    F4 & p 关屏   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000000007

; 🎼🎼🎼🎼🎼🎼🎼🎼🎼🎼 关机  重启  🎼🎼🎼🎼🎼🎼🎼🎼🎼🎼🎼🎼
; 🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️ 文档  编辑  🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️

;     ::a111::ā        a111按下空格后　ā 　　ā后有１个空格    sa111 空格无法替换　　　不能有前缀
;     :?:a111::ā       a111按下空格后　ā 　    ā后有１个空格     sa111 空格完成替换　　  可有前缀

;     :o:a111::ā      a111按下空格后　ā   　   ā后无空格           sa111 空格无法替换        非自动　去除后面的空格
;     :*:a111::ā       a111自动替换为　ā　　  ā后无空格           sa111 空格无法替换　　　自动　 去除后面的空格

:*?:a111::ā
:*?:a222::á
:*?:a333::ǎ
:*?:a444::à
:*?:e111::ē
:*?:e222::é
:*?:e333::ě
:*?:e444::è
:*?:o111::ō
:*?:o222::ó
:*?:o333::ǒ
:*?:o444::ò
:*?:i111::ī
:*?:i222::í
:*?:i333::ǐ
:*?:i444::ì
:*?:u111::ū
:*?:u222::ú
:*?:u333::ǔ
:*?:u444::ù
:*?:v111::ǖ
:*?:v222::ǘ
:*?:v333::ǚ
:*?:v444::ǜ
:*?:v555::ü
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ    aoeiuü   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01

:*?:``m::<br>
:?*:m``::<>{left}

:?*:9'::(){left}
:?*:0'::（）{left}

:?*:['::[]{left}
:?*:]'::{{}{}}{left}

:?*:-'::【】{left}
:?*:='::〖〗{left}
:?*:8'::《》{left}
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   `m::<br> ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 02

:*:.'::。
:*:,'::，

:*::'::：
:*:`;'::；

:*:`/``::、  
:*:.``:: •{space}

:*:,``::……
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   。，：；、 • ……   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 03 

; 🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️ 文档  编辑  🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️🕸️
;🎁🎁🎁🎁🎁🎁🎁🎁🎁🎁  颜色  处理  🎁🎁🎁🎁🎁🎁🎁🎁🎁🎁🎁🎁

{
    ; F6 & R 红色        ;ROYGQBP WETUI
    F6 & r::b205("#f20c00")

    ; F6 & O 橙色                       
    F6 & o::b205("#ec6800")

; F6 & y 暗红色
    F6 & y::b205("#fff143")

; F6 & g 亮绿色
    F6 & g::b205("#00e500")

; F6 & q 兰绿色
    F6 & q::b205("#177cb0")

    ; F6 & B 浅蓝色
    F6 & b::b205("#44cef6")

; F6 & p 暗紫色
    F6 & p::b205("#b61aae")

; F6 & w 绿色
    F6 & w::b205("#bce672")

; F6 & e 绿色
    F6 & e::b205("#955539")

; F6 & t 兰绿色

    F6 & t::b205("#d7003a")

; F6 & u 深紫色
    F6 & u::b205("#ff0097")

; F6 & i 紫色
    F6 & i::b205("#ff461f")
}

; 快捷增加字体颜色
b205(s){
      clipboard := ""
    SendInput,^x
sleep,100
	clipboard = <span style="color: %s%; font-size:18px">%clipboard%</span>
 	SendInput {ctrl down}v{ctrl up}
	;Send {Left 7} ; 光标跟随到文本
}
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & O 橙色   joplin字体颜色   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 07 

{
; F7 & q 兰绿色
    F7 & q::b204("#177cb0")

; F7 & w 绿色
    F7 & w::b204("#bce672")

; F7 & e 绿色
    F7 & e::b204("#955539")

; F7 & R 红色
    F7 & r::b204("#f20c00")

; F7 & t 兰绿色
    F7 & t::b204("#d7003a")

; F7 & y 暗红色
    F7 & y::b204("#fff143")

; F7 & u 深紫色
    F7 & u::b204("#ff0097")

; F7 & i 紫色
    F7 & i::b204("#ff461f")

; F7 & O 橙色      ; ORBPYGMST
    F7 & o::b204("#ec6800")

; F7 & p 暗紫色
    F7 & p::b204("#b61aae")

; F7 & B 浅蓝色
    F7 & b::b204("#44cef6")

; F7 & G 亮绿色
    F7 & g::b204("#00e500")
}

; 快捷增加字体颜色
b204(s){
      clipboard := ""
    SendInput,^x
sleep,100
	clipboard = <span style="font-family:KaiTi; font-size:30px; color: %s%">%clipboard%</span>
	SendInput {ctrl down}v{ctrl up}
	;Send {Left 7} ; 光标跟随到文本
}
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F7 & O 橙色   joplin字体颜色   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 08 

    ; F8 & q 兰绿色       ;   QWERTYUIOP  BG
    F8 & q::b203("#177cb0")

; F8 & w 绿色
    F8 & w::b203("#426666")

; F8 & e 绿色
    F8 & e::b203("#955539")

    ; F8 & R 红色
    F8 & r::b203("#f20c00")

; F8 & t 兰绿色
    F8 & t::b203("#d7003a")

; F8 & y 暗红色
    F8 & y::b203("#fff143")

; F8 & u 兰绿色
    F8 & u::b203("#ff0097")

; F8 & i 紫色
    F8 & i::b203("#ff461f")

    ; F8 & O 橙色
    F8 & o::b203("#ec6800")

; F8 & p 暗紫色
    F8 & p::b203("#b61aae")

    ; F8 & B 浅蓝色
    F8 & b::b203("#44cef6")

; F8 & g 暗绿色
    F8 & g::b203("#00e500")

; 快捷增加字体颜色
b203(s)
{
    clipboard := ""
    SendInput,^x
sleep,100
    SendInput, {TEXT}<span style="font-family:LiSu; font-size:24px; color: #2E3138; background: %s%">%clipboard%</span>
    Send {Left 25}{home}
}                                             ;  ------------------------------------- r t y o p     g b     m s
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F8 & O 橙色 Tyora 背景色   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 09 

; F9 & q 兰绿色       ;   QWERTYUIOP  BG
    F9 & q::b202("#177cb0")

; F9 & w 绿色
    F9 & w::b202("#426666")

; F9 & e 绿色
    F9 & e::b202("#955539")

    ; F9 & R 红色
    F9 & r::b202("#f20c00")

; F9 & t 兰绿色
    F9 & t::b202("#d7003a")

; F9 & y 暗红色
    F9 & y::b202("#000000")

; F9 & u 兰绿色
    F9 & u::b202("#ff0097")

; F9 & i 紫色
    F9 & i::b202("#ff461f")

    ; F9 & O 橙色
    F9 & o::b202("#ec6800")

; F9 & p 暗紫色
    F9 & p::b202("#b61aae")

    ; F9 & B 浅蓝色
    F9 & b::b202("#44cef6")

; F9 & g 暗绿色
    F9 & g::b202("#00e500")

; 快捷增加字体颜色
b202(s)
{
   clipboard := ""
    SendInput ^x
sleep,100
          SendInput, {TEXT}<table><td bgcolor=%s%><font size = '4'></font>%clipboard%<td bgcolor=#2E3138></table>
a := "1"
;Send {Left 8}%a%{Left 20}{home}-{Space}
Send {Left 8}%a%{home}{up}-{Space}
}                                             ;  ------------------------------------- r t y o p     g b     m s
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F9 & O 橙色 Tyora 背景色   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 10 

F7 & 1::b201(12)
F7 & 2::b201(14)
F7 & 3::b201(16)
F7 & 4::b201(18)
F7 & 5::b201(20)
F7 & 6::b201(22)
F7 & 7::b201(24)

b201(size)
{
    clipboard := ""          ; 清空剪贴板
    SendInput ^x             ; 剪切选中的文本
    Sleep, 100               ; 等待剪贴板有内容
    ClipWait                 ; 等待剪贴板内容更新
    ; 设置新的剪贴板内容
    clipboard := "<span style='font-family: KaiTi; font-size: " size "pt;'>" clipboard "</span>"
    ; 等待剪贴板内容更新    color: #d7003a;
    ClipWait
    ; 粘贴新的内容
    SendInput ^v
    ; 光标左移 7 次
    Send {Left 7}
}
return
#IfWinActive
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F7 & 1-7  Tyora 字号   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 11 

;🎁🎁🎁🎁🎁🎁🎁🎁🎁🎁🎁  颜色  处理  🎁🎁🎁🎁🎁🎁🎁🎁🎁🎁🎁
;👔👔👔👔👔👔👔👔👔👔👔  段落  处理  👔👔👔👔👔👔👔👔👔👔👔

#F2::
if (onoff := !onoff)
	{
	Send {home}
	}
else
	{
    	Send {end}
keywait, F2
}
 Return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   #F2 行首 行尾    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 04

#F3::
if (onoff := !onoff)
	{
	Send #!{home}
	}
else
	{
    	Send #!{end}
keywait, F3
}
 Return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  #F3 段首 段尾    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 05 

#F4::
if (onoff := !onoff)
	{
send, ^a{left}
	}
else
	{
send, ^a{right}
	keywait, F4
	}
 Return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   #F4 页首 页尾   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 06 


;👔👔👔👔👔👔👔👔👔👔👔  段落  处理  👔👔👔👔👔👔👔👔👔👔👔
;🎀🎀🎀🎀🎀🎀🎀🎀🎀🎀🎀  空行  处理  🎀🎀🎀🎀🎀🎀🎀🎀🎀🎀🎀

F6 & 1::
    Clipboard := ""
    Send, ^c
    ClipWait, 2
    Clipboard := RegExReplace(Clipboard, "(\R\s*){2,}", "`r`n`r`n")
    Send, ^v
return
; 当我们使用 "`r`n" 时，它只会将光标移动到下一行的开始，但不会创建一个空行。使用 "`r`n`r`n" 实际上是创建了两个连续的换行符，这就会产生一个空行的效果.
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   选中 合并多行空行为１行   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 13

F6 & 2::
SetWorkingDir, %A_ScriptDir%  ; 设置工作目录

; 复制内容到剪贴板
Send, ^c
ClipWait, 2
if ErrorLevel
{
    MsgBox, 复制失败或超时
    return
}

; 处理剪贴板内容
text := Clipboard
text := StrReplace(text, "`r")  ; 移除所有回车符

; 使用数组存储唯一行
lines := StrSplit(text, "`n")
uniqueLines := {}
output := ""

for index, line in lines
{
    if (line != "") {  ; 忽略空行
        if (!uniqueLines.HasKey(line)) {
            uniqueLines[line] := true
            output .= line . "`n"
        }
    }
}

; 移除最后一个换行符
output := RTrim(output, "`n")

; 将结果写回剪贴板
Clipboard := output
Send, ^v

return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   选中 删除空行    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 13

F6 & 3::
    Clipboard := ""
    Send, ^c
    ClipWait
    Clipboard := RegExReplace(Clipboard, "\R", "`r`n`r`n")
    Send, ^v
return                                                                   ;-------回车变换行即增加一行
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   选中 添加空行    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 13

F6 & 4::
clipboard =
send, ^c
sleep, 100
a = %clipboard%
stringreplace, out, a, ` , `n, All
send, %out%
return                                                                   ;-------回车变换行即增加一行．和上面的区别：空格处也变换行　
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   选中 空格及回车 变换行    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 13

F6 & 5::
    Clipboard := ""  ; 清空剪贴板
    Send, ^c         ; 发送 Ctrl+C 复制选中的文本
    ClipWait, 1     ; 等待最多 1 秒，直到剪贴板有内容
    if (ErrorLevel) {
        MsgBox, 剪贴板没有内容，请确保已选中文本。
        return
    }
    ; 使用更简单的正则表达式来替换换行符
    Clipboard := RegExReplace(Clipboard, "\s*[\r\n]+\s*", "")  ; 替换多个换行符为空格
    Send, ^v         ; 粘贴处理后的内容
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   多行文字合并成一行    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 13

;🎀🎀🎀🎀🎀🎀🎀🎀🎀🎀🎀  空行  处理  🎀🎀🎀🎀🎀🎀🎀🎀🎀🎀🎀
;🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️  空格  处理  🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️

F6 & 6::
	Clipboard := ""
	Send, ^c
	ClipWait
	Clipboard := RegExReplace(Clipboard, "[ \R]+", "$1")
sleep, 400
send, ^v
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   选中 删除空格    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 13

F6 & 7::
	Clipboard := ""
	Send, ^c
	ClipWait
	Clipboard := RegExReplace(Clipboard, "[ \R]+", " ")
sleep, 400
send, ^v^a
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   选中 多个空格变一个   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 13

F6 & 8::
	Clipboard := ""
	Send, ^c
	ClipWait
	Clipboard := RegExReplace(Clipboard, "m)^[ \R]+|[ \R]+$", "$1")
	Clipboard := Trim(clipboard)
sleep, 400
send, ^v
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   选中  只删除首尾空格    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 13

F6 & 9::
clipboard =
send, ^c
sleep, 500
Loop
{
StringReplace, clipboard, clipboard, `t ,` , UseErrorLevel                         ;  注意`后有个空格    空格表示法 `
    if ErrorLevel = 0
        break
}
sleep,200
send,^v
return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   Tab替换成空格    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 13

;🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️  空格  处理  🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️🎞️
;🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒  马克  文档  🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒

#If (WinActive("ahk_exe Typora.exe") or WinActive("ahk_exe Joplin.exe"))                  ;---仅Typora  Joplin 

F6 & F1::
	clipboard := ""
    	SendInput,^x
	sleep,100
	clipboard = #  <span style="font-family:KaiTi; font-size:30px; color: #d7003a">%clipboard%</span>  [^0]   ; ------------- 12 握了请握  [^012] {left}
	SendInput {ctrl down}v{ctrl up}{home}{up}{right 2}
return
#If
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F1 标题添加序号等   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01 

#If (WinActive("ahk_exe Typora.exe") or WinActive("ahk_exe Joplin.exe"))
F6 & F2::
	send {space 2}
	clipboard = - [ ] <span style="color: #4c221b">确定已经掌握了请打上对勾！</span>
	SendInput {ctrl down}v{ctrl up}                      ; ------------- 确定已经掌握了请打上对勾！
return
#If
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F2 确定已经掌握了请打上对勾   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01 

#If (WinActive("ahk_exe Typora.exe") or WinActive("ahk_exe Joplin.exe"))

 F6 & F4::zaa()
	zaa()
{
	clipboard := ""
	Send ^x
	Sleep 500
	clipboard = <center>%clipboard%</center>
	Sleep 50
	Send ^v
}
return
#IfWinActive
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F4 Tyora 居中  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01 

#If (WinActive("ahk_exe Typora.exe") or WinActive("ahk_exe Joplin.exe"))

F6 & F5::
	send >✌️ 
	sleep, 100
	send {enter}{bs}{enter}{left 2}
return
#If
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F5  > :v:   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01 

#If (WinActive("ahk_exe Typora.exe") or WinActive("ahk_exe Joplin.exe"))

F6 & F7::zc()
	zc()
{
	clipboard := ""
	Send ^x
	Sleep 500
	clipboard = ``%clipboard%``
	Sleep 50
	Send ^v
}
return
#If
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F7 Tyora 代码块  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01 

#If (WinActive("ahk_exe Typora.exe") or WinActive("ahk_exe Joplin.exe"))

 F6 & F8::zb()
	 zb()
{
	clipboard := ""
	Send ^x
	Sleep 500
	clipboard = ^%clipboard%^
	Sleep 50
	Send ^v
}
return
#If
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F8 上标   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01 

#If (WinActive("ahk_exe Typora.exe") or WinActive("ahk_exe Joplin.exe"))

 F6 & F9::zd()
	zd()
{
	clipboard := ""
	Send ^x
	Sleep 500
	clipboard = ~%clipboard%~
	Sleep 50
	Send ^v
}
return
#If
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F9 下标   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 01 

;🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒  马克  文档  🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒
;🧧🧧🧧🧧🧧🧧🧧🧧🧧🧧🧧  观察  设置  🧧🧧🧧🧧🧧🧧🧧🧧🧧🧧🧧`