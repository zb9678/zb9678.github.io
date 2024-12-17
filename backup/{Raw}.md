## {Raw}

```
SendInput {Raw}{Tab}
```

<p align="center"><img src="https://cdn.jsdelivr.net/gh/zb9678/img@main/up1/12.17:14:46:50.png" style="width:400px;"></p>

## SendRaw, {Tab}

```
SendRaw
功能： 逐字发送输入，不解析特殊字符（如 {}）。
特点： 直接发送文本，避免特殊字符被解释为按键。
使用场景： 输入原始文本，避免字符冲突。
ahk
复制代码
SendRaw, {Tab}
```