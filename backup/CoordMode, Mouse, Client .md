## CoordMode, Mouse, Client 

```
 CoordMode, Mouse, Client  ; 设置坐标模式为客户端
F1 & c::
Run "C:\Program Files\Google\Chrome\Application\chrome.exe" --new-window, , max
WinWait, ahk_exe chrome.exe, , 5  ; 最多等待 5 秒

Send, ^t
Sleep, 100
Send, ^+{Del}                                                       ; 执行 Ctrl + Shift + Delete
Sleep, 1000

; 定义点击次数和位置
clickCount := 1  ; 设置需要点击的次数
xPos := 978      ; 点击的 X 坐标（根据 Client 坐标调整）
yPos := 617       ; 点击的 Y 坐标（根据 Client 坐标调整）

; 循环执行 ControlClick
Loop, %clickCount%
{
    ControlClick, x%xPos% y%yPos%, ahk_class Chrome_WidgetWin_1
    Sleep, 300  ; 每次点击后暂停300毫秒，确保应用程序有时间处理请求
}
send, ^w
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F1 & C  打开 chrome     ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00011-969
```
