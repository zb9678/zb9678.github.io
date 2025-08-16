`
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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   #F2 行首 行尾    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 09-2625

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  #F3 段首 段尾     ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 10 -2638

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   #F4 页首 页尾    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 11-2651


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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ F6 & 1  选中 合并多行空行为１行   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 12-2665

F6 & 2::
SetWorkingDir, %A_ScriptDir%  ; 设置工作目录

; 复制内容到剪贴板
Send, ^c
ClipWait, 2
sleep, 200
if ErrorLevel
{
    MsgBox, 复制失败或超时
    return
}

; 处理剪贴板内容
text := Clipboard
text := StrReplace(text, "`r")  ; 移除所有回车符

; 使用数组存储非空行
lines := StrSplit(text, "`n")
output := ""

for index, line in lines
{
    if (line != "") {  ; 忽略空行
        output .= line . "`n"
    }
}

; 移除最后一个换行符
output := RTrim(output, "`n")

; 将结果写回剪贴板
Clipboard := output
Send, ^v

return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ F6 & 2  选中 删除空行   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 13-2706

F6 & 3::
    Clipboard := ""
    Send, ^c
    ClipWait
    Clipboard := RegExReplace(Clipboard, "\R", "`r`n`r`n")
    Send, ^v
return                                                                   ;-------回车变换行即增加一行
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F6 & 3 选中 添加空行   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 14-2715

F6 & 4::
clipboard =
send, ^c
sleep, 100
a = %clipboard%
stringreplace, out, a, ` , `n, All
send, %out%
return                                                                   ;-------回车变换行即增加一行．和上面的区别：空格处也变换行　
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ F6 & 4  选中 空格及回车 变换行  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 15-2725

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F6 & 5 多行文字合并成一行  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 16-2739

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ F6 & 6  选中 删除空格   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 17-2752

F6 & 7::
	Clipboard := ""
	Send, ^c
	ClipWait
	Clipboard := RegExReplace(Clipboard, "[ \R]+", " ")
sleep, 400
send, ^v^a
	return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F6 & 7  选中 多个空格变一个  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 18-2762

F6 & 8::
	Clipboard := ""
	Send, ^c
	ClipWait
	Clipboard := RegExReplace(Clipboard, "m)^[ \R]+|[ \R]+$", "$1")
	Clipboard := Trim(clipboard)
sleep, 400
send, ^v
	return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F6 & 8  选中  只删除首尾空格  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 19-2773

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
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F6 & 9 Tab替换成空格    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 20-2788

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

;🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒  马克  文档  🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒🛒
;🧧🧧🧧🧧🧧🧧🧧🧧🧧🧧🧧  观察  设置  🧧🧧🧧🧧🧧🧧🧧🧧🧧🧧🧧

F5 & b::
    Process, Exist, uTools.exe       ; 检查程序是否已经在运行
    if (ErrorLevel)      ;根据 ErrorLevel 的值来决定是关闭程序还是启动程序，而不再依赖于 isRunning 状态变量。这可以避免因状态更新不及时而导致的需要按两次热键的问题。
    {
                                                                          ; 如果程序正在运行，则关闭它
        Process, Close, uTools.exe
        isRunning := false     ; 更新状态为未运行
    } 
    else 
    {
                                                                      ; 如果程序没有在运行，则启动它
        Run, C:\Users\z\AppData\Local\Programs\utools\uTools.exe
sleep, 1000
send, ^2
        isRunning := true      ; 更新状态为正在运行
    }
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F5 & b 启动 / 关闭uTools.exe  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00010-2909




/*
保存后  自动刷新脚本                                        01-45
复制后通知                                                            02-68
限制单进程运行                                                         03-95
art+q 批量复制粘贴                                          04-249
 >! 2345sdf复制  wertxcv 粘贴                       05-322
 >^c 复制文件名 >^x 获取路径                     06-369
 >^v 对文件夹文件粘贴文件名                      07-376
Appskey & 1  全屏截存桌面选格式                      001-392
Appskey & 6 当前窗口 截图并贴图                     002-399
Appskey & 2  录屏gif                                        003-405
Appskey & 3 录屏MP4                                       004-411
Appskey & 4  剪贴板中截图保存于desktop                 005-415
Appskey & 5  后台间隔截图 全屏                      008-492
shift+alt+a  框选画中画                                        009-495
win+Esc  框选OCR                                         010-498
+#s  截图  剪贴板 desktop                                     011-507
<!esc  截图 OCR                                                      012-518
F9+9 贴图                                                              013-588
Shift+鼠标滚动   改变粘贴的透明度                            014-588
鼠标滚轮改变贴图大小 双击关闭                              015-588
F9+0 隐藏或显示所有粘贴                                    016-619
F9+- 关闭贴图                                                           017-632
F9+= 打开图并设置为贴图                                     018-639
F9 & 8 剪贴板贴图 放大到1.25倍                       019-645
F1 & y 右键属性                                                         0001-653
F1 & k 打开快捷方式的文件夹                       00004-838
^+z 打开当前活动窗口的文件夹                      00005-846
Rctrl & 5 打开 v2rayN                                       00007-887
Rctrl & t 打开托盘 v2rayN                                    00008-894
F1 & [ 启动 F1 & ] 退出 SnoMouse                    00009-917
Rctrl & 1  打开 chrome                                        00011-969
Rctrl & 2   打开 EmEditor                                      00012-999
Rctrl & 3  打开 资源处理器                                      00013-1026
Rctrl & 4  打开 微信                                          00014-1062
F6 & d 大小写 首字母大写                                       000002-1124
shift+中键按下 复原                                                      000004-1176
NumpadEnter 重启脚本                                     000005-1180
+appskey   Tab                                                       000006-1187
<^!z   撤消                                                           000007-1192
<!z  窗口左半，右半切换                                       000008-1261
< !x  切换窗口  70%·····100%                                       000009-1329
!+左键 移窗口 #+左键 调窗口大小                    000011-1363
 >^b  单 新建文件夹 双 TxT文件  名为剪贴板                  000013-1506
F12  代理 变量 管理 控制台 组件服务                   000015-1571
F11 控制面板 IP 组策略 网络连接 共享                    000016-1593
CapsLock  浏览器  1全局 2auto 3直连                    000017-1631
 >^q 上一页                                                         000018-1637
 >^e 下一页                                                         000019-1643
F4 & 0  计时器                                                       000020-1660
++ keepast                                                            0000001-1665
<!1 复整行　<!q 到行首  <!a 到行尾                   0000002-1679
<!2 粘整行  <!w 光标前 <!s 光标后                     0000003-1690
<!3 剪整行  <!e 光标前   <!d 光标后                    0000004-1701
<#1选整行　<#q到行首 <#a到行尾                    0000005-1712
<#2 选整段  <#w光标前 <#s光标后                    0000006-1723
<#3 删整行 <#e 光标前 <#d 光标后                   0000007-1736
F2 & F1 快速向上滚动                                                      00000001-1765
F2 & F3 快速向下滚动                                                      00000002-1789
F2 & Esc 缓慢向上滚动                                                     00000003-1812
F2 & F4 缓慢向下滚动                                                      00000004-1838

F1 & z  上传截图到github/img                                    000001-1984
F1 & x  上传截图到github/img                                    000002-2000
F1 & c  上传截图到图库                                        000003-2013
F1 & v  上传截图到图库                                        000004-2037
F1 & b  上传剪贴板中的文件                                     000005-2051
F1 & n  上传剪贴板中的文件                                     000006-2067
adws 上 下 左 右                                                       0000001-2076
q 退格 e 删除 f 回车                                                     0000002-2081
AppsKey & g 任意位置回                                       0000003-2087
F1 & 1 用Evething搜索选中的文字                         00000001-2102
F1 & 2   谷歌翻译  中/ 英                                       00000002 -2128
F1 & 3 Mobi                                                         00000003-2183
 F1 & 4 用百度搜索选中的文字                               00000004-2190
 F1 & 5 用谷歌搜索选中的文字                               00000005-2197
F1 & 6 Mobi                                                         00000006-2220
 F1 & 7 腾讯翻译                                                   00000007-2227
 F1 & 8  youtube                                                  00000008-2235
 F1 & 0 百度翻译                                                   00000009-2242
F1 & = 腾讯翻译                                                   00000009-2252
 F1 & 9  wiki                                                         00000010-2260
F4 & z 注销                                                           000000001-2280
F4 & c 重启                                                           000000002-2285
F4 & g 关机                                                          000000003-2291
F4 & d 待机                                                          000000004-2299
F4 & q 重启资源管理器                                         000000005-2305
F4 & q 重启资源管理器                                         000000006-2312
F4 & p 关屏                                                          000000007-2318

3个12345  aoeiuü                                                 01-2354
`m::<br>                                                               02-2368
。，：；、 • ……                                                   03 -2380
F6 & O 橙色   joplin字体颜色                                04 -2434
F7 & O 橙色   joplin字体颜色                                05-2484
F8 & O 橙色 Tyora 背景色                                    06 -2532
F9 & O 橙色 Tyora 背景色                                    07-2582
F7 & 1-7  Tyora 字号                                            08-2609
#F2 行首 行尾                                                       09-2625
#F3 段首 段尾                                                       10 -2638
#F4 页首 页尾                                                       11-2651
F6 & 1  选中 合并多行空行为１行                         12-2665
F6 & 2  选中 删除空行                                          13-2706
F6 & 3 选中 添加空行                                           14-2715
F6 & 4  选中 空格及回车 变换行                            15-2725
F6 & 5 多行文字合并成一行                                  16-2739
F6 & 6  选中 删除空格                                          17-2752
F6 & 7  选中 多个空格变一个                                18-2762
F6 & 8  选中  只删除首尾空格                               19-2773
F6 & 9 Tab替换成空格                                           20-2788
F6 & F1 标题添加序号等                                        001-2803 
F6 & F2 确定已经掌握了请打上对勾                       002-2812 
F6 & F4 Tyora 居中                                               003-2828
F6 & F5  > :v:                                                        004-2838 
F6 & F7 Tyora 代码块                                            005-2854
F6 & F8 上标                                                         006-2870
F6 & F9 下标                                                         007-2886

F5 & v  FSCapture.exe                                          006-452
F5 & b  Umi-OCR.exe                                           007-487
F5 & 1  隐藏任务栏                                                0002-679
F5 & 2  隐藏桌面图标                                            0003-690
F5 & 3  隐.显桌面                                                  0004-706
F5 & - 显示扩展名 F5 & = 显隐文件                      0005-728
F5 & 4  缩略图                                                      0006-757
F5 & 5 显示预览窗格                                             0007-762
F5 & 6  窗口置顶                                                   0008-782
F5 & e  帮助文档                                                   00001-796
F5 & 9  快捷键目录                                                00002-801
F5 & 0  快捷键目录                                               00003-806
F5 & 8   EmEditor打开3文件                                 00006-856
F5 & c[ 启动 / 关闭ZoomIt64.exe                          00010-938
F5 & /  VS Code                                                   00015-1067
F5 & F4  AltTab                                                    000001-1074
F5 & ,   锁键盘鼠标                                                000003-1129
F5 & 7  二维码                                                      000010-1340
F5 & . 切换鼠标左右键                                           000012-1467
F5 & u  文字转语音                                               000014-1531
F5 & o 获得 RGB 值                                              000000001-1853
F5 & p 显示颜色                                                    000000002-1890
F5 & [  颜色值 鼠标跟随                                         000000003-1951
F5 & ] 获取当前鼠标指针的坐标                             000000004-1959
F5 & b 启动 / 关闭uTools.exe                               00010-2909
*/
`