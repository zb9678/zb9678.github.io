Rctrl::
loop,1
SoundBeep, 9000, 20
Send #{Space}
keywait, space
	V++
  	M := mod(V,2)  ;; 模數
  if M=1
  	SetDefaultKeyboard(0x0404)  ;; 切換為中文輸入
  else
  	SetDefaultKeyboard(0x0409)  ;; 切換為英文輸入
  return

SetDefaultKeyboard(LocaleID) 
{
  	Global SPI_SETDEFAULTINPUTLANG := 0x005A
  	SPIF_SENDWININICHANGE := 2
Lan := DllCall("LoadKeyboardLayout", "Str", Format("{:08x}", LocaleID), "Int", 0)
  	VarSetCapacity(Lan%LocaleID%, 4, 0)
  	NumPut(LocaleID, Lan%LocaleID%)
;Lan := 0xE0090404
  	DllCall("SystemParametersInfo", "UInt", SPI_SETDEFAULTINPUTLANG, "UInt", 0, "UPtr", &Lan%LocaleID%, "UInt", SPIF_SENDWININICHANGE)
  	WinGet, windows, List
  	Loop %windows% 
	{
	PostMessage 0x50, 0, %Lan%, , % "ahk_id " windows%A_Index%
	}
}


return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  切换中英输入法   Rctrl  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 4-75

# 上面是下面２种方法的合并

Rctrl::
  V++
  M := mod(V,2)  ;; 模數
  if M=1
    SetDefaultKeyboard(0x0404)  ;; 切換為中文輸入
  else
    SetDefaultKeyboard(0x0409)  ;; 切換為英文輸入
  return

SetDefaultKeyboard(LocaleID) {
  Global SPI_SETDEFAULTINPUTLANG := 0x005A
  SPIF_SENDWININICHANGE := 2
  Lan := DllCall("LoadKeyboardLayout", "Str", Format("{:08x}", LocaleID), "Int", 0)
  VarSetCapacity(Lan%LocaleID%, 4, 0)
  NumPut(LocaleID, Lan%LocaleID%)
  ;Lan := 0xE0090404
  DllCall("SystemParametersInfo", "UInt", SPI_SETDEFAULTINPUTLANG, "UInt", 0, "UPtr", &Lan%LocaleID%, "UInt", SPIF_SENDWININICHANGE)
  WinGet, windows, List
  Loop %windows% {
    PostMessage 0x50, 0, %Lan%, , % "ahk_id " windows%A_Index%
  }
}
  return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  切换中英输入法   Rctrl  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 4-75

Ralt::
if (A_PriorHotkey <> "Ralt" or A_TimeSincePriorHotkey > 400)
{
	; 两次按下时间间隔太长, 所以这不是一个两次按下.
	KeyWait, Ralt
	return
}
{
	loop,3
   	 SoundBeep, 4000, 50
}
{
	Text=全半角
	btt(Text,300,400,,"Style5")
	sleep, 600
	btt()​
	send, +{space}
	return
}
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  全半角  双击  Ralt  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 5-96

Appskey::
	t:=-oldt+(oldt:=A_TickCount)
	if (t<100 || t>300)
    	Return
 	else oldt:=0
{
	loop,3
   	 SoundBeep, 3000, 30
	Text=中英标点
	btt(Text,,,,"Style6")
	sleep, 600
	btt()​
	send, ^.
	Return
}
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 中英标点  双击 Appskey    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 6-113


/*
Rctrl::
	loop,1
	SoundBeep, 9000, 20
	Send ^{Space}
	keywait, space
return
*/