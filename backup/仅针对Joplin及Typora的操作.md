## 仅针对Joplin及Typora的操作

```
#If (WinActive("ahk_exe Typora.exe") or WinActive("ahk_exe Joplin.exe"))                  ;---仅Typora  Joplin 

F6 & F1::
	clipboard := ""
    	SendInput,^x
	sleep,100
	clipboard = #  <span style="font-family:KaiTi; font-size:30px; color: #d7003a">%clipboard%</span>  [^0]   ; ------------- 12 握了请握  [^012] {left}
	SendInput {ctrl down}v{ctrl up}{home}{up}{right 2}
return
#If
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F1 标题添加序号等    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 001-2803 

#If (WinActive("ahk_exe Typora.exe") or WinActive("ahk_exe Joplin.exe"))
F6 & F2::
	send {space 2}
	clipboard = - [ ] <span style="color: #4c221b">确定已经掌握了请打上对勾！</span>
	SendInput {ctrl down}v{ctrl up}                      ; ------------- 确定已经掌握了请打上对勾！
return
#If
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F2 确定已经掌握了请打上对勾    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 002-2812 

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F4 Tyora 居中   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 003-2828

#If (WinActive("ahk_exe Typora.exe") or WinActive("ahk_exe Joplin.exe"))

F6 & F5::
	send >✌️ 
	sleep, 100
	send {enter}{bs}{enter}{left 2}
return
#If
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F5  > :v:    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 004-2838 

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F7 Tyora 代码块   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 005-2854

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F8 上标    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 006-2870

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & F9 下标    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 007-2886
```