`#SingleInstance force                                          ;----------- 强制加载新的脚本
isRunning := false                  ; 状态变量: isRunning 用于跟踪脚本是否正在运行

$^esc::                  ; $+esc::
    	if (isRunning) 
	{
      					 ; 1.如果脚本已经在运行，则关闭它
        	Name := "SnoMouse.ahk"                     ;------ 指定要退出的脚本名称
        	DetectHiddenWindows, On                   ;------ 启用对隐藏窗口的检测
       	SetTitleMatchMode, 2 ; 设置标题匹配模式

       	WinClose, %Name% ahk_class AutoHotkey
        isRunning := false 			                        ;-----------更新状态为未运行
    	} 

      else {
       					 ; 2.如果脚本没有在运行，则启动它
        	Run D:\ahk1.0\Lib\SnoMouse.ahk
        isRunning := true                                         ;---------更新状态为正在运行
   	 }
return`