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

##

```
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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F6 & O 橙色   joplin字体颜色  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 04 -2434

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F7 & O 橙色   joplin字体颜色  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 05-2484

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F8 & O 橙色 Tyora 背景色    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 06 -2532

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F9 & O 橙色 Tyora 背景色    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 07-2582

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F7 & 1-7  Tyora 字号    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 08-2609
```