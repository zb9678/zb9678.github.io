> [!TIP]
> 空格TAB等转换为换行  1

```
F6 & 4::
	clipboard =
	send, ^c
	sleep, 100
	a = %clipboard%
	stringreplace, out, a, ` , `n, All
	send, %out%
return                                                                   ;-------回车变换行即增加一行．和上面的区别：空格处也变换行　
```

> [!TIP]
> 空格TAB等转换为换行 2

```
F6 & 4::
    	Clipboard := ""
    	Send, ^c
    	ClipWait
    	Clipboard := RegExReplace(Clipboard, "\s", "`r`n")
    	Send, ^v
return  
```

> [!Note]
> 选中 添加空行

```
F6 & 3::
    	Clipboard := ""
    	Send, ^c
    	ClipWait
    	Clipboard := RegExReplace(Clipboard, "\R", "`r`n`r`n")
    	Send, ^v
return
```


;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ F6 & 4  选中 空格及回车 变换行  ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 15-2725