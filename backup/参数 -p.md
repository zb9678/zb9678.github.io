## RunWait, "C:\AutoHotkey\v1\AutoHotkey.exe" "GetPassword.ahk" /p

## RunWait, "C:\AutoHotkey\v2\AutoHotkey.exe" "GetPassword.ahk" /p

- 注意：系统安装了2种版本V1,V2，要安装在不同位置。
-  RunWait,  “D:\ahk1.0\GetPassword.ahk" /p  会无法搞清是哪个版本来运行脚本。
- 如果你的脚本开头有 #Requires AutoHotkey v1.1.36：
即使脚本使用的是错误版本的解释器（例如 v2），解释器也会提示版本不匹配并终止运行。这是一个安全措施，防止脚本被错误的解释器执行。
但它无法自动切换到正确的版本；你仍需手动调整环境或明确指定解释器路径。

RunWait

AutoHotkey 的内置命令，用于运行外部程序。
RunWait 的特点是暂停当前脚本的执行，直到被调用的外部程序或脚本完成后才继续。

AutoHotkey.exe

调用 AutoHotkey 主程序。
如果系统配置了环境变量，直接写 AutoHotkey.exe 即可；否则，需要提供完整路径，比如：C:\Program Files\AutoHotkey\AutoHotkey.exe

/p

传递给脚本的自定义参数。
参数 /p 将通过 AutoHotkey 提供的命令行参数机制传递给 GetPassword.ahk，供其内部使用。

## 示例脚本和输出
假设你的 GetPassword.ahk 文件内容如下：

```
if (A_Args.Length() > 0) {
    MsgBox % "传递的参数是：" A_Args[1]
} else {
    MsgBox "没有传递任何参数"
}
```
运行：RunWait, "C:\AutoHotkey\v1\AutoHotkey.exe" "GetPassword.ahk" /p

弹出消息框：传递的参数是：/p


## 如果改为：RunWait, "C:\AutoHotkey\v1\AutoHotkey.exe" "GetPassword.ahk"

弹出消息框：没有传递任何参数

/p 是命令行参数，脚本会通过 A_Args 变量接收它。
它的实际作用完全由脚本 GetPassword.ahk 决定，通常用来触发某种模式或动态调整脚本行为。
使用 RunWait 时，将参数附加到脚本路径后面，用空格分隔即可传递。