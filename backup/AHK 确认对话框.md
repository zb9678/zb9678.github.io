`DetectHiddenWindows, On                                 ;------ 启用对隐藏窗口的检测
SetTitleMatchMode, 2                                           ;----------- 设置标题匹配模式

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
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F1 & [ 启动 F1 & ] 退出 SnoMouse  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00009`