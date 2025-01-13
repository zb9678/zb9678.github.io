## TrayTip

0=没有图标（默认）
1=消息
2=警告
3=错误

```
v::
TrayTip, 第1个气球提示, 我是消息, , 3
sleep, 1000
TrayTip, 第2个气球提示, 确定, , 1
sleep, 1000
TrayTip, 第3个气球提示, 确定, , 2
sleep, 1000
TrayTip, 第4个气球提示, 确定, , 0
```
<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/up1/01.13:19:18:25.png" style="width:400px;"></p>


##  仅在notepad中交换a、b键

#IfWinActive ahk_class Notepad

a::b 
b::a

#IfWinActive ;