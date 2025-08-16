`#SingleInstance force
isRunning := false                                                ;---- 用于跟踪脚本是否在运行
timerRunning := false                                          ;-- 用于跟踪定时器是否在运行

F5 & b::                                             
    	Process, Exist, Umi-OCR.exe                   ; --------检查程序是否在运行
    	if (ErrorLevel) 
{
        	Process, Close, Umi-OCR.exe                 ;---- 如果程序在运行则关闭它
        	isRunning := false                                  ;----------- 更新状态为未运行
        	SetTimer, AutoCloseUmi-OCR, Off        ;------------------ 关闭定时器
        	timerRunning := false                            ;------------- 更新定时器状态
}
else 
{
        	Run, "D:\ahk1.0\Lib\0 tool\Umi-OCR_Rapid_dev_20231025\Umi-OCR.exe"
        	Sleep, 1700
        	Send, +^!z                                             ;-------------截图快捷键 +^!z  
       	isRunning := true                                   ;--------  更新状态为正在运行

        	if (!timerRunning)                                   ;----------- 如果定时器未运行
       {                                          
            	SetTimer, AutoCloseUmi-OCR, -11000  ; --------------------------设置一个11秒的单次定时器
            	timerRunning := true                             ;---- 更新定时器状态为运行中
       }
}
return
;----------------------------------------------------------------------------定时器
AutoCloseUmi-OCR:
    	Process, Close, Umi-OCR.exe                ;------------自动关闭截图软件
    	isRunning := false                                  ;----------- 更新状态为未运行
    	timerRunning := false                            ;---- 更新定时器状态为未运行
	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F5 & b  Umi-OCR.exe  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 005`