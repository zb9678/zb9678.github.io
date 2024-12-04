## 解码

```
+#d::
send, ^c
Run, wscript.exe "D:\ahk1.0\fg.vbs" 
sleep, 2000

b64Decode(string)
{
    if !(DllCall("crypt32\CryptStringToBinary", "ptr", &string, "uint", 0, "uint", 0x1, "ptr", 0, "uint*", size, "ptr", 0, "ptr", 0))
        throw Exception("CryptStringToBinary failed", -1)
    VarSetCapacity(buf, size, 0)
    if !(DllCall("crypt32\CryptStringToBinary", "ptr", &string, "uint", 0, "uint", 0x1, "ptr", &buf, "uint*", size, "ptr", 0, "ptr", 0))
        throw Exception("CryptStringToBinary failed", -1)

    return StrGet(&buf, size, "UTF-8") ; 确保返回 UTF-8 编码的字符串
} 

decoded := b64decode(clipboard)
FileAppend, % decoded , d:\5.txt ; 写入文件
sleep, 1000
Run, nircmd.exe clipboard readfile "d:\5.txt"
return
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