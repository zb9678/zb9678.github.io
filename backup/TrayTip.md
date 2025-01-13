> [!TIP]
>0=没有图标（默认）
>1=消息
>2=警告
>3=错误
>20=AHK
>16=为无声音无图标
>17=为无声音信息图标

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

> [!TIP]
>SetTimer

```
c::                                                                          ; 要更精确的控制显示的时间 SetTimer, 而不使用 Sleep 的方法 (它停止了当前线程)
TrayTip, NO.2标题, 第1内容,  , 18
SetTimer, HideTrayTip, 2000                                ; 等待 2 (只用为1-6) 秒关闭通知
HideTrayTip()
{
    TrayTip   
}
return
```

> [!TIP]
> 60 指持续时间为6秒

```
z::
TrayTip , 标题,  第1内容 `n第2行内容 `n第3行内容 `n第4行内容, 60 , 3               ; 60 指持续时间为6秒（可为10.20.30.40.50.60）再设置高没有用。 3 为警告图标  
;TrayTip , 标题,  第1内容 `n第2行内容 `n第3行内容 `n第4行内容 `n第5行内容 `n第6行内容 `n第7行内容                 ; 标题除外，最多显示4行内容,567是无法显示的
return
```

> [!TIP]
> traytip一直不断地出现

``
;使用计时器进行周期性的刷新，使traytip一直不断地出现
x::
SetTimer, RefreshTrayTip7, 13000                       ; 6秒后消失(固定值)，等7秒再次出现(可调)，一直持续   RefreshTrayTip7 如有多个脚本这段文字要用不同的
Gosub, RefreshTrayTip7                                       ; 调用一次来让它立即开始.
return

RefreshTrayTip7:    

TrayTip, 有标题 , 显示内容不超过68个字符 , ,3               ; 有标题的内容文字不超过68个。 
sleep, 6000
TrayTip,  , 无标题，则内容显示不超过102个字符 , ,3        ;无标题  内容不超过102个字符。
return
```


> [!NOTE]
>  仅在notepad中交换a、b键


```
#IfWinActive ahk_class Notepad
a::b 
b::a
#IfWinActive ;
```