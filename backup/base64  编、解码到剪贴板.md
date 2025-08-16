## 解码

```
+#d::
    Clipboard := "" ; 清空剪贴板
    send, ^c ; 复制剪贴板内容
    ClipWait, 1 ; 等待剪贴板内容更新，超时为1秒
    if (ErrorLevel) {
        MsgBox, 剪贴板未能成功更新！
        return
    }
    decoded := b64Decode(clipboard) ; 解码剪贴板内容

    file := FileOpen("D:\5.txt", "w", "UTF-8") ; 打开文件并指定为 UTF-8 编码
    file.Write(decoded) ; 写入解码后的内容
    file.Close() ; 关闭文件
sleep, 1000
Run, nircmd.exe clipboard readfile "d:\5.txt"
return 

b64Decode(string)
{
    if !(DllCall("crypt32\CryptStringToBinary", "ptr", &string, "uint", 0, "uint", 0x1, "ptr", 0, "uint*", size, "ptr", 0, "ptr", 0))
        throw Exception("CryptStringToBinary failed", -1)
    VarSetCapacity(buf, size, 0)
    if !(DllCall("crypt32\CryptStringToBinary", "ptr", &string, "uint", 0, "uint", 0x1, "ptr", &buf, "uint*", size, "ptr", 0, "ptr", 0))
        throw Exception("CryptStringToBinary failed", -1)

    return StrGet(&buf, size, "UTF-8") ; 确保返回 UTF-8 编码的字符串
}
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   base64解码到剪贴板 +#d   ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 8-182

```

## 编码

```
+#f::
send, ^c
sleep, 400
Run, wscript.exe "D:\ahk1.0\fg.vbs"
sleep,2000

b64Encode(string)
{
    VarSetCapacity(bin, StrPut(string, "UTF-8")) && len := StrPut(string, &bin, "UTF-8") - 1
    if !(DllCall("crypt32\CryptBinaryToString", "ptr", &bin, "uint", len, "uint", 0x1, "ptr", 0, "uint*", size))
        throw Exception("CryptBinaryToString failed", -1)
    VarSetCapacity(buf, size << 1, 0)
    if !(DllCall("crypt32\CryptBinaryToString", "ptr", &bin, "uint", len, "uint", 0x1, "ptr", &buf, "uint*", size))
        throw Exception("CryptBinaryToString failed", -1)
    return StrGet(&buf)
}
FileAppend, %  b64encode( clipboard ) , d:\5.txt
sleep, 1000
Run, nircmd.exe clipboard readfile "d:\5.txt"
return
;ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ   base64编码到剪贴板 +#f    ΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞΞ 9-203

```

## 详解

```
+#d::
    Clipboard := "" ; 清空剪贴板
    send, ^c ; 复制剪贴板内容
    ClipWait, 1 
    if (ErrorLevel) {
        MsgBox, 剪贴板未能成功更新！
        return
    }    ;等待剪贴板更新：ClipWait, 1 等待剪贴板在最多 1 秒内更新。如果未能更新，则显示消息框并退出。
```

 'decoded := b64Decode(clipboard) ; 解码剪贴板内容'

- 解码操作：调用 b64Decode 函数，将剪贴板中的 Base64 编码字符串解码为原始字符串，并将结果存储在 decoded 变量中。


```

## file := FileOpen("D:\5.txt", "w", "UTF-8")

- FileOpen：这是 AutoHotkey 中用于打开文件的函数。
- "D:\5.txt"：这是要打开的文件的路径。如果文件不存在，FileOpen 将会创建一个新文件。
- "w"：这是访问模式，表示以写入模式打开文件。如果文件已存在，它将被覆盖。
- "UTF-8"：指定文件的编码格式为 UTF-8。这意味着写入到该文件的内容将以 UTF-8 编码格式保存。

## file.Write(decoded) 

```
- file.Write(decoded)：这行代码将 decoded 变量中的内容写入到D:\5.txt中。decoded 应该是经过 Base64 解码后的字符串。
- 由于在打开文件时指定了 UTF-8 编码，写入的内容将被正确编码为 UTF-8，从而避免了乱码问题。
```

### file.Close() 

`file.Close()：这行代码用于关闭之前打开的文件。关闭文件是良好的编程习惯，可以确保所有数据都被正确写入，并释放系统资源。`