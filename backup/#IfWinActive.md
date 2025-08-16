> [!TIP]
> 仅在notepad中交换a、b键


```
#IfWinActive ahk_class Notepad
a::b 
b::a
#IfWinActive 
```