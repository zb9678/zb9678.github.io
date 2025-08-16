## 合并多行空行为１行

```
F6 & 1::
    Clipboard := ""
    Send, ^c
    ClipWait, 2
    Clipboard := RegExReplace(Clipboard, "(\R\s*){2,}", "`r`n`r`n")
    Send, ^v
return
; 当我们使用 "`r`n" 时，它只会将光标移动到下一行的开始，但不会创建一个空行。使用 "`r`n`r`n" 实际上是创建了两个连续的换行符，这就会产生一个空行的效果.
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ F6 & 1  选中 合并多行空行为１行   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 12-2665
```

## 删除所有空行

```
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
```

## 给每行添加空行

```
F6 & 3::
    	Clipboard := ""
    	Send, ^c
    	ClipWait
    	Clipboard := RegExReplace(Clipboard, "\R", "`r`n`r`n")
    	Send, ^v
return                                                                   ;-------回车变换行即增加一行
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F6 & 3 选中 添加空行   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 14-2715
```

## 空格及回车 变换行

```
/*
F6 & 4::
	clipboard =
	send, ^c
	sleep, 100
	a = %clipboard%
	stringreplace, out, a, ` , `n, All
	send, %out%
return                                                                   ;-------回车变换行即增加一行．和上面的区别：空格处也变换行　
*/

F6 & 4::
    	Clipboard := ""
    	Send, ^c
    	ClipWait
    	Clipboard := RegExReplace(Clipboard, "\s", "`r`n")
    	Send, ^v
return  
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ F6 & 4  选中 空格及回车 变换行  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 15-2725
```

## 多行文字合并成一行

```
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
```

## 删除空格

```
F6 & 6::
	Clipboard := ""
	Send, ^c
	ClipWait
	Clipboard := RegExReplace(Clipboard, "[ \R]+", "$1")
sleep, 400
send, ^v
	return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ F6 & 6  选中 删除空格   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 17-2752
```

## 合并多个空格

```
F6 & 7::
	Clipboard := ""
	Send, ^c
	ClipWait
	Clipboard := RegExReplace(Clipboard, "[ \R]+", " ")
sleep, 400
send, ^v^a
	return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ  F6 & 7  选中 多个空格变一个  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 18-2762
```

##  删除首尾空格

```
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
```

##  Tab替换成空格 

```
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
```