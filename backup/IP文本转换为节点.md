## 获取IP

- https://www.lddgo.net/network/randomip

- 162.159.0.0    162.159.0.255

- 2803:f800:51::/48

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/up1/02.19:11:45:14.png" style="width:400px;"></p>

## 获取 IPv4 节点 （数量根据4.txt中的IP数量决定）

- ahk脚本目录下建立IP库文本文件 4.txt 内容如下

104.17.253.154
104.17.253.229
104.17.253.127...........

- 注意 6784c6ee-cc88-419b-8fee-ca090dbaa428 和 edk.v07.us.kg  成对修改

- 修改 #104

```
F1 & j::  
    ; 读取剪贴板内容
    ;originalText := Clipboard
     originalText := "vless://6784c6ee-cc88-419b-8fee-ca090dbaa428@104.21.236.177:443?encryption=none&security=tls&sni=edk.v07.us.kg&type=ws&host=edk.v07.us.kg&path=%3Fed%3D2560#104"
                                            ; 可修改  6784c6ee-cc88-419b-8fee-ca090dbaa428和edk.v07.us.kg     以及最后的#C  
    ; 读取 IP 列表文件
    ipList := []
    Loop, Read, 4.txt
    {
        ipList.Push(A_LoopReadLine)  ; 逐行读取并存入数组
    }

    newText := ""  ; 存储最终文本

    ; 依次替换 IP
    for index, ip in ipList
    {
        newText .= StrReplace(originalText, "104.21.236.177", ip) . "`n"
    }

    ; 写入剪贴板
    Clipboard := RTrim(newText, "`n")
    ;MsgBox, 生成完成，已复制到剪贴板！
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & j 将4.txt中的IP替换为节点   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000004-3062
```

## IPv6

- ahk脚本目录下建立IP库文本文件 6.txt 内容如下

[2803:F800:0051:0000:0000:0000:508C:CB2E]
[2803:F800:0051:0000:0000:0000:7559:838C]
[2803:F800:0051:0000:0000:0000:CE83:4BD6]......

```
F1 & u::  
    ; 读取剪贴板内容
    ;originalText := Clipboard
     originalText := "vless://1ae2d51f-1cfe-4453-b7f5-e2bf8263a9d1@[2606:4700::31ed:42ab]:2096?encryption=none&security=tls&sni=ff.v07.us.kg&fp=random&type=ws&host=ff.v07.us.kg&path=%2F%3Fed%3D2560#83"
                                            ; 可修改  6784c6ee-cc88-419b-8fee-ca090dbaa428和edk.v07.us.kg     以及最后的#C  
    ; 读取 IP 列表文件
    ipList := []
    Loop, Read, 6.txt
    {
        ipList.Push(A_LoopReadLine)  ; 逐行读取并存入数组
    }

    newText := ""  ; 存储最终文本

    ; 依次替换 IP
    for index, ip in ipList
    {
        newText .= StrReplace(originalText, "[2606:4700::31ed:42ab]", ip) . "`n"
    }

    ; 写入剪贴板
    Clipboard := RTrim(newText, "`n")
    ;MsgBox, 生成完成，已复制到剪贴板！
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   F1 & u 将6.txt中的IP替换为节点   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 00000004-3062
```