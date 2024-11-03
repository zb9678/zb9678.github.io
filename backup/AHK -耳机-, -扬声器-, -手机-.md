`	; 指定 SoundVolumeView 的路径
global SoundVolumeViewPath, devices, currentIndex, command
SoundVolumeViewPath := "D:\ahk1.0\Lib\soundvolumeview-x64\SoundVolumeView.exe"
	; 定义设备名称（确保这些设备名称与 SoundVolumeView 中显示的名称完全匹配）
	devices := ["耳机", "扬声器", "手机"]
	currentIndex := 0  ; 当前设备的索引
appskey & F1::
currentIndex := (currentIndex + 1) > devices.MaxIndex() ? 1 : currentIndex + 1  ; 循环切换  
    	; 拼接命令
command := SoundVolumeViewPath . " /SetDefault """ . devices[currentIndex] . """ ""Render"""
    
    	; 调试：显示生成的命令，检查是否正确
{
    	loop, 1
        	SoundBeep, 400, 10
; 400 声音频率, 可以为表达式. 它是介于 37-32767 之间的数字. 省略则频率为523
; -------------------10 声音的持续时间, 单位为毫秒. 如果省略, 则持续时间为 150      
        	; 显示当前设备名称
        	Text := "⭕    " . devices[currentIndex] . "   ⭕"
        	btt(Text, 600, 10, ,"Style7")
        	sleep, 500
        	btt()
}    
    	Run, %command%                              ; ----------------------执行命令
    	return
; ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ     切换音频设备     ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 1`

# sound_volume_view　下载地址
https://www.nirsoft.net/utils/sound_volume_view.html