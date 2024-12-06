##  利用 edge 的朗读功能将文本转为语音

```
F5 & w::
Clipboard := ""                  ; 清空剪贴板
Send, ^c                         ; 复制选中文本
ClipWait, 2                      ; 等待剪贴板更新
if ErrorLevel
{
    MsgBox, 未能检测到剪贴板内容，请检查是否已选中内容！
    Return
}
filePath := "C:\Users\z\Desktop\q.htm"
file := FileOpen(filePath, "w", "UTF-8")
file.Write(Clipboard)
file.Close()

Run, "D:\ahk1.0\Lib\0 tool\录音.exe"
WinWait, ahk_exe 录音.exe, , 5
if !ErrorLevel
{
    WinHide, ahk_exe 录音.exe  ; 隐藏窗口
}
;MouseClick, left, 255, 17
sleep, 4000 
;录音.exe的快捷键即使在后台也可以激发, 而msedge.exe不行,
;所以要等它彻底启动后再启动msedge.exe, 以使得msedge.exe为当前窗口
Run, msedge.exe "C:\Users\z\Desktop\q.htm"

sleep, 2000
Send,  ^+u
sleep, 20
Send,  ^+{space}
send, <!ju                    　　　　　  ; 开VPN会影响录音启动的时间，所以要关掉。
sleep, 30000
send, !u
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F5 & w  文字转语音    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 000014-1531
```

##  安装xiaoxiao

<p align="center"><img src="https://jsd.cdn.zzko.cn/gh/zb9678/img@main/up1/12.06:08:18:14.png" style="width:400px;"></p>

## 选择使用xiaoxiao

<p align="center"><img src="https://jsd.cdn.zzko.cn/gh/zb9678/img@main/up1/12.06:08:20:57.png" style="width:400px;"></p>